```mermaid
    flowchart LR

    user["User
    id: uuid v7
    nickname: str
    email: string (unique)
    description:string
    created: datetime
    "]

    message["Msg
    id: uuid v7
    sender_id: uuid v7
    receiver_id: uuid v7
    text_msg(encrypted): text
    created: datetime
    "]

    user --- message
```


## Comments

* Если у нас больше 1 чата между двумя юзерами, то сущность чатов оправдана. Если нет, то наверное можно просто чат_Id завести как поле, или и вовсе убрать, а смотреть как-то иначе.
* Имхо для MVP многовато сущностей. Каналы пока перебор. Стоит начать только с пользователей и 1to1 сообщений.
