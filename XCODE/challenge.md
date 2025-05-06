### 1. `CreateChallenge`
**Request**: `CreateChallengeRequest` (JSON)
```json
{
  "title": "Code Wars",
  "creator_id": "user1",
  "difficulty": "Medium",
  "is_private": false,
  "problem_ids": ["problem1", "problem2", "problem3"],
  "time_limit": 3600,
  "start_at": {
    "seconds": 1697059500,
    "nanos": 0
  }
}
```

**Response**: `CreateChallengeResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "id": "challenge1",
    "password": "xyz123",
    "join_url": "https://example.com/challenges/challenge1/join"
  },
  "Error": null
}
```

---

### 2. `GetChallengeDetails`
**Request**: `GetChallengeDetailsRequest` (Query Parameters)
```
challenge_id=challenge1&user_id=user1
```

**Response**: `GetChallengeDetailsResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "challenge": {
      "id": "challenge1",
      "title": "Code Wars",
      "creator_id": "user1",
      "difficulty": "Medium",
      "is_private": false,
      "status": "active",
      "password": null,
      "problem_ids": ["problem1", "problem2", "problem3"],
      "time_limit": 3600,
      "created_at": 1697059200,
      "is_active": true,
      "participant_ids": ["user1", "user2", "user3"],
      "user_problem_metadata": {
        "user1": {
          "challenge_problem_metadata": [
            {
              "problem_id": "problem1",
              "score": 100,
              "time_taken": 1200,
              "completed_at": 1697060000
            }
          ]
        },
        "user2": {
          "challenge_problem_metadata": []
        }
      },
      "start_time": 1697059500,
      "end_time": 1697063100
    },
    "leaderboard": [
      {
        "user_id": "user1",
        "problems_completed": 1,
        "total_score": 100,
        "rank": 1
      },
      {
        "user_id": "user2",
        "problems_completed": 0,
        "total_score": 0,
        "rank": 2
      }
    ]
  },
  "Error": null
}
```

---

### 3. `GetPublicChallenges`
**Request**: `GetPublicChallengesRequest` (Query Parameters)
```
difficulty=Medium&is_active=true&page=1&page_size=10&user_id=user1&include_private=false
```

**Response**: `GetPublicChallengesResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "challenges": [
      {
        "id": "challenge1",
        "title": "Code Wars",
        "creator_id": "user1",
        "difficulty": "Medium",
        "is_private": false,
        "status": "active",
        "password": null,
        "problem_ids": ["problem1", "problem2", "problem3"],
        "time_limit": 3600,
        "created_at": 1697059200,
        "is_active": true,
        "participant_ids": ["user1", "user2", "user3"],
        "user_problem_metadata": {},
        "start_time": 1697059500,
        "end_time": 1697063100
      },
      {
        "id": "challenge2",
        "title": "Algorithm Sprint",
        "creator_id": "user2",
        "difficulty": "Hard",
        "is_private": true,
        "status": "pending",
        "password": "xyz123",
        "problem_ids": ["problem4", "problem5"],
        "time_limit": 7200,
        "created_at": 1697062800,
        "is_active": false,
        "participant_ids": ["user2"],
        "user_problem_metadata": {},
        "start_time": 0,
        "end_time": 0
      }
    ]
  },
  "Error": null
}
```

---

### 4. `JoinChallenge`
**Request**: `JoinChallengeRequest` (JSON)
```json
{
  "challenge_id": "challenge1",
  "user_id": "user1",
  "password": null
}
```

**Response**: `JoinChallengeResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "challenge_id": "challenge1",
    "success": true,
    "message": "Successfully joined challenge"
  },
  "Error": null
}
```

---

### 5. `StartChallenge`
**Request**: `StartChallengeRequest` (JSON)
```json
{
  "challenge_id": "challenge1",
  "user_id": "user1"
}
```

**Response**: `StartChallengeResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "success": true,
    "start_time": 1697059500
  },
  "Error": null
}
```

---

### 6. `EndChallenge`
**Request**: `EndChallengeRequest` (JSON)
```json
{
  "challenge_id": "challenge1",
  "user_id": "user1"
}
```

**Response**: `EndChallengeResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "message": "Challenge ended successfully",
    "leaderboard": [
      {
        "user_id": "user1",
        "problems_completed": 1,
        "total_score": 100,
        "rank": 1
      },
      {
        "user_id": "user2",
        "problems_completed": 0,
        "total_score": 0,
        "rank": 2
      }
    ]
  },
  "Error": null
}
```

---

### 7. `GetSubmissionStatus`
**Request**: `GetSubmissionStatusRequest` (Query Parameters)
```
submission_id=submission1
```

**Response**: `GetSubmissionStatusResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "submission": {
      "id": "submission1",
      "problem_id": "problem1",
      "user_id": "user1",
      "challenge_id": "challenge1",
      "submitted_at": {
        "seconds": 1697060000,
        "nanos": 0
      },
      "score": 100,
      "status": "accepted",
      "output": "Correct output",
      "language": "python",
      "execution_time": 0.123,
      "difficulty": "Medium",
      "is_first": true,
      "title": "Two Sum",
      "user_code": "def two_sum(nums, target):\n    for i in range(len(nums)):\n        for j in range(i+1, len(nums)):\n            if nums[i] + nums[j] == target:\n                return [i, j]\n    return []"
    }
  },
  "Error": null
}
```

---

### 8. `GetChallengeSubmissions`
**Request**: `GetChallengeSubmissionsRequest` (Query Parameters)
```
challenge_id=challenge1
```

**Response**: `GetChallengeSubmissionsResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": [
    {
      "id": "submission1",
      "problem_id": "problem1",
      "user_id": "user1",
      "challenge_id": "challenge1",
      "submitted_at": {
        "seconds": 1697060000,
        "nanos": 0
      },
      "score": 100,
      "status": "accepted",
      "output": "Correct output",
      "language": "python",
      "execution_time": 0.123,
      "difficulty": "Medium",
      "is_first": true,
      "title": "Two Sum",
      "user_code": "def two_sum(nums, target):\n    for i in range(len(nums)):\n        for j in range(i+1, len(nums)):\n            if nums[i] + nums[j] == target:\n                return [i, j]\n    return []"
    },
    {
      "id": "submission2",
      "problem_id": "problem2",
      "user_id": "user2",
      "challenge_id": "challenge1",
      "submitted_at": {
        "seconds": 1697060100,
        "nanos": 0
      },
      "score": 0,
      "status": "wrong_answer",
      "output": "Incorrect output",
      "language": "java",
      "execution_time": 0.200,
      "difficulty": "Medium",
      "is_first": false,
      "title": "Reverse String",
      "user_code": "public class Solution {\n    public void reverseString(char[] s) {\n        int left = 0, right = s.length - 1;\n        while (left < right) {\n            char temp = s[left];\n            s[left++] = s[right];\n            s[right--] = temp;\n        }\n    }\n}"
    }
  ],
  "Error": null
}
```

---

### 9. `GetUserStats`
**Request**: `GetUserStatsRequest` (Query Parameters)
```
user_id=user1
```

**Response**: `GetUserStatsResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "stats": {
      "user_id": "user1",
      "problems_completed": 10,
      "total_time_taken": 12000,
      "challenges_completed": 5,
      "score": 1750.5,
      "challenge_stats": {
        "challenge1": {
          "rank": 1,
          "problems_completed": 3,
          "total_score": 300
        },
        "challenge2": {
          "rank": 2,
          "problems_completed": 1,
          "total_score": 100
        }
      }
    }
  },
  "Error": null
}
```

---

### 10. `GetChallengeUserStats`
**Request**: `GetChallengeUserStatsRequest` (Query Parameters)
```
challenge_id=challenge1&user_id=user1
```

**Response**: `GetChallengeUserStatsResponse` wrapped in `GenericResponse` (JSON)
```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "user_id": "user1",
    "problems_completed": 3,
    "total_score": 300,
    "rank": 1,
    "challenge_problem_metadata": [
      {
        "problem_id": "problem1",
        "score": 100,
        "time_taken": 1200,
        "completed_at": 1697060000
      },
      {
        "problem_id": "problem2",
        "score": 100,
        "time_taken": 1500,
        "completed_at": 1697060100
      },
      {
        "problem_id": "problem3",
        "score": 100,
        "time_taken": 1800,
        "completed_at": 1697060200
      }
    ]
  },
  "Error": null
}
```
# GetUserChallengeHistory

### Request: `GetUserChallengeHistoryRequest` (Query Parameters)

```
user_id=user1&page=1&page_size=10
```

### Response: `GetUserChallengeHistoryResponse` wrapped in `GenericResponse` (JSON)

```json
{
  "Success": true,
  "Status": 200,
  "Payload": {
    "challenges": [
      {
        "id": "challenge1",
        "title": "Code Wars",
        "creator_id": "user1",
        "difficulty": "Medium",
        "is_private": false,
        "status": "active",
        "password": null,
        "problem_ids": ["problem1", "problem2", "problem3"],
        "time_limit": 3600,
        "created_at": {
          "seconds": 1697059200,
          "nanos": 0
        },
        "is_active": true,
        "participant_ids": ["user1", "user2", "user3"],
        "user_problem_metadata": {
          "user1": {
            "challenge_problem_metadata": [
              {
                "problem_id": "problem1",
                "score": 100,
                "time_taken": 1200,
                "completed_at": 1697060000
              }
            ]
          },
          "user2": {
            "challenge_problem_metadata": []
          }
        },
        "start_time": {
          "seconds": 1697059500,
          "nanos": 0
        },
        "end_time": {
          "seconds": 1697063100,
          "nanos": 0
        }
      },
      {
        "id": "challenge2",
        "title": "Algorithm Sprint",
        "creator_id": "user2",
        "difficulty": "Hard",
        "is_private": true,
        "status": "ended",
        "password": "xyz123",
        "problem_ids": ["problem4", "problem5"],
        "time_limit": 7200,
        "created_at": {
          "seconds": 1697062800,
          "nanos": 0
        },
        "is_active": false,
        "participant_ids": ["user1", "user2"],
        "user_problem_metadata": {
          "user1": {
            "challenge_problem_metadata": [
              {
                "problem_id": "problem4",
                "score": 50,
                "time_taken": 1800,
                "completed_at": 1697064600
              }
            ]
          }
        },
        "start_time": {
          "seconds": 1697063000,
          "nanos": 0
        },
        "end_time": {
          "seconds": 1697070200,
          "nanos": 0
        }
      }
    ],
    "total_count": 2,
    "page": 1,
    "page_size": 10,
    "message": "Challenge history retrieved successfully"
  },
  "Error": null
}
```

### Error Response Example (Missing user_id)

```json
{
  "Success": false,
  "Status": 400,
  "Payload": null,
  "Error": {
    "ErrorType": "INVALID_REQUEST",
    "Code": 400,
    "Message": "Missing required field: user_id",
    "Details": "The user_id query parameter is required"
  }
}
```

### Error Response Example (No Challenges Found)

```json
{
  "Success": false,
  "Status": 404,
  "Payload": null,
  "Error": {
    "ErrorType": "NOT_FOUND",
    "Code": 404,
    "Message": "No challenges found for the user",
    "Details": "No challenges found for the user"
  }
}
```
POST   http://localhost:7000/api/v1/challenges
GET    http://localhost:7000/api/v1/challenges/details
GET    http://localhost:7000/api/v1/challenges/public
POST   http://localhost:7000/api/v1/challenges/join
POST   http://localhost:7000/api/v1/challenges/start
POST   http://localhost:7000/api/v1/challenges/end
GET    http://localhost:7000/api/v1/challenges/submissions/status
GET    http://localhost:7000/api/v1/challenges/submissions
GET    http://localhost:7000/api/v1/challenges/stats/user
GET    http://localhost:7000/api/v1/challenges/stats/challenge-user

