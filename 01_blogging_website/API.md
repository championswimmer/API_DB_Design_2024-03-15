# API 

BaseURL: `https://api.blog.site/api/v1`

## Responses 

### Success 

```json
{
    "status": "success",
    "code": 200, 
    "message": "Success",
    "data": {},
    "meta": {
        "page": 1,
        "total_pages": 1,
        "per_page": 10,
        "total": 0
    }
}
```

### Error 

```json
{
    "status": "error",
    "code": 400, 
    "message": "Bad Request",
    "data": {},
    "meta": {}
}
```

## Endpoints 

### Users

#### `POST /users/` - Signup / Create User 

#### `POST /users/login` - Login User

#### `GET /users/{username}` - Get User Profile

#### `PUT /users/{username}/follow` 🔐 - Follow User

#### `DELETE /users/{username}/follow` 🔐 - Unfollow User

### Articles

#### `GET /articles/` - Get All Articles

#### `GET /articles/{slug}` - Get Single Article

#### `POST /articles/` 🔐 - Create Article

#### `PATCH /articles/{slug}` 🔐 - Update Article

#### `DELETE /articles/{slug}` 🔐 - Delete Article

#### `PUT /articles/{slug}/like` 🔐 - Favourite Article

#### `DELETE /articles/{slug}/like` 🔐 - Unfavourite Article


### Comments 

#### `GET /articles/{slug}/comments` - Get All Comments of an Article

#### `POST /articles/{slug}/comments` 🔐 - Create Comment

#### `DELETE /articles/{slug}/comments/{id}` 🔐 - Delete Comment

