## Overview

Xcode is a competitive coding platform designed for real-time 1-to-1 battle royale-style coding challenges. It provides a robust user management system that includes authentication, profile management, social interactions, and security features like two-factor authentication (2FA).

The platform supports:

- **1-to-1 Global Challenges**: Random matchmaking where the first to complete all questions wins.
- **Friendly Challenges**: Multiple problems, time-bound, for casual competitions.
- **Code Execution Engine**: Backend optimized for scalability using Go (Golang) with microservices.
- **Frontend**: Built with React and ShadCN for a seamless user experience.
- **User Features**: Profile customization, language preferences, following/followers system, and login activity tracking.
- **Security**: Email & OAuth authentication, password management, and optional 2FA.
---

## Authentication Endpoints

### 1. Register User

**Endpoint:** `POST /api/v1/auth/register` **Description:** Registers a new user with the platform.

**Request Body:**

```json
{
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "role": "string",
    "primaryLanguageID": "string",
    "secondaryLanguageID": ["string"],
    "email": "string",
    "authType": "string",
    "password": "string",
    "confirmPassword": "string",
    "muteNotifications": boolean,
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
    }
}
```

**Response:** **Status Code:** `201 Created`

```json
{
    "userID": "string",
    "message": "User registered successfully"
}
```

---

### 2. Login User

**Endpoint:** `POST /api/v1/auth/login` **Description:** Authenticates the user and returns a session token.

**Request Body:**

```json
{
    "email": "string",
    "password": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "refreshToken": "string",
    "expiresIn": "integer",
    "userID": "string"
}
```

---
### 3. Token Refresh

**Endpoint:** `GET /api/v1/auth/refresh` **Description:** Authenticates the user and returns a session token.

**Response:** **Status Code:** `200 OK`

```json
{
    "accessToken": "string",
    "expiresIn": "integer",
    "userID": "string"
}
```

---
### 3. Logout

**Endpoint:** `GET /api/v1/auth/logout` **Description:** Log Out the user and revoke the tokens.

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "User Logged Out,Refresh Token and Access Token Revoked",
}
```

---
### 4. Resend OTP

**Endpoint:** `GET /api/v1/auth/resendotp` **Description:** Resend the OTP after expiry
**Response:** **Status Code:** `200 OK`

```json
{
    "message": "OTP sent successfully",
}
```

---

### 5. Google Authentication

**Endpoint:** `GET /api/v1/auth/google` **Description:** Initiates Google authentication.

**Response:** **Status Code:** `302 Found` Redirects to Google OAuth login.

---

### 6. Google Authentication Callback

**Endpoint:** `GET /api/v1/auth/google/callback` **Description:** Handles the response from Google authentication.

**Response:** **Status Code:** `200 OK`

```json
{
    "token": "string",
    "userID": "string"
}
```

---

### 7. Verify User

**Endpoint:** `PATCH /api/v1/auth/verify` **Description:** Verifies the user's email.

**Path Variables:**

- `token` (string) - a secret token shared to the user for verification.
- `email` (string) 

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "User verified successfully"
}
```

---

### 8. Set Two-Factor Authentication (2FA)

**Endpoint:** `PATCH /api/v1/auth/set2fa` **Description:** Enables or disables 2FA for the user.

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "2FA status updated"
}
```

---

### 9. Forgot Password

**Endpoint:** `POST /api/v1/auth/forgotpassword` **Description:** Initiates the password reset process.

**Path Variables:**

- `email` (string) 

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "Password reset link sent"
}
```

---

### 10. Password Reset Callback

**Endpoint:** `GET /api/v1/auth/forgotpassword/callback` **Description:** Handles the password reset confirmation.

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "Password reset successful"
}
```

---

### 11. Change Password

**Endpoint:** `PATCH /api/v1/auth/changepassword` **Description:** Allows the user to change their password.

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "Password changed successfully"
}
```

---

## User Profile Management

### 12. Update Profile

**Endpoint:** `PATCH /api/v1/user/update` **Description:** Updates user profile information.

**Request Body:**

```json
{
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "primaryLanguageID": "string",
    "secondaryLanguageID": ["string"],
    "muteNotifications": boolean,
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
    }
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "Profile updated successfully"
}
```

---
### 13. Update Profile Image

**Endpoint:** `PATCH /api/v1/user/uploadAvatar` **Description:** Updates user profile image.

**Request Body:**

```json
{ "avatarData": "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD..." }
```

**Response:** **Status Code:** `200 OK`

```json
{
  "message": "Profile picture updated successfully",
  "avatarData": "https://cdn.example.com/users/avatars/uniqueFilename.jpg"
}

```

---

### 14. Get User Profile

**Endpoint:** `GET /api/v1/user/profile` **Description:** Retrieves the user's profile information.

**Response:** **Status Code:** `200 OK`

```json
{
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "email": "string",
    "role": "string",
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
    }
}
```

---

## Social Features

### 15. Follow a User

**Endpoint:** `POST /api/v1/user/follow` **Description:** Follows a user.

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "User followed successfully"
}
```

---

### 16. Unfollow a User

**Endpoint:** `POST /api/v1/user/unfollow` **Description:** Unfollows a user.

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "User unfollowed successfully"
}
```

---
### 17. Following

**Endpoint:** `GET /api/v1/user/following` **Description:** Retreive all followings

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "User following fetched successfully",
    "data":[
    {
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "email": "string",
    "role": "string",
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
        }
     },
      {
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "email": "string",
    "role": "string",
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
        }
     }
    ]
}
```

---
### 18. Followers

**Endpoint:** `GET /api/v1/user/followers` **Description:** Retreive all followers

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "User followers fetched successfully",
    "data":[
    {
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "email": "string",
    "role": "string",
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
        }
     },
      {
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "email": "string",
    "role": "string",
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
        }
     }
    ]
}
```

---
## Admin User Management

### 19. Get All Users

**Endpoint:** `GET /api/v1/admin/user/all`  
**Description:** Retrieves a list of all registered users.

**Response:**  
**Status Code:** `200 OK`

```json
{
    "users": [
        {
            "userID": "string",
            "firstName": "string",
            "lastName": "string",
            "email": "string",
            "role": "string",
            "status": "string"
        }
    ]
}
```

---

### 20. Block User

**Endpoint:** `PATCH /api/v1/admin/user/block`  
**Description:** Blocks a user account.

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "User blocked successfully"
}
```

---

### 21. Unblock User

**Endpoint:** `PATCH /api/v1/admin/user/unblock`  
**Description:** Unblocks a previously blocked user account.

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "User unblocked successfully"
}
```

---

### 22. Verify User

**Endpoint:** `PATCH /api/v1/admin/user/verify`  
**Description:** Verifies a user account.

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "User verified successfully"
}
```

---

### 23. Unverify User

**Endpoint:** `PATCH /api/v1/admin/user/unverify`  
**Description:** Removes verification status from a user account.

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "User unverified successfully"
}
```

---

### 24. Create User

**Endpoint:** `POST /api/v1/admin/user/create`  
**Description:** Creates a new user account.

**Request Body:**

```json
{
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "role": "string",
    "primaryLanguageID": "string",
    "secondaryLanguageID": ["string"],
    "email": "string",
    "authType": "string",
    "password": "string",
    "confirmPassword": "string",
    "muteNotifications": boolean,
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
    }
}
```

**Response:**  
**Status Code:** `201 Created`

```json
{
    "userID": "string",
    "message": "User created successfully"
}
```

---

### 25. Update User

**Endpoint:** `PUT /api/v1/admin/user/update`  
**Description:** Updates user account information.

**Request Body:**

```json
{
    "userID": "string",
    "firstName": "string",
    "lastName": "string",
    "country": "string",
    "role": "string",
    "email":"string",
    "password":"string",
    "primaryLanguageID": "string",
    "secondaryLanguageID": ["string"],
    "muteNotifications": boolean,
    "socials": {
        "github": "string",
        "twitter": "string",
        "linkedin": "string"
    }
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "User updated successfully"
}
```

---

### 26. Soft Delete User

**Endpoint:** `DELETE /api/v1/admin/user/delete`  
**Description:** Marks a user account as deleted without permanently removing it.

**Request Body:**

```json
{
    "userID": "string"
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "User deleted successfully"
}
```

---

## Wallet Management

### 27. Get Wallet Balance

**Endpoint:** `GET /api/v1/user/wallet/balance`  
**Description:** Retrieves the current balance of the user's wallet.

**Response:**  
**Status Code:** `200 OK`

```json
{
    "walletID": "string",
    "balance": "float",
    "currency": "string"
}
```

---

### 28. Get Wallet Transaction History

**Endpoint:** `GET /api/v1/user/wallet/history`  
**Description:** Fetches the transaction history of the user's wallet.

**Response:**  
**Status Code:** `200 OK`

```json
{
    "transactions": [
        {
            "transactionID": "string",
            "amount": "float",
            "type": "string",
            "status": "string",
            "timestamp": "string"
        }
    ]
}
```

---

### 29. Refill Wallet

**Endpoint:** `POST /api/v1/user/wallet/refill`  
**Description:** Allows the user to add funds to their wallet.

**Request Body:**

```json
{
    "amount": "float",
    "currency": "string",
    "paymentMethod": "string"
}
```

**Response:**  
**Status Code:** `201 Created`

```json
{
    "transactionID": "string",
    "message": "Wallet refilled successfully"
}
```

---

## Payment Processing

### 30. Initiate Payment

**Endpoint:** `GET /api/v1/user/payment`  
**Description:** Initiates a payment request.

**Response:**  
**Status Code:** `200 OK`

```json
{
    "paymentID": "string",
    "amount": "float",
    "status": "string",
    "redirectURL": "string"
}
```

---

### 31. Payment Callback

**Endpoint:** `POST /api/v1/user/payment/callback`  
**Description:** Handles the callback response from the payment gateway.

**Request Body:**

```json
{
    "paymentID": "string",
    "status": "string",
    "transactionID": "string"
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "Payment processed successfully"
}
```

---
## Problems and Submissions

### 32. Get All Problems

**Endpoint:** `GET /api/v1/problems/all` **Description:** Fetches a list of all available problems.

**Response:** **Status Code:** `200 OK`

```json
{
    "problems": [
        {
            "problemId": "string",
            "title": "string",
            "difficulty": "string",
            "tags": ["string"]
        }
    ]
}
```

---

### 33. Get Problem by ID

**Endpoint:** `GET /api/v1/problems/{problemId}` **Description:** Retrieves detailed information about a specific problem.

**Path Variables:**

- `problemId` (string) - The ID of the problem.

**Response:** **Status Code:** `200 OK`

```json
{
    "problemId": "string",
    "title": "string",
    "description": "string",
    "difficulty": "string",
    "tags": ["string"],
    "testCases": [
        {
            "input": "string",
            "output": "string"
        }
    ]
}
```

---

### 34. Run Problem

**Endpoint:** `POST /api/v1/problems/run/{problemId}` **Description:** Runs a problem against test cases without submitting.

**Path Variables:**

- `problemId` (string) - The ID of the problem.

**Request Body:**

```json
{
    "code": "string",
    "language": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "executionTime": "string",
    "output": "string",
    "error": "string"
}
```

---

### 35. Submit Problem

**Endpoint:** `POST /api/v1/problems/submit/{problemId}` **Description:** Submits a solution for evaluation.

**Path Variables:**

- `problemId` (string) - The ID of the problem.

**Request Body:**

```json
{
    "code": "string",
    "language": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "submissionId": "string",
    "status": "string",
    "score": "integer"
}
```

---

### 36. Get Suggested Problems

**Endpoint:** `GET /api/v1/problems/suggest` **Description:** Fetches problem recommendations based on user history.

**Response:** **Status Code:** `200 OK`

```json
{
    "suggestedProblems": [
        {
            "problemId": "string",
            "title": "string",
            "difficulty": "string"
        }
    ]
}
```

---

### 37. Get All Playlists

**Endpoint:** `GET /api/v1/problems/playlists/all` **Description:** Retrieves all available problem playlists.

**Response:** **Status Code:** `200 OK`

```json
{
    "playlists": [
        {
            "playlistID": "string",
            "title": "string",
            "problemCount": "integer"
        }
    ]
}
```

---

### 38. Get Problems in a Playlist

**Endpoint:** `GET /api/v1/problems/playlists/{playlistID}` **Description:** Fetches all problems in a given playlist.

**Path Variables:**

- `playlistID` (string) - The ID of the playlist.

**Response:** **Status Code:** `200 OK`

```json
{
    "problems": [
        {
            "problemId": "string",
            "title": "string",
            "difficulty": "string"
        }
    ]
}
```

---

### 39 Get Problem Submissions

**Endpoint:** `GET /api/v1/problems/submissions/{problemID}` **Description:** Retrieves all submissions for a given problem.

**Path Variables:**

- `problemID` (string) - The ID of the submitted problem.

**Response:** **Status Code:** `200 OK`

```json
{
    "submissions": [
        {
            "submissionId": "string",
            "status": "string",
            "score": "integer"
        }
    ]
}
```

---

### 40. Get Attempted Problems

**Endpoint:** `GET /api/v1/problems/attempted` **Description:** Retrieves a list of problems attempted by the user.

**Response:** **Status Code:** `200 OK`

```json
{
    "attemptedProblems": [
        {
            "problemId": "string",
            "title": "string"
        }
    ]
}
```

---

### 41. Get Solved Problems with Answer

**Endpoint:** `GET /api/v1/problems/solved` **Description:** Fetches solved problems along with submitted answers.

**Response:** **Status Code:** `200 OK`

```json
{
    "solvedProblems": [
        {
            "problemId": "string",
            "title": "string",
            "userSolution": "string"
        }
    ]
}
```

---

### 42. Get Problem Insights

**Endpoint:** `GET /api/v1/problems/insights/all` **Description:** Retrieves insights for different problems.

**Path Variables:**

- `problemID` (string) - The ID of the submitted problem.

**Response:** **Status Code:** `200 OK`

```json
{
    "insights": [
        {
            "insightID": "string",
            "content": "string"
        }
    ]
}
```

---

### 43. Add Problem Insight

**Endpoint:** `POST /api/v1/problems/insights` **Description:** Adds a new insight to a problem.

**Request Body:**

```json
{
    "problemId": "string",
    "content": "string"
}
```

**Response:** **Status Code:** `201 Created`

```json
{
    "insightID": "string",
    "message": "Insight added successfully"
}
```

---

### 44. Delete Insight

**Endpoint:** `DELETE /api/v1/problems/delete/{insightID}` **Description:** Deletes a specific problem insight.

**Path Variables:**

- `insightID` (string) - The ID of the insight to be deleted.

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "Insight deleted successfully"
}
```

---

### 45. Get AI Feedback

**Endpoint:** `GET /api/v1/problems/aifeedback` **Description:** Provides AI-generated feedback on problem solutions.

**Request Body:**

```json
{
    "problemId": "string",
    "code": "string"
}
```

**Response:** **Status Code:** `200 OK`

```json
{
    "feedback": "string"
}
```

---


### 46. Create Playlist

**Endpoint:** `POST /api/v1/admin/programs/playlist`  
**Description:** Creates a new problem playlist.

**Request Body:**

```json
{
    "name": "string",
    "description": "string"
}
```

**Response:**  
**Status Code:** `201 Created`

```json
{
    "playlistID": "string",
    "message": "Playlist created successfully"
}
```

---

### 47. Add Problem to Playlist

**Endpoint:** `POST /api/v1/admin/problems/playlists/:playlistID/:problemID`  
**Description:** Adds a specific problem to a playlist.

**Path Variables:**

- `playlistID`: ID of the playlist
- `problemID`: ID of the problem

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "Problem added to playlist successfully"
}
```

---

### 48. Update Problems in Playlist

**Endpoint:** `PATCH /api/v1/admin/problems/playlists/:playlistID`  
**Description:** Updates the list of problems within a playlist.

**Path Variables:**

- `playlistID`: ID of the playlist

**Request Body:**

```json
{
    "problems": ["problemID1", "problemID2", "problemID3"]
}
```

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "Playlist updated successfully"
}
```

---

### 49. Remove Problem from Playlist

**Endpoint:** `DELETE /api/v1/admin/problems/playlists/:playlistID/:problemID`  
**Description:** Removes a specific problem from a playlist.

**Path Variables:**

- `playlistID`: ID of the playlist
- `problemID`: ID of the problem

**Response:**  
**Status Code:** `200 OK`

```json
{
    "message": "Problem removed from playlist successfully"
}
```

---

### 50. Add Problem and Test Cases

**Endpoint:** `POST /api/v1/admin/problems`  
**Description:** Adds a new coding problem along with test cases.

**Request Body:**

```json
{
    "title": "string",
    "description": "string",
    "difficulty": "string",
    "tags": ["string"],
    "testCases": [
        {
            "input": "string",
            "expectedOutput": "string"
        }
    ]
}
```

**Response:**  
**Status Code:** `201 Created`

```json
{
    "problemID": "string",
    "message": "Problem added successfully"
}
```

---

### 51. Validate New Problem

**Endpoint:** `GET /api/v1/admin/problems/validate`  
**Description:** Validates a newly added problem before submission.

**Query Parameters:**

- `problemID`: ID of the problem to validate

**Response:**  
**Status Code:** `200 OK`

```json
{
    "valid": true,
    "message": "Problem validation successful"
}
```

# Compiler Management

### 52. Run Code

**Endpoint:** `GET /api/v1/compiler/run` **Description:** Runs the provided code and returns the output.

**Query Parameters:**

- `language` (string) - The programming language used.
- `code` (string) - The source code to be executed.

**Response:** **Status Code:** `200 OK`

```json
{
    "output": "string",
    "executionTime": "integer",
    "memoryUsage": "integer"
}
```

---

### 53. Save Code

**Endpoint:** `POST /api/v1/user/compiler/save` **Description:** Saves the user's code snippet.

**Request Body:**

```json
{
    "title": "string",
    "language": "string",
    "code": "string"
}
```

**Response:** **Status Code:** `201 Created`

```json
{
    "message": "Code saved successfully",
    "codeID": "string"
}
```

---

### 54. Retrieve Saved Code

**Endpoint:** `GET /api/v1/user/compiler/saved/all` **Description:** Retrieves all saved code snippets of the user.

**Response:** **Status Code:** `200 OK`

```json
[
    {
        "codeID": "string",
        "title": "string",
        "language": "string"
    }
]
```

---

### 55. Retrieve Code By ID

**Endpoint:** `GET /api/v1/user/compiler/saved/:codeID` **Path Variables:**

- `codeID` (string) - The unique identifier of the saved code.

**Response:** **Status Code:** `200 OK`

```json
{
    "codeID": "string",
    "title": "string",
    "language": "string",
    "code": "string"
}
```

---

### 56. Delete Saved Code

**Endpoint:** `DELETE /api/v1/user/compiler/delete/:codeID` **Path Variables:**

- `codeID` (string) - The unique identifier of the saved code.

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "Code deleted successfully"
}
```

---

# Chat Management

### 57. Retrieve All Chats Metadata

**Endpoint:** `GET /api/v1/users/chats/metadata` **Description:** Retrieves metadata for all chat conversations of the user.

**Response:** **Status Code:** `200 OK`

```json
[
    {
        "userID": "string",
        "lastMessage": "string",
        "timestamp": "string"
    }
]
```

---
### 58. Send Message

**Endpoint:** `POST /api/v1/users/chats/send` **Description:** Send message to your friend.

**Response:** **Status Code:** `200 OK`

```json
[
    {
        "friendID": "string",
        "content": "string",
        "timestamp": "string"
    }
]
```

---
### 59. Retrieve Chat Content

**Endpoint:** `GET /api/v1/users/chats/:friendID` **Path Variables:**

- `friendID` (string) - The ID of the friend whose chat content is retrieved.

**Response:** **Status Code:** `200 OK`

```json
[
    {
        "sender": "string",
        "message": "string",
        "timestamp": "string"
    }
]
```

---

# Game Management

### 60. Create Challenge

**Endpoint:** `POST /api/v1/users/battle/challenge/:friendID` **Path Variables:**

- `friendID` (string) - The ID of the friend to challenge.

**Response:** **Status Code:** `201 Created`

```json
{
    "challengeID": "string",
    "message": "Challenge created successfully"
}
```

---
### 61. Accept Challenge

**Endpoint:** `POST /api/v1/users/battle/challenge/accept/:challengeID` **Path Variables:**

- `challengeID` (string) - The ID of the challenge.

**Response:** **Status Code:** `201 Created`

```json
{
    "challengeID": "string",
    "message": "Challenge started successfully"
}
```

---

### 62. Retrieve All Challenges

**Endpoint:** `GET /api/v1/users/battle/challenge/all` **Description:** Retrieves all active challenges for the user.

**Response:** **Status Code:** `200 OK`

```json
[
    {
        "challengeID": "string",
        "opponent": "string",
        "status": "string"
    }
]
```

---

### 63. Retrieve Challenge Stats

**Endpoint:** `GET /api/v1/users/battle/challenge/:challengeID` **Path Variables:**

- `challengeID` (string) - The unique identifier of the challenge.

**Response:** **Status Code:** `200 OK`

```json
{
    "challengeID": "string",
    "opponent": "string",
    "score": "integer",
    "status": "string"
}
```

---

### 64. Exit Challenge

**Endpoint:** `GET /api/v1/users/battle/challenge/exit/:challengeID` **Path Variables:**

- `challengeID` (string) - The ID of the challenge to exit.

**Response:** **Status Code:** `200 OK`

```json
{
    "message": "Exited challenge successfully"
}
```

---

# Rank Management

### 65. Retrieve Local & Global Ranks

**Endpoint:** `GET /api/v1/users/rank/:period` **Path Variables:**

- `period` (string) - Timeframe for ranking (day, week, month, year).

**Response:** **Status Code:** `200 OK`

```json
[
    {
        "userID": "string",
        "rank": "integer",
        "score": "integer"
    }
]
```

---

### 66. Retrieve Ranks Metadata

**Endpoint:** `GET /api/v1/ranks/metadata` **Description:** Retrieves metadata about the ranking system.

**Response:** **Status Code:** `200 OK`

```json
{
    "totalUsers": "integer",
    "topScore": "integer",
    "averageScore": "integer"
}
```