1. Feature: User registration

Scenario(success): Successful registration
Given user provides valid email and password
When user submits registration form
Then system creates a new account
And user becomes authenticated

Scenario(fail): Registration with already used email
Given user provides an email that is already registered and a valid password
When user submits registration form
Then system does not create a new account
And user sees an error message


2. Feature: User authentication

Scenario(success): Successful login
Given a registered user exists
And the user provides valid login and password
When the user submits a login request
Then the system authenticates the user
And user becomes authenticated

Scenario(fail): Login with invalid login+password
Given a registered user exists
And the user provides incorrect login or password
When the user submits a login request
Then the system does not authenticate the user
And user sees an error message

3. Scenario: Unauthorized user cannot access chat
Given user is not authenticated
When user tries to open chats page
Then system denies access
And user is redirected to the login page

4. Scenario: User starts a new chat
Given auth user finds another user
When user clicks the "new chat" and searches by nickname
Then a new chat is created with an existing user
And the user is redirected to the new chat

5. Scenario: Auth user sends a message
Given auth user has an existing chat with another user
When user types a message
Then the system submits the message
And the recipient can see the message

6. Scenario: User requests messages
Given user enters in chat with another user
When user calls GET
Then system returns paginated messages

7. Scenario: User views own profile
Given auth user
When user opens the profile page
Then user sees their username, email and avatar

Scenario: User updates own profile
Given auth user on the own profile page
When user changes their profile information + user saves the changes
Then system updates the user profile
And user sees updated profile information

8. Scenario: User creates a new group chat
Given auth user try to create a group chat with another users
When user clicks the "new group" and searches members by nickname
Then system creates the group chat
And all deleted users are added to the private group

9. Scenario: User subscribes to a channel
Given auth users looking for a public channel
When user subscribes to the channel
Then system adds user to channel subscribers
And user starts receiving channel messages

10. Scenario: User views profile
Given auth user has a chat with another user
When user opens the profile page
Then user sees another users information(nickname, avatar, description)

11. Scenario: User views group chat members
Given auth user is a member of a group chat
When user opens group chat information
Then user sees the list of group members
And user sees the total number of members

12. Scenario: User views channels info
Given auth user subscribed to the public channel
When user opens the channel info
Then user sees channel information(link, avatar, description)

13. Scenario: encrypted message
Given user sends a message to another user/group chat
When user types message script encrypted it before sending
Then system stores encrypted message and sends to another user
And message decrypt in the browser