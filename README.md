# Решение задания 1

## Выбор подхода
В качестве подхода к разделению приложения на микрофронтенды был выбран **Module Federation** по следующим причинам:
 1. Мы обеспечиваем управление зависимостями и управление гибкостью проекта, разделяя основные сервисы на маленькие микрофронты
 2. Позволяет разделить код динамически, сохраняя при этом шеринг ресурсов (отдельных компонентов)
 3. Приложение не является большим и сложным, поэтому проблемы в разделении на компоненты и модули не должны возникнуть
 4. Не требуется различный стек для работы фронта
 5. Разделяем ответственность за модулю на микрокоманды (авторизация, пользователи, карты)
 6. Позволяет каждую часть микрофронта масштабировать отдельно

## Структура проекта
Примерная структура проекта после реализации представлена в папке microfrontend и продублирована здесь

### host - Главное приложение
```json
- microfrontend
    - host-app
        - src
            - components
                - Header.js //Общий элемент для header приложения
                - Footer.js //Общий элемент для footer приложения
            - styles
                - footer // Папка из изначального проекта
                - header // Папка из изначального проекта
            index.js
        package.json
        webpack.config.js
```
### authApp - Микрофронтенд авторизации
```json
 - microfrontend
    - authApp
        - src
            - components
                - Login.js
                - Register.js
                - InfoTooltip.js
            - styles
                - auth-form //вся структура из изначального проекта
            - utils
                - auth.js // Перенесена из utils/api
            index.js
        webpack.config.js
```
### App - Микрофронтенд карточки
```json
 - microfrontend
    - cardsApp
        - src
            - components
                - Card.js
                - Main.js
                - AddPlacePopup.js
                - ImagePopup.js
            - styles
                - card
                - page
                - places
                - popup
            - utils
                - cards-api.js // Выделенная из utils/api часть по работе только с карточками
            index.js
        webpack.config.js
```

### App - Микрофронтенд профиля
```json
 - microfrontend
    - usersApp
        - src
            - components
                - EditProfilePopup.js
                - EditAvatarPopup.js
            - styles
                - profile //вся структура из изначального проекта
            - utils
                - users-api.js // Выделенная из utils/api часть по работе только с профилем
            index.js
        webpack.config.js
```

## Дополнительно
Также вижу потребность в разделении backend части на микросервисы для полного выделения микрофронтов и прихода к концепции Backend for Frontend. Для этого структура backend должна быть поделена следующим образом:

```json
 - backend
    - auth-service
        - src
            - controllers
            - models
            - routes
        app.ts
        config.ts
    - profile-service
        - src
            - controllers
            - models
            - routes
        app.ts
        config.ts
    - card-service
        - src
            - controllers
            - models
            - routes
        app.ts
        config.ts
    - common-modules
        - middlewares
        - errors
        - config.ts
```
# Решение задания 2
## Ссылка на решение
[Ссылка на исправленное решение в draw.io по результатам review](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=%D0%9A%D0%B0%D0%B1%D0%B4%D1%83%D0%BB%D0%BB%D0%B8%D0%BD%20%D0%A2%D0%B8%D0%BC%D1%83%D1%80%20-%20%D0%90%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D0%B0%20%D0%BC%D0%B8%D0%BA%D1%80%D0%BE%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%B0%20%D1%81%20%D0%BC%D0%BE%D0%BD%D0%BE%D0%BB%D0%B8%D1%82%D0%B0%20Django%20-%20Sprint%201#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1BUI-H6ef10Qg7Ysz6WMlreMLbQV6dEDc%26export%3Ddownload)