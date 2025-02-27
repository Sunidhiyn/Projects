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
