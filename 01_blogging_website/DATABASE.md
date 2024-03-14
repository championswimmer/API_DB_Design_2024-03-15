# Database Schema 

## Table: users

| Column Name | Data Type | Constraints                         |
| ----------- | --------- | ----------------------------------- |
| id          | integer   | primary key, autoincrement          |
| created_at  | datetime  |                                     |
| updated_at  | datetime  |                                     |
| username    | string    | lenth: 50, not null, unique         |
| email       | string    | not null, unique                    |
| password    | string    | not null, (encrpyt, not plain text) |
| image       | string    | length: 1024, nullable              |
| bio         | string    | length: 500                         |


## Table: articles

| Column Name | Data Type     | Constraints                |
| ----------- | ------------- | -------------------------- |
| id          | integer       | primary key, autoincrement |
| created_at  | datetime      |                            |
| updated_at  | datetime      |                            |
| title       | string        | length: 100, not null      |
| subtitle    | string        | length: 200, not null      |
| body        | string        | not null                   |
| author_id   | integer       | foreign key(users.id)      |
| tags        | array<string> |                            |

## Table: comments

| Column Name | Data Type | Constraints                |
| ----------- | --------- | -------------------------- |
| id          | integer   | primary key, autoincrement |
| created_at  | datetime  |                            |
| updated_at  | datetime  |                            |
| body        | string    | length: 1000, not null     |
| author_id   | integer   | foreign key(users.id)      |
| article_id  | integer   | foreign key(articles.id)   |

## Database Creation SQL 

### Create Tables 

```sql
--- postgresql 
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(150) NOT NULL UNIQUE,
    password NOT NULL,
    image VARCHAR(1024),
    bio VARCHAR(500)
);

CREATE TABLE IF NOT EXISTS articles (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    title VARCHAR(100) NOT NULL,
    subtitle VARCHAR(200) NOT NULL,
    body TEXT NOT NULL,
    author_id INTEGER REFERENCES users(id),
    tags TEXT[]
);

CREATE INDEX articles_author_id ON articles(author_id);

CREATE TABLE IF NOT EXISTS comments (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    body TEXT NOT NULL,
    author_id INTEGER REFERENCES users(id),
    article_id INTEGER REFERENCES articles(id)
);

CREATE INDEX comments_author_id ON comments(author_id);
CREATE INDEX comments_article_id ON comments(article_id);
```
