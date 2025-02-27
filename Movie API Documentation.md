# Overview
The Movie API allows users to fetch movie details by title or ID, search movies based on various criteria such as genre, actor, or director names. This API also supports adding movie reviews. 
# Schema
## Types
### Movie
The following are the attributes to represent a movie:
| Field | Type | Description |
|-------|------|-------------|
| id    | ID   | Unique identifier for the movie |
| title | String | Title of the movie |
| genre | String | Genre of the movie |
| director | String | Director of the movie |
| releaseyear | Integer | Release year of the movie |
| rating | Float | Average rating of the movie |
### ReviewResponse
| Field | Type | Description |
|-------|------|-------------|
| success | Boolean | Indicates if the operation was successful |
| message | String | Displays message with operation result details |
# Authentication
The Movie API requires authentication for certain operations. Users must include an API key in the request headers.
## Authentication Method
- API Key: Pass an API key in the Authorization header.
- Example Header:  Authorization: USER_API_KEY
## Authorization Levels
- Public Access: Read-only queries such as getMovieById and searchMovies do not require authentication.
- Authenticated Access: Mutations like addReview require a valid API key.
# Endpoints
## Base URL
https://api.example.com/abc
## Available Endpoints
| Endpoints | Method | Description |
|-----------|--------|-------------|
| /movies/{id} | GET | Fetch movie details by ID |
| /movies/search | GET | Search movies with optional filters
| /reviews | POST | Add a review to a movie |
## Queries
### GET
**getMovieById(id: ID!): Movie**
**Description**: Fetches a movie using a unique identifier. If not found, then returns null.
### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| id | ID | Yes | The unique identifier of the movie. |

**Example Request**
```query {
  getMovieById(id: "12345") {
    title
    genre
    director
    releaseYear
    rating
  }
} 
```
**Example Response**
```{
  "data": {
    "getMovieById": {
      "title": "Inception",
      "genre": "Sci-Fi",
      "director": "Christopher Nolan",
      "releaseYear": 2010,
      "rating": 8.8
    }
  }
}
```

## Search
**searchMovies(genre: String, director: String, actor: String): [Movie]**
**Description**: Searches for movies based on optional filters.

## Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| genre | String | No | Filter based on genre. |
| director | String | No | Filter based on director name. |
| actor | String | No | Filter based on actor name. |

### Example Request
``` query {
  searchMovies(genre: "Action", director: "Quentin Tarantino") {
    id
    title
    releaseYear
  }
}
```
### Example Response
``` {
  "data": {
    "searchMovies": [
      {
        "id": "67890",
        "title": "Kill Bill",
        "releaseYear": 2003
      }
    ]
  }
}
```

# Mutation
**addReview(movieId: ID!, rating: Float!, comment: String): ReviewResponse**
**Description**: Allows user to add a review to a movie.

## Parameter
| Name | Type | Required | Description |
|------|------|----------|-------------|
| movieId | ID | Yes | The movie ID that needs to be reviewed. |
| rating | Float | Yes | The rating provided to the movie. |
| Comment | String | No | A comment about the movie.|

**Example Request**
``` mutation {
  addReview(movieId: "12345", rating: 9.0, comment: "Fantastic movie!") {
    success
    message
  }
```

**Example Response**
```{
  "data": {
    "addReview": {
      "success": true,
      "message": "Review added successfully."
    }
  }
}
```

# Error Handling 
The following are the common GraphQL API error and their meanings:
| Error Code | Message | Description |
|------------|---------|-------------|
| 400 | Bad Request | Invalid input parameter |
| 401 | Unauthorized | Invalid API Key |
| 404 | Movie Not Found | The requested movie ID does not exist. |
| 500 | Internal Server Error Message | Internal server error return |

# Best Practices 
- Use caching for frequently accessed movie data to reduce database load.
- Validate user inputs to prevent incorrect data submissions.
- Implement proper authentication and authorization mechanisms.
- Handle pagination efficiently when retrieving large movie datasets.























