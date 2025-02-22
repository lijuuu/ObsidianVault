
---

**Base URL:**

```
https://api.example.com/v1
```

---

## **1. Authentication**

### **Signup a New User**

- **Endpoint:**  
    `POST /auth/user/signup`
    
- **Headers:**  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "firstName": "John",
      "lastName": "Doe",
      "email": "john@example.com",
      "password": "securepassword",
      "authType": "email"
    }
    ```
    
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "userId": "12345",
      "message": "User registered successfully"
    }
    ```
    

---

### **Login a User**

- **Endpoint:**  
    `POST /auth/user/login`
    
- **Headers:**  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "email": "johnuser@example.com",
      "password": "securepassword"
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "token": "jwt_token_here",
      "message": "Login successful"
    }
    ```
    

---

### **Login a Admin**

- **Endpoint:**  
    `POST /auth/admin/login`
    
- **Headers:**  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "email": "johnadmin@example.com",
      "password": "securepassword"
    }
    ```
    
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "token": "jwt_token_here",
      "message": "Login successful"
    }
    ```
    

---

### **Forgot Password**

- **Endpoint:**  
    `POST /auth/user/forgot-password`
    
- **Headers:**  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "email": "john@example.com"
    }
    ```
    
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "message": "Password reset link sent to your email"
    }
    ```
    

---

### **Update Password**

- **Endpoint:**  
    `PUT /auth/user/update-password`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "oldPassword": "securepassword",
      "newPassword": "newSecurePassword"
    }
    ```
    
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "message": "Password updated successfully"
    }
    ```
    

---

## **2. User Profile Management**

### **Get User Profile**

- **Endpoint:**  
    `GET /users/{userId}`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "userId": "12345",
      "firstName": "John",
      "lastName": "Doe",
      "place": "New York",
      "role": "admin",
      "rank": 10,
      "topics": ["golang", "mongodb"],
      "reputation": {
        "questionsAnswered": 50,
        "questionsAsked": 20,
        "tipsReceived": 15,
        "tipsGiven": 5
      },
      "isBanned": false,
      "badgeURL": "https://example.com/badge.png",
      "email": "john@example.com",
      "authType": "github",
      "socials": {
        "github": "johndoe"
      },
      "streakHeatMap": [{ "2024-07-12": 3 }, { "2024-07-13": 1 }]
    }
    ```
    

---

### **Update Profile Details (Name, Place, Role, Add Social)**

- **Endpoint:**  
    `PUT /users/{userId}`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "firstName": "John",
      "lastName": "Doe",
      "place": "San Francisco",
      "role": "moderator",
      "socials": {
        "github": "johndoe",
        "linkedin": "john-doe"
      }
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Profile updated successfully"
    }
    ```
    

---

### **Delete Profile Photo**

- **Endpoint:**  
    `DELETE /users/{userId}/photo`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`
    
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "message": "Profile photo deleted successfully"
    }
    ```
    

---

### **Update Profile Photo**

- **Endpoint:**  
    `PUT /users/{userId}/photo`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`  
    `Content-Type: multipart/form-data`
    
- **Request Body:**  
    _(Form-data)_
    
    - **Field:** `file` (e.g., `profile.jpg`)
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "message": "Profile photo updated successfully",
      "photoURL": "https://example.com/new-profile.jpg"
    }
    ```
    

---

## **3. Topic Management**

### **Get Topics Followed by User**

- **Endpoint:**  
    `GET /users/{userId}/topics`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`
    
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "topics": ["golang", "mongodb"]
    }
    ```
    

---

### **Follow a Topic**

- **Endpoint:**  
    `POST /users/{userId}/topics`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`  
    `Content-Type: application/json`
    
- **Request Body:**
     
    ```json
    {
      "topic": "javascript"
    }
    ```
    
- **Response:**
     **Status Code:** `200 OK`
    ```json
    {
      "message": "Topic followed successfully"
    }
    ```
    

---

### **Unfollow a Topic**

- **Endpoint:**  
    `DELETE /users/{userId}/topics/{topicName}`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`
    
- **Response:**
    **Status Code:** `200 OK`    
    ```json
    {
      "message": "Topic unfollowed successfully"
    }
    ```
    

---

## **4. Admin Actions**

### **Ban a User**

- **Endpoint:**  
    `PUT /admin/users/{userId}/ban`
    
- **Headers:**  
    `Authorization: Bearer admin_jwt_token`  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "isBanned": true,
      "banReason": "Violation of community guidelines"
    }
    ```
    
- **Response:**
	**Status Code:** `200 OK`
    ```json
    {
      "message": "User banned successfully"
    }
    ```
    

---

### **Unban a User**

- **Endpoint:**  
    `PUT /admin/users/{userId}/unban`
    
- **Headers:**  
    `Authorization: Bearer admin_jwt_token`
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "User unbanned successfully"
    }
    ```
    

---

## **5. Reputation System**

### **Get User Reputation**

- **Endpoint:**  
    `GET /users/{userId}/reputation`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "questionsAnswered": 50,
      "questionsAsked": 20,
      "tipsReceived": 15,
      "tipsGiven": 5
    }
    ```
    

---

## **6. User Activity Heat Map**

### **Get User Activity Heat Map**

- **Endpoint:**  
    `GET /users/{userId}/heatmap`
    
- **Headers:**  
    `Authorization: Bearer jwt_token_here`
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "streakHeatMap": [{ "2024-07-12": 3 }, { "2024-07-13": 1 }]
    }
    ```
    

---