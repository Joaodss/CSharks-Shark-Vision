# CSharks - Sharkvision



### Summary

Welcome to your new favourite Movie service. Sharkvision allows you to search for movies, add them to playlists and even recommends a random movie when you can't decide what to watch. 



### Table Of Contents

1. [**Requirements**](#Project-Requirements)
2. [**SETUP: Cloud Method**](#SETUP-Cloud-Method)
3. [**SETUP: Local Method**](#SETUP-Local-Method)
4. [**Back End Routes**](#Back-End-Routes)
5. [**DTOs**](#DTOs)

### Project Requirements

Your project must meet all of the requirements below:

**Core Functionality**

1. Include a Java/Spring Boot backend and an Angular frontend.
2. You will have to use the [IMDB API](https://imdb-api.com/api) to retrieve some of the information you want to use in the project (you have to create an account to get your API Key)
3. The project will have at least these sections:
   1. A section to search movies (the search should be case insensitive)
   2. A movie detail
   3. Login/Register section (only registered users can create playlists)
   4. User profile page (if logged)
   5. User playlist section (if logged)
4. Playlists with their respective content will be stored in your backend DB. 
5. When searching movies you must make the field case **insensitive** and make it submit when pressing enter as an alternative to pressing the search button.
6. You only can add up to 10 movies per playlist. If you try to add more, a warning message should be displayed.
7. Playlists can be created, updated, or eliminated by the user
8. Users can personalize their account by selecting a profile picture (image url), and writing a bio.
9. Unexpected routes and errors should be appropriately managed.
10. Include adequate and complete documentation of your backend API in the `README.md` file.

**Optional Requirements**

1. Users can search for other users profiles and see their playlists 

2. Users can create public or private playlists (private playlists shouldn't be displayed if searched)

3. Create a section to display the most popular movies (from the API)

   

### SETUP: Cloud Method

**Backend:**

* Use this gateway as normal: [https://sharkvision-db.herokuapp.com](https://sharkvision-db.herokuapp.com/)
* All request must have login authentication.
  * 
  * Admin can access all routes

**Authentication for admin:**

```
login: admin
password: admin
```



### SETUP: Local Method

* Clone the repository

* Select "Trust Project"

  

**Back End Repository**:

https://github.com/EN-IH-WDPT-JUN21/CSharks-BackEndHomework

**Front End Repository**:

https://github.com/EN-IH-WDPT-JUN21/CSharks-SharkVisionFrontEnd



### Back End Routes

| Port | Route Type |                        Route                         |                        Input Required                        |
| :--: | :--------: | :--------------------------------------------------: | :----------------------------------------------------------: |
| 8000 |    POST    |             "/movie-app/users/register"              |                       RegisterUserDTO                        |
| 8000 |    POST    |         "/movie-app/users/validate/username"         |                         UsernameDTO                          |
| 8000 |    POST    |          "/movie-app/users/validate/email"           |                           EmailDTO                           |
| 8000 |    GET     |           "/movie-app/users/authenticated"           |                        Authentication                        |
| 8000 |   PATCH    |           "/movie-app/users/authenticated/           | OPTIONAL<String> Picture, OPTIONAL<String> Bio, OPTIONAL<String> Password |
| 8000 |    POST    |   "/movie-app/users/authenticated/createPlaylist"    |                 Authentication, PlaylistDTO                  |
| 8000 |    POST    |     "/movie-app/users/1/createPlaylistWithMovie"     |             Authentication, PlaylistWithMovieDTO             |
| 8000 |    GET     |                "/movie-app/users/all"                |                                                              |
| 8000 |    GET     |               "/movie-app/users/{id}"                |                         Long userId                          |
| 8000 |   PATCH    |               "/movie-app/users/{id}"                | OPTIONAL<String> Picture, OPTIONAL<String> Bio, OPTIONAL<String> Username, OPTIONAL<String> Password |
| 8000 |    POST    |        "/movie-app/users/{id}/createPlaylist"        |                   Long userId, PlaylistDTO                   |
| 8000 |    GET     |      "/movie-app/playlists/user/authenticated"       |                        Authentication                        |
| 8000 |    GET     |             "/movie-app/playlists/{id}"              |               Authentication, Long playlistId                |
| 8000 |    GET     |            "/movie-app/playlists/visible"            |                        String search                         |
| 8000 |    GET     |          "/movie-app/playlists/{id}/movies"          |               Authentication, Long playlistId                |
| 8000 |   DELETE   |          "/movie-app/playlists/{id}/delete"          |               Authentication, Long playlistId                |
| 8000 |    PUT     |  "/movie-app/playlists/{playlistId}/add/{titleId}"   |                Long playlistId, Long titleId                 |
| 8000 |    PUT     | "/movie-app/playlists/{playlistId}/remove/{titleId}" |                Long playlistId, Long titleId                 |
| 8000 |    GET     |              "/movie-app/playlists/all"              |                                                              |
| 8000 |    GET     |         "/movie-app/playlists/user/{userId}"         |                         Long userId                          |



### DTOs

#### EmailDTO

``` 
{ 
    email: String
} 
```

#### MoviesDTO

``` 
{ 
    titleId: Long,
    name: String,
    visible: boolean,
    playlists: Set<PlaylistsDTO>
} 
```

#### PlaylistsDTO

``` 
{ 
    playlistId: Long,
    user: Users,
    name: String,
    visible: boolean
} 
```

#### PlaylistWithMovieDTO

``` 
{ 
    playlistId: Long,
    user: Users,
    name: String,
    visible: boolean,
    movieId: String
} 
```

#### RegisterUserDTO

``` 
{ 
    username: String,
    emailAddress: String,
    password: String
} 
```

#### UsernameDTO

``` 
{ 
    username: String
} 
```

#### UsersDTO

``` 
{ 
    username: String,
    emailAddress: String,
    password: String,
    pictureUrl: String,
    bio: String,
    playlistId: List<PlaylistDTO>
} 
```
