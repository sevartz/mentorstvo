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

    System_Ext(email, "Email Service", "Рассылка уведомлений, подтверждение регистрации(later)")

    Rel(guest, webApp, "Регистрируется/входит, не получает доступа к остальным функциям API", "HTTPS")
    Rel(user, webApp, "Отправляет/получает сообщения, управляет профилем", "HTTPS/SSE")

    Rel(webApp, apiBackend, "Запросы к API", "REST, JSON")
    Rel(apiBackend, database, "Читает/пишет данные", "SQL")
    Rel(apiBackend, email, "Отправляет уведомления (later)", "SMTP")

```
