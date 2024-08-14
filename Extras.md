Yes, the FIFA Performance Analyzer project involves several APIs. Here’s a summary of the APIs used in the project, including their functionality, endpoints, and request/response formats:

### 1. **User Registration API**

**Endpoint:** `/api/auth/register`  
**Method:** `POST`  
**Description:** Registers a new user with a username and password.

**Request:**
- **Headers:** None
- **Body (JSON):**
  ```json
  {
    "username": "player1",
    "password": "securePassword123"
  }
  ```

**Response:**
- **Status Code:** 201 (Created)
- **Body (JSON):**
  ```json
  {
    "message": "User registered successfully"
  }
  ```

### 2. **User Login API**

**Endpoint:** `/api/auth/login`  
**Method:** `POST`  
**Description:** Logs in a user and returns a JWT token for authentication.

**Request:**
- **Headers:** None
- **Body (JSON):**
  ```json
  {
    "username": "player1",
    "password": "securePassword123"
  }
  ```

**Response:**
- **Status Code:** 200 (OK)
- **Body (JSON):**
  ```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InBsYXllciIsImlhdCI6MTYwNTgxNjA5MywiZXhwIjoxNjA1ODIxNjMwfQ.K4qPvLsjG8lUwU4O7S8FzA2Q_4-f0s5GsoT4LhmPTxA"
  }
  ```

### 3. **Save Game Data API**

**Endpoint:** `/api/games/save`  
**Method:** `POST`  
**Description:** Saves game data for a specific game ID. Requires authentication.

**Request:**
- **Headers:**
  - `Authorization: Bearer <your_jwt_token>`
- **Body (JSON):**
  ```json
  {
    "gameId": "game123",
    "gameData": {
      "goals": 3,
      "assists": 2,
      "possession": 55.5
    }
  }
  ```

**Response:**
- **Status Code:** 200 (OK)
- **Body (JSON):**
  ```json
  {
    "message": "Game data saved successfully"
  }
  ```

### 4. **Analyze Game Performance API**

**Endpoint:** `/api/analysis/performance/:gameId`  
**Method:** `GET`  
**Description:** Retrieves performance analysis for a specific game ID. Requires authentication.

**Request:**
- **Headers:**
  - `Authorization: Bearer <your_jwt_token>`
- **Params:**
  - `gameId`: The ID of the game to analyze.

**Response:**
- **Status Code:** 200 (OK)
- **Body (JSON):**
  ```json
  {
    "goals": 3,
    "assists": 2,
    "possession": 55.5
  }
  ```

### Summary of APIs Used

- **User Registration API**: Creates a new user in the system.
- **User Login API**: Authenticates the user and issues a JWT token.
- **Save Game Data API**: Stores game performance data in the database.
- **Analyze Game Performance API**: Retrieves and displays performance metrics for a given game.

These APIs cover the core functionalities of registering users, logging in, saving game data, and analyzing performance. For each API, ensure that error handling and input validation are implemented to handle various scenarios and edge cases in a real-world application.
