``` mermaid
C4Context
    title System Context diagram для Мессенджера

    Person(user, "Пользователь", "Зарегистрированный пользователь мессенджера")
    Person(guest, "Гость", "Неавторизованный посетитель")

    System_Boundary(messenger, "Мессенджер") {
        System(webApp, "Web Application", "фронт на React/Vue/Angular, шифрование в браузере")
        System(apiBackend, "Backend API", "REST API, управление чатами, авторизация, хранение данных")
        SystemDb(database, "Database", "PostgreSQL/MySQL, хранение пользователей, сообщений, чатов")
    }

    System_Ext(oauth, "Identity Provider (OAuth2.0)", "OAuth2.0")
    System_Ext(email, "Email Service", "Рассылка уведомлений, подтверждение регистрации(later)")

    Rel(guest, webApp, "Регистрируется/входит, не получает доступа к остальным функциям API", "HTTPS")
    Rel(user, webApp, "Отправляет/получает сообщения, управляет профилем, РЕГИСТРАЦИЯ И АВТОРИЗАЦИЯ также обрабатывается формой", "HTTPS/SSE")
    Rel(webApp, oauth, "Редирект для логина, получает токен", "HTTPS/OAuth2")
    Rel(webApp, apiBackend, "Вызов функции РЕГ/auth, запросы к API с access token(связь туда обратно)", "REST, JSON, Bearer token")
    Rel(apiBackend, oauth, "получение токена, вызов функции на обращение к БД")


    Rel(webApp, apiBackend, "Запросы к API", "REST, JSON")
    Rel(apiBackend, database, "Читает/пишет данные", "SQL")
    Rel(apiBackend, email, "Отправляет уведомления (later), о входе или сообщениях", "SMTP")

```


## Comments

Не хватает OAuth провайдера на схеме
