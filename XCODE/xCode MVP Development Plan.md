
## **Overview**
The Xcode MVP will deliver a scalable, sandboxed coding platform with user management, problem-solving capabilities, and real-time competitive features. The 5-week plan focuses on building core infrastructure, integrating microservices, and deploying a production-ready system with performance optimizations.

---

## **Week 1: Core Infrastructure and User Management Foundation**
**Objective:** Establish the sandboxed execution engine, basic compiler frontend, and start user management.

### **Tasks**
1. **Sandboxed Code Engine**
   - Develop a Docker-based sandboxed execution engine (`executor` package).
   - Conduct performance tests using Grafana k6.
   - Deploy and test on an EC2 instance to validate scalability and reliability.

2. **Compiler Frontend**
   - Build a basic frontend for code submission and execution.
   - Integrate with the sandboxed engine for running submitted code.

3. **User Management**
   - Begin implementing `AuthUserAdminService` (gRPC) for user registration, login, and basic admin features.  "isBanned": false,
            "isVerified": true,

---

## **Week 2: User Management Completion and Problem Setup**
**Objective:** Finalize user management, connect the execution engine to microservices, and set up problem management.

### **Tasks**
1. **User Management Backend**
   - Complete `AuthUserAdminService` with login, 2FA, password recovery, profile management, and admin features (block, verify, etc.).
   - Develop frontend for authentication (login, signup) and user profiles.

2. **Microservice Integration**
   - Connect the sandboxed code engine to the microservice architecture using gRPC.
   - Define service boundaries (e.g., UserService, ExecutionService).

3. **Message Queue NATS**
   - Integrate NATS for real-time messaging between Execution Service, Compiler, and Challenge System (e.g., submission updates, execution results).

4. **Admin Portal**
   - Create an admin portal backend and frontend to add problems, validator code, and test cases.
---

## **Week 3: Problems and Competitive Features**
**Objective:** Implement problem browsing/submission and start real-time coding matches.

### **Tasks**
1. **Problem Frontend**
   - Build a frontend for listing problems (filter by category, difficulty, tags) and managing submissions.

2. **Problem Execution**
   - Implement LeetCode-style problem execution with test cases, integrating Compiler and Sandboxed Engine for instant feedback.

3. **1-to-1 Coding Matches**
   - Start backend implementation for 1-to-1 coding matches with basic real-time capabilities (e.g., match initiation, submission tracking).

---

## **Week 4: Challenges and Frontend Completion**
**Objective:** Complete real-time coding matches and finalize the frontend.

### **Tasks**
1. **1-to-1 Matches**
   - Finish 1-to-1 match implementation using WebSocket (WSS) for real-time updates and submissions (e.g., live code execution, opponent progress).

2. **Frontend Finalization**
   - Complete frontend for problems (submission UI), challenges (match interface), and user profiles (view/edit).

---

## **Week 5: Hosting, Refactoring, and Scalability Enhancements**
**Objective:** Deploy the MVP to production, optimize performance, and ensure scalability.

### **Tasks**
1. **Dockerization**
   - Dockerize all microservices: UserService, CompilerService, Sandboxed Engine, Execution Service.

2. **CI/CD Pipeline**
   - Set up CI/CD pipelines (e.g., GitHub Actions or Jenkins) for automated builds, tests, and deployments.

3. **Kubernetes Deployment**
   - Deploy the application to Kubernetes (k8s) for orchestration and scalability.

4. **Code Refactoring**
   - Refactor code for performance (e.g., optimize gRPC calls, database queries) and maintainability (e.g., modular structure, clear error handling).

5. **Caching with Memcached**
   - Integrate Memcached for caching user sessions, problem results, and submission outcomes to enhance Execution Service performance.

---