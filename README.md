
---

## Score API

### Description

A Kotlin Spring Boot API backend to record highscores. It allows users to sign up, log in with JWT, record their game scores, view leaderboards, and manage privacy settings.

### Requirements

- **JDK 21**
- **Gradle 8.x** (included with the project)


---
### Dependncy

- **Spring Boot 3.3.3**
- **Kotlin**
- **Spring Security (JWT)**
- **H2 Database (Embedded)**
- **Gradle**
- **Spring Data JPA**
- **Springdoc OpenAPI (Swagger UI)**

---

### How to Build and Run the Application

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/Score.git
   cd Score
   ```

2. **Build the project**:
   ```bash
   ./gradlew build
   ```

3. **Run the application**:
   ```bash
   ./gradlew bootRun
   ```

   The application will start at `http://localhost:8080`.

---

### API Routes

#### 1. **Auth and User Management**

- **POST /api/auth/signup**  
  _Registers a new user._  
  **Request**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```

- **POST /api/auth/login**  
  _Authenticates user and returns a JWT token._  
  **Request**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```

- **PUT /api/user/password**  
  _Allows the logged-in user to change their password._  
  **Request**:
  ```json
  {
    "old_password": "string",
    "new_password": "string"
  }
  ```

---

#### 2. **Score Recording and Scoreboard**

- **POST /api/score/record**  
  _Records the score for a user._  
  **Request**:
  ```json
  {
    "player_id": "UUID",
    "user_name": "string",
    "start_time": "ISO-8601 format",
    "end_time": "ISO-8601 format",
    "score": "int"
  }
  ```

- **GET /api/scoreboard**  
  _Fetches the public scoreboard with pagination._  
  **Request Parameters**:
  - `page`: Page number (default = 0)
  - `size`: Page size (default = 10)

  **Response**:
  ```json
  {
    "content": [
      {
        "player_id": "UUID",
        "user_name": "string",
        "score": "int"
      }
    ],
    "total_pages": "int",
    "total_elements": "int",
    "current_page": "int"
  }
  ```

- **GET /api/leaderboard**  
  _Fetches the global leaderboard with pagination._  
  **Request Parameters**:
  - `page`: Page number (default = 0)
  - `size`: Page size (default = 10)

  **Response**:
  ```json
  {
    "content": [
      {
        "user_name": "string",
        "score": "int"
      }
    ],
    "total_pages": "int",
    "total_elements": "int",
    "current_page": "int"
  }
  ```

- **PUT /api/scoreboard/privacy**  
  _Sets the user's scoreboard privacy to public or private._  
  **Request**:
  ```json
  {
    "is_private": "true/false"
  }
  ```

---

#### 3. **Game Download**

- **GET /api/game/download**  
  _Provides a page or link to download the game._

---

### Running Tests

To run tests for the application:

```bash
./gradlew test
```

---
