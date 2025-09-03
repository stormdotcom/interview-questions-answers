# High-Level Design: Social Media Platform

This document outlines a minimal, scalable design for a social media platform suitable for a full-stack developer interview.

---

## 1. Database Design

**Users Table**  
Stores user credentials and timestamps.

```sql
CREATE TABLE Users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

**Posts Table**  
Stores posts authored by users.

```sql
CREATE TABLE Posts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id)
);
```

**Comments Table**  
Stores comments on posts.

```sql
CREATE TABLE Comments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    post_id INT NOT NULL,
    user_id INT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (post_id) REFERENCES Posts(id),
    FOREIGN KEY (user_id) REFERENCES Users(id)
);
```

**Followers Table**  
Manages follow relationships between users.

```sql
CREATE TABLE Followers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    follower_id INT NOT NULL,
    followed_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (follower_id) REFERENCES Users(id),
    FOREIGN KEY (followed_id) REFERENCES Users(id)
);
```

---

## 2. API Design

| Method | Endpoint             | Description                            |
| ------ | -------------------- | -------------------------------------- |
| POST   | /signup              | Register a new user                    |
| POST   | /login               | Authenticate user, return JWT          |
| GET    | /posts               | List all posts (supports pagination)   |
| POST   | /posts               | Create a new post                      |
| GET    | /posts/{id}          | Retrieve a specific post with comments |
| POST   | /comments            | Add a comment to a post                |
| GET    | /user/{id}/followers | List followers of a user               |
| POST   | /follow              | Follow another user                    |

---

## 3. Key Considerations

- **Authentication**  
  Use JWTs for stateless session management; store tokens securely (e.g., HttpOnly cookies or Authorization header).

- **Authorization**  
  Protect endpoints so users can only modify their own posts/comments. Validate JWT scope/claims.

- **Pagination & Filtering**  
  Implement `limit` and `offset` (or cursor-based) for `/posts` and `/comments` to improve performance.

- **Rate Limiting & Throttling**  
  Apply per-user or per-IP rate limits on write endpoints (`/signup`, `/login`, `/posts`, `/comments`) to prevent abuse.

- **Data Consistency & Indexing**  
  Add indexes on `user_id`, `post_id` and relationship tables to support fast lookups and joins.

- **Extensibility**

  - Add likes, media uploads, notifications
  - Move to microservices or CQRS for scale
  - Use message queues for background tasks (e.g., feed generation, notifications)

- **Security**
  - Hash & salt passwords (e.g., bcrypt)
  - Validate and sanitize all user inputs to prevent XSS/SQL injection
  - Use HTTPS and secure headers
