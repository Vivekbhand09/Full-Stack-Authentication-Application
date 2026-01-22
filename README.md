# 🔐 Full Stack Authentication App  
![Java](https://img.shields.io/badge/Java-17-orange?style=for-the-badge&logo=java)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen?style=for-the-badge&logo=springboot)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6.x-6DB33F?style=for-the-badge&logo=springsecurity)
![JWT](https://img.shields.io/badge/JWT-Authentication-red?style=for-the-badge&logo=jsonwebtokens)
![OAuth2](https://img.shields.io/badge/OAuth2-Google%20%7C%20GitHub-orange?style=for-the-badge&logo=oauth)
![MySQL](https://img.shields.io/badge/MySQL-Database-4479A1?style=for-the-badge&logo=mysql)
![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react)
![Vite](https://img.shields.io/badge/Vite-Build%20Tool-646CFF?style=for-the-badge&logo=vite)
![TypeScript](https://img.shields.io/badge/TypeScript-Frontend-3178C6?style=for-the-badge&logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-Styling-38B2AC?style=for-the-badge&logo=tailwindcss)
![Axios](https://img.shields.io/badge/Axios-HTTP%20Client-5A29E4?style=for-the-badge&logo=axios)
![Swagger](https://img.shields.io/badge/OpenAPI-Swagger-85EA2D?style=for-the-badge&logo=swagger)

## React (Vite) + Spring Boot + JWT + OAuth2

A **production-ready full stack authentication system** built using **React (Vite)** on the frontend and **Spring Boot** on the backend.

This project demonstrates **modern authentication & authorization practices** used in real-world applications, including **JWT, OAuth2, refresh tokens, secure cookies, and role-based access control**.

---

## 🚀 Key Features

### 🔑 Authentication
- Username & Password authentication
- Password hashing using BCrypt
- JWT-based authentication (Access Token + Refresh Token)

### 🍪 Secure Cookie Handling
- HTTP-Only cookies for refresh tokens
- Secure, SameSite cookie configuration
- Protection against XSS attacks
- Optional secure flag for production

### 🔁 Refresh Token Flow
- Short-lived access tokens
- Long-lived refresh tokens
- Automatic access token renewal
- Silent refresh without re-login
- Logout invalidates refresh token

### 🌐 OAuth2 Authentication
- Google OAuth2 login
- GitHub OAuth2 login
- Automatic user creation on first OAuth login
- Unified JWT issuance for OAuth & local login

### 🧑‍💼 Multi-Role Based Authorization
- Support for multiple roles per user
- Role-based endpoint protection
- Predefined roles:
  - `ROLE_ADMIN`
  - `ROLE_USER`
  - `ROLE_GUEST`
- Method-level security using `@PreAuthorize`

### 📄 API Documentation
- OpenAPI 3 (Swagger)
- Production-ready API documentation
- JWT authorization support in Swagger UI
- Clear request/response schemas

### 🛡️ Security Best Practices
- Spring Security 6.x
- Stateless authentication
- CSRF disabled for APIs
- CORS configured for frontend
- Token validation filters

---

## 🧱 Tech Stack

### 🖥️ Frontend
- React (Vite)
- TypeScript
- Tailwind CSS
- Axios
- React Router DOM
- ShadCN UI (optional)
- JWT handling via cookies

### ⚙️ Backend
- Java 17
- Spring Boot 3.x
- Spring Security 6.x
- Spring Data JPA
- OAuth2 Client (Google, GitHub)
- JWT (Access + Refresh Tokens)
- MySQL
- Lombok
- HikariCP
- OpenAPI / Swagger

---
## 📁 Project Structure

```
src/
├── backend/
│   ├── java/com/substring/auth/app/
│   │   ├── auth/
│   │   │   ├── config/        # JWT, OAuth2, Security config
│   │   │   ├── controllers/   # Auth & OAuth controllers
│   │   │   ├── entities/      # User, Role, Token entities
│   │   │   ├── helpers/       # Utility classes
│   │   │   ├── payload/       # Request / Response models
│   │   │   ├── repositories/  # JPA repositories
│   │   │   └── services/      # Business logic
│   │   │
│   │   ├── config/            # Global configuration
│   │   ├── dtos/              # Shared DTOs
│   │   ├── exceptions/        # Global exception handling
│   │   └── AuthBackend.java   # Spring Boot main class
│   │
│   └── resources/
│       ├── application.yaml
│       ├── application-dev.yml
│       ├── application-qa.yml
│       └── application-prod.yml
│
├── frontend/
│   └── src/
│       ├── assets/        # Static assets
│       ├── auth/          # Auth guards & context
│       ├── components/    # Reusable UI components
│       ├── config/        # App configuration
│       ├── models/        # TypeScript types
│       ├── pages/         # Pages (Login, Register, Dashboard)
│       ├── services/      # API calls (Axios)
│       │
│       ├── App.tsx
│       └── main.tsx
```


---

## ⚙️ Backend Setup (Spring Boot)

### 🧩 Prerequisites
- Java 17+
- Maven 3.9+
- MySQL
- Git

### 🧰 Steps to Run Backend

```bash
cd backend
```

```sql
CREATE DATABASE auth_app;
```

### `application.yml`

```yaml
server:
  port: 8081

spring:
  application:
    name: auth-backend

  datasource:
    url: jdbc:mysql://localhost:3306/auth_app
    username: root
    password: root

  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL8Dialect

security:
  jwt:
    secret: ${JWT_SECRET}
    issuer: auth-backend
    access-ttl-seconds: 900
    refresh-ttl-seconds: 1209600
    refresh-cookie-name: refresh_token
    cookie-secure: false
    cookie-same-site: Lax

  oauth2:
    client:
      registration:
        google:
          client-id: ${GOOGLE_CLIENT_ID}
          client-secret: ${GOOGLE_CLIENT_SECRET}
          scope: [email, profile]
        github:
          client-id: ${GITHUB_CLIENT_ID}
          client-secret: ${GITHUB_CLIENT_SECRET}
          scope: [user:email, read:user]
```

### Environment Variables

```bash
export JWT_SECRET="your-long-random-secret"
export GOOGLE_CLIENT_ID="your-google-client-id"
export GOOGLE_CLIENT_SECRET="your-google-client-secret"
export GITHUB_CLIENT_ID="your-github-client-id"
export GITHUB_CLIENT_SECRET="your-github-client-secret"
```

### Run Backend

```bash
mvn spring-boot:run
```

📍 Backend runs at: `http://localhost:8081`

---

## 💻 Frontend Setup (React + Vite)

### 🧩 Prerequisites
- Node.js 18+
- npm / yarn / pnpm

### Steps

```bash
cd frontend
npm install
```

Create `.env`

```env
VITE_BACKEND_URL=http://localhost:8081
```

Run frontend:

```bash
npm run dev
```

📍 Frontend runs at: `http://localhost:5173`

---

## 🔗 Authentication Flow

### 1️⃣ Username / Password Login
- User submits credentials
- Backend validates and hashes password
- Issues access token + refresh token
- Refresh token stored in HTTP-only cookie

### 2️⃣ OAuth2 Login (Google / GitHub)
- Redirect to provider
- Successful authentication
- Backend issues JWT tokens
- User created automatically if first login

### 3️⃣ Token Refresh
- Access token expires
- Refresh token used silently
- New access token generated
- User stays logged in

### 4️⃣ Role-Based Access
- Roles loaded from DB
- Protected endpoints using roles
- Admin-only APIs secured

### 5️⃣ Logout
- Refresh cookie cleared
- Tokens invalidated

---

## 🔑 API Endpoints

| Method | Endpoint                       | Description                     |
|------|--------------------------------|---------------------------------|
| POST | /api/auth/login                | Login with credentials          |
| POST | /api/auth/register             | Register new user               |
| POST | /api/auth/refresh              | Refresh access token            |
| POST | /api/auth/logout               | Logout user                     |
| GET  | /api/auth/me                   | Current logged-in user          |
| GET  | /oauth2/authorization/google   | Google OAuth login              |
| GET  | /oauth2/authorization/github   | GitHub OAuth login              |

---

## 📄 API Documentation (Swagger)

- Swagger UI enabled
- JWT authorization supported
- OpenAPI 3 specification

📍 Access Swagger UI:
```
http://localhost:8081/swagger-ui.html
```

---

## 🧰 Common Commands

```bash
# Backend
mvn spring-boot:run
mvn clean package
java -jar target/auth-app.jar

# Frontend
npm run dev
npm run build
```

---

## ✅ Project Highlights (Interview Ready)

- Production-grade security architecture
- Modern JWT + Refresh Token flow
- OAuth2 integration
- Role-based authorization
- Secure cookie handling
- Clean code structure
- OpenAPI documentation

---

## 📸 Application Screenshots

### 🏠 Home Page
![Home Page](src/utils/sc1.png)

### 🔐 Login Page
![Login Page](src/utils/sc2.png)

### 📝 Register Page
![Register Page](src/utils/sc3.png)

### 🌐 Google OAuth Login Flow
![Google OAuth](src/utils/sc4.png)

### 📊 Dashboard (After Login)
![Dashboard](src/utils/sc5.png)

### 🐙 GitHub OAuth Login Flow
![GitHub OAuth](src/utils/sc6.png)
