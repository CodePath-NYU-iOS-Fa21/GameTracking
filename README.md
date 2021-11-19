Unit 8 - Group Milestone

# GAMELOG

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)

## Overview
### Description
Tracks the gaming activity of an individual across multiple platforms and also provides info about games. Could also be used to find other gamers and make friends.

### App Evaluation
- **Category:** Gaming / Social Networking
- **Mobile:** This app would be primarily developed for mobile but would perhaps be just as viable on a computer, such as tinder or other similar apps. Functionality wouldn't be limited to mobile devices, however mobile version could potentially have more features.
- **Story:** Analyzes users gaming activity and provides information to users about game difficulty, progress, etc. The user can also view other gamers' activity, follow them, comment on their activity and connect with them.
- **Market:** Any individual could choose to use this app, and to keep it a safe environment, people would be organized into age groups.
- **Habit:** This app could be used as often as the user wanted depending on how much they game and what exactly they're specifically using the app for.
- **Scope:** We would initially build a database of user gaming history and also allows users to learn more about games they're interested in. Then, once we get enough users, the social aspects of this app would become more prominent - users could follow other users, comment on their posts and make friends with them.  

## Product Spec
### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* User logs in to access gameplay history and lookup game information. 
* User populates their profile pages and indicates whatever games/platforms they're interested in.
* User can follow other users and view their activity
* Settings (Accesibility, Notification, General, etc.)

**Optional Nice-to-have Stories**

* Discover page to see trending games
* Chat client to allow users to communicate with each other
* Share functionality 

### 2. Screen Archetypes

* Login 
* Register - User signs up or logs into their account
   * Upon Download/Reopening of the application, the user is prompted to log in to gain access to their profile information to be properly matched with another person. 
   * ...
* Profile Screen 
   * Allows user to upload a photo or select an avatar and fill in their interests
* Feed Screen.
   * Feed populated by gaming activity of users that the current user is following.
* Game details screen
  * Display user's history with the game and provide information about game difficulty.
* Settings Screen
   * Lets people change language, and app notification settings.

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Feed
* Profile
* Search

Optional:
* Discover Screen
* Chat Screen

**Flow Navigation** (Screen to Screen)
* Forced Log-in -> Account creation if no log in is available
* Feed -> Other user profile or write comments
* Profile -> Fields that can be modified
* Search -> Other user profile or Game Detail 
* Settings -> Toggle settings

## Wireframes
<img src="https://github.com/CodePath-NYU-iOS-Fa21/GameTracking/blob/main/gamelog.jpg?raw=true" width=800><br>


# Game Log Schema
    

## Schema 
### Models

#### User

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | uuid for the user (default field) |
   | email         | String   | login email for the user |
   | password      | String   | hashed password for the user |
   | userId        | String   | unique user handle for the user |
   | userName      | String   | display name for the user |
   | profileImage  | File     | profile image for the user |
   | bannerImage*  | File     | banner image for the user |
   | platformInfo  | List     | list of platform info for the user |
   | createdAt     | DateTime | date when user is created (default field) |
   | updatedAt     | DateTime | date when user is last updated (default field) |
   |gameIDs | Array [String] | collection of games that the user has played | 

#### Post

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user post (default field) |
   | author        | Pointer to User| post author |
   | game          | Pointer to Game| The game this post is about |
   | image         | File     | image that user posts |
   | caption       | String   | image caption by author |
   |comments       | Array [String] | array containing comments for post 
   | commentsCount | Number   | number of comments that has been posted to an image |
   | likesCount    | Number   | number of likes for the post |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |

#### Game

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the game |
   | studio        | String   | Studio name for the game |
   | platforms     | Array [String] | platforms that the game is available on |
   | genre         | String   | genre catalog for the game |
   | age rating | String | age rating for game |
   | image     | File     | poster image for the game |
   | description       | String   | short description of game |
   | releaseDate     | DateTime | date when game was released |
   


### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all posts where user is author or any of the user's following are authors
      - (Create/POST) Create a new like on a post
      - (Delete) Delete existing like

   - Post Detail Screen
      - (Create/POST) Create a new comment on a post
      - (Delete) Delete existing comment
      - (Create/POST) Create a new like on a post
      - (Delete) Delete existing like 
   - Create Post Screen
      - (Create/POST) Create a new post object
      - (Update/PUT) User's game library/history
   - Settings Screen
      - (Read/GET) Query logged in user object
      - (Update/PUT) Update user profile image or other settings
   - User Profile Screen
      - (Read/GET) Query a user object (including logged in usert)
      - (Update/PUT) Follow/unfollow a user
   - Search screen
       - (Read/GET) Query a game object
       - (Read/GET) Query a user object
   - Game Detail screen
       - (Read/GET) Query info about a game 
#### [OPTIONAL:] Existing API Endpoints
##### Video Game Database API

- IGDB - [https://api-docs.igdb.com/#endpoints]

- Games - [https://api.igdb.com/v4/games]

##### Video Game Info API

- Howlongtobeat: https://pypi.org/project/howlongtobeatpy/
