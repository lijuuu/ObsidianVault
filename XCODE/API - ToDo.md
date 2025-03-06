
---

### Minimal API Cheatsheet

| **Endpoint**                             | **Method** | **Auth** | **Data Needed**                                                               | **Notes**                   | **Done** |
| ---------------------------------------- | ---------- | -------- | ----------------------------------------------------------------------------- | --------------------------- | -------- |
| `/api/v1/auth/register`                  | POST       | None     | JSON: `firstName`, `lastName`, `email`, `password`, `confirmPassword`         | Optional: `country`, `role` | yes      |
| `/api/v1/auth/login`                     | POST       | None     | JSON: `email`, `password`                                                     | RefreshToken : `30days`     | yes      |
| `/api/v1/auth/token/refresh`             | POST       | None     | JSON: `refreshToken`                                                          | AccesToken:`7days`          | yes      |
| `/api/v1/auth/verify`                    | GET        | None     | Query: `email`, `token`                                                       |                             | yes      |
| `/api/v1/auth/otp/resend`                | GET        | None     | Query: `userID`                                                               |                             | yes      |
| `/api/v1/auth/password/forgot`           | GET        | None     | Query: `email`                                                                |                             | no       |
| `/api/v1/users/profile`                  | GET        | JWT      | JSON: `userID`                                                                | UserID typically from JWT   | yes      |
| `/api/v1/users/profile/update`           | PUT        | JWT      | JSON: `userID`, Optionally: `firstName`, `lastName`, `country`                |                             | yes      |
| `/api/v1/users/profile/image`            | PATCH      | JWT      | JSON: `userID`, `avatarURL`                                                   |                             | yes      |
| `/api/v1/users/follow`                   | POST       | JWT      | Query: `userID` (to follow)                                                   |                             | yes      |
| `/api/v1/users/follow`                   | DELETE     | JWT      | Query: `userID` (to unfollow)                                                 |                             | yes      |
| `/api/v1/users/follow/following`         | GET        | JWT      | Query: `userID` (optional, defaults to JWT)                                   |                             | yes      |
| `/api/v1/users/follow/followers`         | GET        | JWT      | Query: `userID` (optional, defaults to JWT)                                   |                             | yes      |
| `/api/v1/users/security/password/change` | POST       | JWT      | JSON: `userID`, `oldPassword`, `newPassword`, `confirmPassword`               |                             | no       |
| `/api/v1/users/security/2fa`             | POST       | JWT      | JSON: `userID`, `enable`                                                      |                             | no       |
| `/api/v1/users/logout`                   | POST       | JWT      | JSON: `userID`                                                                |                             | no       |
| `/api/v1/admin/login`                    | POST       | None     | JSON: `email`, `password`                                                     |                             | no       |
| `/api/v1/admin/users`                    | GET        | JWT      | Query: Optional `page`, `limit`, `roleFilter`, `statusFilter`                 | Admin only                  | no       |
| `/api/v1/admin/users`                    | POST       | JWT      | JSON: `firstName`, `lastName`, `email`, `password`, `confirmPassword`, `role` | Admin only                  | no       |
| `/api/v1/admin/users/update`             | PUT        | JWT      | Query: `userID`, JSON: Optionally: `firstName`, `email`                       | Admin only                  | no       |
| `/api/v1/admin/users/soft-delete`        | DELETE     | JWT      | Query: `userID`                                                               | Admin only                  | no       |
| `/api/v1/admin/users/verify`             | POST       | JWT      | Query: `userID`                                                               | Admin only                  | no       |
| `/api/v1/admin/users/unverify`           | POST       | JWT      | Query: `userID`                                                               | Admin only                  | no       |
| `/api/v1/admin/users/block`              | POST       | JWT      | Query: `userID`                                                               | Admin only                  | no       |
| `/api/v1/admin/users/unblock`            | POST       | JWT      | Query: `userID`                                                               | Admin only                  | no       |
| `/api/v1/admin/users/following`          | GET        | JWT      | Query: `userID`                                                               | Admin only                  | no       |
| `/api/v1/admin/users/followers`          | GET        | JWT      | Query: `userID`                                                               | Admin only                  | no       |


---

