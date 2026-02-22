```mermaid
    flowchart LR

    user["User
    id: uuid/int
    email: string (unique)
    password_hash: string
    avatar:string
    description:string
    created:datetime"]

    chat["Chat
    id: int
    type: enum(direct/group)
    created_at: datetime"]

    chatMembers["Member
    chat_id: uuid/int
    user_id: uuid/int"]

    message["Msg
    id: uuid/int
    chat_id: int
    sender_id: uuid/int
    text_msg(encrypted):text
    created:datetime
    "]
    
    channel["channel
    id: uuid/int
    name: string (unique)
    avatar: str(url)
    description: str
    owner_id: uuid/int
    created:datetime
    "]

    channelSub["Sub
    channel_id: uuid/int
    user_id: uuid/int
    subscribed: datetime
    "]

    channelPosts["Posts
    user_id: uuid/int
    channel_id: uuid/int
    created:datetime
    "]

    user --- chatMembers
    chatMembers --- chat
    chat --- message
    user --- message
    user --- channel
    channel --- channelSub
    user --- channelSub
    channel --- channelPosts
    user --- channelPosts

    ```