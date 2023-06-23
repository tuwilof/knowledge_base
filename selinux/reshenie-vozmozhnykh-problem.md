# Решение возможных проблем

#### unicorn.sock failed (13: Permission denied)

```log
2023/04/25 10:17:21 [crit] 149898#0: *1 connect() to 
unix:/opt/xx/tmp/sockets/unicorn.sock failed 
(13: Permission denied) while connecting to upstream, 
client: xx.xx.xx.xx, 
server: xx.xx.io, 
request: "GET /api/xx/v1/xx HTTP/1.0", 
upstream: "http://unix:/opt/xx/tmp/sockets/unicorn.sock:/api/xx/v1/xx", 
host: "xx.xx.io"
```

Для проверки что дело в SElinux его можно отключить

```bash
sudo setenforce 0
```

Хорошая подробная статья&#x20;

{% embed url="https://nts.strzibny.name/allowing-nginx-to-use-a-pumaunicorn-unix-socket-with-selinux/" %}

Если кратко то надо выполнить команду и сохранить вывод в файл **nginx.te**

```bash
sudo grep nginx /var/log/audit/audit.log | audit2allow -m nginx                                                                                                                        
                                                           
module nginx 1.0;                                          
                                                                
require {                                                                                                                                                                                                            
        type httpd_t;                                           
        type initrc_t;                                                                                                                                                                                               
        class unix_stream_socket connectto;              
}                                                         
                                                       
#============= httpd_t ==============                        
allow httpd_t initrc_t:unix_stream_socket connectto;  
```

а затем проверить, скомпилить и подрубить

```
sudo checkmodule -M -m -o nginx.mod nginx.te
sudo semodule_package -o nginx.pp -m nginx.mod
sudo semodule -i nginx.pp
```

должно заработать

так же можно настроить ansible по примеру

{% embed url="https://github.com/nginxinc/ansible-role-nginx/blob/main/tasks/prerequisites/setup-selinux.yml?ysclid=lj8eomy4td530655797" %}

```
#ansible/playbooks/roles/my_app/files/nginx.te
module nginx 1.0;

require {
        type initrc_t;
        type httpd_t;
        class unix_stream_socket connectto;
}

#============= httpd_t ==============
allow httpd_t initrc_t:unix_stream_socket connectto;
```

```
#ansible/playbooks/roles/my_app/tasks/main.yml
    - name: Copy SELinux NGINX module
      copy:
        src: nginx.te
        dest: /tmp/nginx.te

    - name: Check SELinux NGINX module
      ansible.builtin.command: checkmodule -M -m -o /tmp/nginx.mod /tmp/nginx.te

    - name: Compile SELinux NGINX module
      ansible.builtin.command: semodule_package -o /tmp/nginx.pp -m /tmp/nginx.mod

    - name: Import SELinux NGINX module
      ansible.builtin.command: semodule -i /tmp/nginx.pp 
```

