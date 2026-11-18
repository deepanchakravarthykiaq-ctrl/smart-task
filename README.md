# Smart Task Management System

## 1. Project Overview

The **Smart Task Management System** is a microservices-based web application designed to help users efficiently manage their daily tasks.

Users can register, log in, create tasks, view tasks, update task details, and delete completed or unnecessary tasks.

The application uses a React frontend, Node.js and Express microservices, MongoDB database, and Docker for containerization.

### Key Features

- User registration and login.
- JWT-based authentication.
- Create new tasks.
- View all tasks.
- Update existing tasks.
- Delete tasks.
- REST API integration.
- Microservices architecture.
- Docker containerization.
- API Gateway for centralized API access.

## 2. Microservices Architecture

The project follows a microservices architecture in which each service performs a separate responsibility.

### Architecture Components

| Component | Responsibility | Port |
|---|---|---:|
| Frontend | React user interface | 5173 |
| API Gateway | Routes client requests | 5000 |
| Auth Service | Registration and login | 5001 |
| Task Service | Task CRUD operations | 5002 |
| Notification Service | Notification management | 5003 |
| Report Service | Report management | 5004 |
| MongoDB | Database storage | 27017 |

### Architecture Flow

1. User interacts with the React frontend.
2. Frontend sends HTTP requests to the API Gateway.
3. API Gateway forwards requests to the appropriate microservice.
4. Authentication service validates user credentials and JWT tokens.
5. Task service handles task operations.
6. MongoDB stores application data.
7. The response is returned to the frontend.

## 3. Technology Stack

| Technology | Purpose |
|---|---|
| React.js | Frontend development |
| JavaScript | Application programming |
| Node.js | Backend runtime |
| Express.js | REST API development |
| MongoDB | Database |
| JWT | Authentication |
| Axios | Frontend API communication |
| Docker | Containerization |
| Docker Compose | Container orchestration |
| Git | Version control |
| GitHub | Source code hosting |

## 4. Docker Containers and Port Numbers

The application consists of the following services:

| Service | Port |
|---|---:|
| Frontend | 5173 |
| API Gateway | 5000 |
| Auth Service | 5001 |
| Task Service | 5002 |
| Notification Service | 5003 |
| Report Service | 5004 |
| MongoDB | 27017 |

### Verify Running Containers

```bash
docker ps
```

### Check Docker Compose Services

```bash
docker compose ps
```

## 5. API Endpoint Documentation

Base URL:

```text
http://localhost:5000
```

### API Gateway

| Method | Endpoint | Description |
|---|---|---|
| GET | /health | Gateway health check |
| GET | /metrics | Gateway metrics |

### Authentication Service

| Method | Endpoint | Description |
|---|---|---|
| POST | /api/auth/register | Register a new user |
| POST | /api/auth/login | User login |
| GET | /api/auth/profile | Get authenticated user profile |

### Task Management Service

| Method | Endpoint | Description |
|---|---|---|
| GET | /api/tasks | Get tasks |
| GET | /api/tasks/all | Get all tasks |
| GET | /api/tasks/:id | Get task by ID |
| POST | /api/tasks/create | Create a new task |
| PUT | /api/tasks/:id | Update an existing task |
| DELETE | /api/tasks/:id | Delete a task |

### Notification Service

| Method | Endpoint | Description |
|---|---|---|
| GET | /api/notifications | Get notifications |
| POST | /api/notifications/create | Create notification |

### Report Service

| Method | Endpoint | Description |
|---|---|---|
| GET | /api/reports | Get reports |
| POST | /api/reports/create | Create report |

**Note:** The notification and report gateway prefixes should be checked against the API Gateway configuration before publishing. The service route paths are identified, but their complete public gateway URLs need verification.

## 6. Installation and Docker Startup Commands

### Step 1: Clone Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

### Step 2: Navigate to Project

```bash
cd Smart-Task-Management-System-main
```

### Step 3: Install Dependencies

Install dependencies in the respective frontend and service directories using:

```bash
npm install
```

### Step 4: Start Docker Containers

```bash
docker compose up --build
```

### Step 5: Check Running Containers

```bash
docker compose ps
```

### Step 6: View Container Logs

```bash
docker compose logs -f
```

### Step 7: Access Application

Frontend:

```text
http://localhost:5173
```

API Gateway:

```text
http://localhost:5000
```

### Step 8: Stop Containers

```bash
docker compose down
```

## 7. Login and Task Management Testing

The following application functionality has been tested.

### Login Testing

1. Open the frontend application.
2. Navigate to the login page.
3. Enter registered user credentials.
4. Click Login.
5. Verify successful authentication.
6. Verify redirection to the dashboard.

Login API:

```bash
curl -X POST http://localhost:5000/api/auth/login \
-H "Content-Type: application/json" \
-d '{"email":"YOUR_EMAIL","password":"YOUR_PASSWORD"}'
```

Expected result: HTTP 200 OK for valid credentials.

### Create Task

```bash
curl -X POST http://localhost:5000/api/tasks/create \
-H "Content-Type: application/json" \
-H "Authorization: Bearer YOUR_TOKEN" \
-H "Accept: application/json" \
-d '{"title":"Testing Task","description":"Testing task creation"}'
```

Expected result: HTTP 201 Created.

### View Tasks

```bash
curl http://localhost:5000/api/tasks \
-H "Authorization: Bearer YOUR_TOKEN"
```

Expected result: HTTP 200 OK.

### Update Task

```bash
curl -X PUT http://localhost:5000/api/tasks/TASK_ID \
-H "Content-Type: application/json" \
-H "Authorization: Bearer YOUR_TOKEN" \
-d '{"title":"Updated Testing Task"}'
```

### Delete Task

```bash
curl -X DELETE http://localhost:5000/api/tasks/TASK_ID \
-H "Authorization: Bearer YOUR_TOKEN"
```

### Testing Results

| Test Case | Status |
|---|---|
| User Login | Passed |
| Task Creation | Passed |
| View Tasks | Passed |
| Update Task | Passed |
| Delete Task | Passed |
| Notification Service | Pending verification |
| Report Service | Pending verification |

## 8. Screenshots

Add screenshots of your actual application to demonstrate the working functionality.

Create a screenshots folder:

```bash
mkdir screenshots
```

Recommended screenshots:

### Application Login Page

![Login Page](screenshots/login.png)

### Dashboard

![Dashboard](screenshots/dashboard.png)

### Create Task

![Create Task](screenshots/create-task.png)

### View Tasks

![View Tasks](screenshots/view-tasks.png)

### Update Task

![Update Task](screenshots/update-task.png)

### Docker Containers

![Docker Containers](screenshots/docker-containers.png)

### API Testing

![API Testing](screenshots/api-testing.png)

## 9. Future Improvements

- Implement role-based access control.
- Add email notifications.
- Improve task priority management.
- Add task deadlines and reminders.
- Develop advanced reporting and analytics.
- Implement automated testing.
- Add CI/CD pipeline using Jenkins or GitHub Actions.
- Deploy the application using Kubernetes.
- Improve application monitoring and logging.

## Conclusion

The Smart Task Management System demonstrates the implementation of a microservices-based web application using React, Node.js, Express.js, MongoDB, and Docker.

The project provides practical experience in REST API development, authentication, task management, containerization, and microservices communication.
