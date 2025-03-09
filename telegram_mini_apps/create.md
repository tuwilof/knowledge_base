## 🛫 Telegram Mini Apps

### Создание Telegram Mini Apps

#### Что не нужно

Сначала надо понять что не нужно. На самом в привычном помнимание вам не нужен телеграм бот, то есть бэкенд обработка.

Так как визуально в ваще телеграм боте будет только кнопка открыть веб версию, а это все делает через ботфазер.

#### Что нужно для МВП в декстопной верси телеграм

* Создайте проект
  * `yarn create @telegram-apps/mini-app`
  * https://docs.telegram-mini-apps.com/packages/telegram-apps-create-mini-app
* перейдите в проект
  * установите yarn install
  * запустите `yarn dev:https`
    * можете проверить в браузере
* перейдите в https://t.me/botfather
  * подробнее https://docs.telegram-mini-apps.com/platform/creating-new-app#creating-application-in-botfather
  * создайте бота `/newbot`
  * создайте ссылку `/newapp`
  * установите ссылку в кнопку `/setmenubutton`

теперь можете првоерить на декстопной версии

на телефоне такой вариант еще не будет работать, так как адрес локальный, надо установить публичный домен через специальные библоитеки

#### Как првоерить МВП на телефоне

* Подробнее
  * https://docs.telegram-mini-apps.com/packages/telegram-apps-mate
  * https://docs.telegram-mini-apps.com/packages/telegram-apps-mate/hosting
* перейдите в каталог с мини приложением
  * установите `yarn add -D @telegram-apps/mate`
  * проверьте что установился `yarn mate -h`
* перейдите в бота https://t.me/tma_mate_bot
  * создайте проект
  * сохраните токен
  * укажите в проекте домен новый
* перейдите в каталог с мини приложением
  * проверьте `yarn mate deploy info --token token --project project --tag latest`
  * соберите `yarn run build`
  * задеплойте `yarn mate deploy upload --dir dist --token token --project project --tag latest`