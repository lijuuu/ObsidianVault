
---

**Base URL:**

```
https://api.example.com/v1
```

---

## **1. Question Management**

### **Add New Question**

- **Endpoint:**  
    `POST /questions`
- **Headers:**  
    `Content-Type: application/json`  
    `Authorization: Bearer <jwt_token>`
- **Request Body:**
    
    ```json
    {
      "title": "How to implement authentication in Node.js?",
      "body": "I'm building an authentication system using Node.js. What are the best practices?",
      "tags": ["nodejs", "authentication", "security"]
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "questionId": "q12345",
      "message": "Question posted successfully"
    }
    ```
    

---

### **Edit/Update Question**

- **Endpoint:**  
    `PUT /questions/{questionId}`
- **Headers:**  
    `Content-Type: application/json`  
    `Authorization: Bearer <jwt_token>`
- **Request Body:**
    
    ```json
    {
      "title": "Updated Title: How to implement authentication in Node.js?",
      "body": "I added more details about JWT integration with Node.js.",
      "tags": ["nodejs", "jwt", "security"]
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Question updated successfully"
    }
    ```
    

---

### **Remove/Delete Question**

- **Endpoint:**  
    `DELETE /questions/{questionId}`
- **Headers:**  
    `Authorization: Bearer <jwt_token>`
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Question deleted successfully"
    }
    ```
    

---

### **View All Questions**

- **Endpoint:**  
    `GET /questions`
- **Optional Query Parameters:**
    - `page` (number): For pagination
    - `limit` (number): Items per page
    - `tag` (string): Filter by a specific tag
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "questions": [
        {
          "questionId": "q12345",
          "title": "How to implement authentication in Node.js?",
          "body": "I'm building a secure authentication system...",
          "tags": ["nodejs", "authentication", "security"],
          "createdAt": "2024-07-12T12:34:56Z",
          "author": {
            "userId": "12345",
            "name": "John Doe"
          },
          "votes": 10,
          "answersCount": 2
        }
      ],
      "pagination": {
        "page": 1,
        "limit": 10,
        "totalPages": 5,
        "totalItems": 50
      }
    }
    ```
    

---

### **View Detailed Question Data (including Answers)**

- **Endpoint:**  
    `GET /questions/{questionId}`
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "questionId": "q12345",
      "title": "How to implement authentication in Node.js?",
      "body": "I'm building a secure authentication system...",
      "tags": ["nodejs", "authentication", "security"],
      "createdAt": "2024-07-12T12:34:56Z",
      "author": {
        "userId": "12345",
        "name": "John Doe"
      },
      "votes": 10,
      "answers": [
        {
          "answerId": "a98765",
          "body": "You can use Passport.js to handle authentication effectively.",
          "votes": 5,
          "createdAt": "2024-07-12T14:00:00Z",
          "author": {
            "userId": "67890",
            "name": "Jane Smith"
          }
        }
      ]
    }
    ```
    

---

## **2. Answer Management**

### **Add Answer**

- **Endpoint:**  
    `POST /questions/{questionId}/answers`
- **Headers:**  
    `Content-Type: application/json`  
    `Authorization: Bearer <jwt_token>`
- **Request Body:**
    
    ```json
    {
      "body": "I recommend using Passport.js because it provides various strategies for authentication."
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "answerId": "a98765",
      "message": "Answer added successfully"
    }
    ```
    

---

### **Edit/Update Answer**

- **Endpoint:**  
    `PUT /answers/{answerId}`
- **Headers:**  
    `Content-Type: application/json`  
    `Authorization: Bearer <jwt_token>`
- **Request Body:**
    
    ```json
    {
      "body": "Updated: Passport.js can be integrated with Express for a robust solution."
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Answer updated successfully"
    }
    ```
    

---

### **Remove/Delete Answer**

- **Endpoint:**  
    `DELETE /answers/{answerId}`
- **Headers:**  
    `Authorization: Bearer <jwt_token>`
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Answer deleted successfully"
    }
    ```
    

---

## **3. Voting & Reputation**

### **Vote on a Question**

- **Endpoint:**  
    `POST /questions/{questionId}/vote`
- **Headers:**  
    `Content-Type: application/json`  
    `Authorization: Bearer <jwt_token>`
- **Request Body:**
    
    ```json
    {
      "voteType": "upvote"  // or "downvote"
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Your vote has been recorded",
      "votes": 11
    }
    ```
    

---

### **Vote on an Answer**

- **Endpoint:**  
    `POST /answers/{answerId}/vote`
- **Headers:**  
    `Content-Type: application/json`  
    `Authorization: Bearer <jwt_token>`
- **Request Body:**
    
    ```json
    {
      "voteType": "downvote"  // or "upvote"
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Your vote has been recorded",
      "votes": 4
    }
    ```
    

---

### **Get User Reputation**

- **Endpoint:**  
    `GET /users/{userId}/reputation`
- **Headers:**  
    `Authorization: Bearer <jwt_token>`
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "userId": "12345",
      "reputation": 1500,
      "upvotesReceived": 50,
      "downvotesReceived": 5
    }
    ```
    

---

## **4. Badge Awarding**

### **Get User Badges**

- **Endpoint:**  
    `GET /users/{userId}/badges`
- **Headers:**  
    `Authorization: Bearer <jwt_token>`
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "badges": [
        {
          "badgeId": "b001",
          "name": "Quality Answer",
          "description": "Awarded for providing an answer with high upvotes.",
          "awardedAt": "2024-07-15T10:00:00Z"
        }
      ]
    }
    ```
    

---

### **Award a Badge (Admin Endpoint)**

- **Endpoint:**  
    `POST /admin/badges/award`
- **Headers:**  
    `Content-Type: application/json`  
    `Authorization: Bearer <admin_jwt_token>`
- **Request Body:**
    
    ```json
    {
      "userId": "12345",
      "badgeId": "b001",
      "name": "Quality Answer",
      "description": "Awarded for providing an answer with high upvotes."
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Badge awarded successfully",
      "badge": {
        "badgeId": "b001",
        "name": "Quality Answer",
        "description": "Awarded for providing an answer with high upvotes.",
        "awardedAt": "2024-07-15T10:00:00Z"
      }
    }
    ```
    
---

## **7. Badge Management (Admin Endpoints)**

### **Create a Badge**

- **Endpoint:**  
    `POST /admin/badges`
    
- **Headers:**  
    `Authorization: Bearer admin_jwt_token`  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "name": "Quality Answer",
      "description": "Awarded for providing an answer with high upvotes",
      "criteria": "Answer must receive over 50 upvotes",
      "iconURL": "https://example.com/badge-quality.png"
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "badgeId": "b001",
      "message": "Badge created successfully",
      "badge": {
        "badgeId": "b001",
        "name": "Quality Answer",
        "description": "Awarded for providing an answer with high upvotes",
        "criteria": "Answer must receive over 50 upvotes",
        "iconURL": "https://example.com/badge-quality.png",
        "createdAt": "2024-07-15T10:00:00Z"
      }
    }
    ```
    

---

### **Edit a Badge**

- **Endpoint:**  
    `PUT /admin/badges/{badgeId}`
    
- **Headers:**  
    `Authorization: Bearer admin_jwt_token`  
    `Content-Type: application/json`
    
- **Request Body:**
    
    ```json
    {
      "name": "Quality Answer Updated",
      "description": "Awarded for answers that receive high upvotes consistently",
      "criteria": "Answer must receive over 75 upvotes",
      "iconURL": "https://example.com/badge-quality-updated.png"
    }
    ```
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Badge updated successfully",
      "badge": {
        "badgeId": "b001",
        "name": "Quality Answer Updated",
        "description": "Awarded for answers that receive high upvotes consistently",
        "criteria": "Answer must receive over 75 upvotes",
        "iconURL": "https://example.com/badge-quality-updated.png",
        "updatedAt": "2024-07-16T11:00:00Z"
      }
    }
    ```
    

---

### **Delete a Badge**

- **Endpoint:**  
    `DELETE /admin/badges/{badgeId}`
    
- **Headers:**  
    `Authorization: Bearer admin_jwt_token`
    
- **Response:**
    **Status Code:** `200 OK`
    ```json
    {
      "message": "Badge deleted successfully"
    }
    ```
    

---

