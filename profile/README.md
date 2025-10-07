# Kaarmic Journey - Astrology & Hypnotherapy Platform (Enterprise-Grade)

A fully **Dockerized, Kubernetes-ready, and highly scalable web application** for kaarmicjourney.com, an astrology and clinical hypnotherapy platform. The platform supports secure user profiles, administrative content, and seamless multi-channel communication, including a critical **Multi-Channel Messaging Service** to synchronize secure in-app chat with **WhatsApp Business Chat**.

## 1. Architecture & Tech Stack (Enterprise-Grade)

The architecture is designed for security, massive scalability, and complex multi-channel operations.

| Component | Technology | Role & Responsibility |
| :--- | :--- | :--- |
| **Frontend** | **React** (Functional Components, Tailwind CSS) | Responsive UI, state management, and consumer of both REST (APIs) and WebSocket (Chat). |
| **Backend** | **Java (Spring Boot 3+)** | Core business logic, security, payments, and the **central Multi-Channel Messaging Service**. |
| **Database** | **MongoDB Atlas** | Primary database for profiles, bookings, chat logs, and content (configured as a Replica Set for HA). |
| **Containerization** | **Docker** & **Docker Compose** (Dev) | Local development and container image building. |
| **Orchestration** | **Kubernetes (K8s) & AWS ECS/DigitalOcean** | Orchestration for production scaling and high availability (HA). |
| **Messaging** | **WhatsApp Business API** | Integrated via the Java backend for two-way chat synchronization. |
| **Security** | **Spring Security** | Enforces JWT authentication, input validation, and best practices. |

---

## 2. Core Features

The platform supports all original features while adding complex multi-channel communication and secure asset retrieval.

* **User Authentication & Authorization**: Secure JWT authentication enforced by Spring Security. Primary login is **Google OAuth 2.0**.
* **Booking System**: Service-tiered forms for scheduling consultations and secure payment initiation. Requires client profile (including **WhatsApp number**) before booking is finalized.
* **Payments**: Integrated support for **Stripe** and **Razorpay** webhook verification in the Java backend.
* **Multi-Channel Messaging Service (CRITICAL)**: Real-time, synchronized chat between the consultant (in-app) and the customer (via In-App Messenger or their personal WhatsApp).
* **Content Management**: Public-facing Community **Blog management** and private Admin Contributions.
* **Secure Assets**: Ability for customers to retrieve post-session recordings/reports via secure integration with the **Google Workspace Drive API**.
* **Scalability & Security**: Designed for horizontal scaling of all components; enforced by Spring Security, JWT, HTTPS, and MongoDB security best practices.

---

## 3. Backend API Endpoints (Java/Spring Boot API)

The API is centralized in the Java backend, covering all business logic and multi-channel synchronization.

### Authentication & Profile Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Register a new user |
| `POST` | `/api/auth/login` | Login user (Handles both direct login and OAuth callback) |
| `GET` | `/api/auth/me` | Get current user profile |
| `POST` | `/api/auth/logout` | Logout user |
| `GET/PATCH` | `/api/profile/{userId}` | Get/Update secure client profile data (incl. WhatsApp contact number). |

### Booking & Appointments Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/bookings` | Get all bookings (admin only) |
| `GET` | `/api/bookings/my-bookings` | Get user bookings |
| `POST` | `/api/bookings` | Create a new booking |
| `PATCH` | `/api/bookings/:id/status` | Update booking status |
| `GET` | `/api/bookings/available-slots` | Get available time slots |

### Messaging Service (Multi-Channel Synchronization)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/chat/history/{appointmentId}` | Retrieve all synchronized messages (In-App + WhatsApp). |
| `POST` | `/api/chat/send` | Receives message from in-app UI and routes to the appropriate customer channel. |
| `POST` | **`/api/messaging/whatsapp/inbound`** | **Public Webhook:** Receives messages and status updates from the WhatsApp Business API. |

### Blog Endpoints (Admin & Public)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/blog` | Get all published blog posts |
| `GET` | `/api/blog/:slug` | Get a single blog post by slug |
| `POST` | `/api/blog` | Create a new blog post (admin only) |
| `PUT` | `/api/blog/:id` | Update a blog post (admin only) |
| `DELETE` | `/api/blog/:id` | Delete a blog post (admin only) |

### Payment Endpoints & Assets

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/payments/create-payment-intent` | Create a payment intent (Stripe/Razorpay) |
| `POST` | `/api/payments/webhook` | Receives and verifies payment confirmation/failure. |
| `GET` | `/api/payments/history` | Get payment history for user |
| `GET` | `/api/recordings/{userId}` | Fetches secure links/metadata for Google Drive session recordings. |

---

## 4. Getting Started & Development

### Prerequisites

* **Docker** and **Docker Compose** installed
* **Java** (for Spring Boot Backend) and **Node.js/npm** (for React Frontend) for local development

### Local Development Flow

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/ankur-agarwal-38aa6766/kaarmicJourney.git
    cd kaarmicjourney
    ```
2.  **Create Backend Environment File**:
    Copy the backend example file to create your local backend configuration.
    ```bash
    cp backend/.env.example backend/.env
    ```
3.  **Create Frontend Environment File**:
    Copy the frontend example file. Note the `.local` suffix, which is standard for Next.js to prevent committing secrets.
    ```bash
    cp frontend/.env.example frontend/.env.local
    ```
4.  **Update Environment Variables**:
    Open both `backend/.env` and `frontend/.env.local` and fill in your actual credentials (e.g., Google Client ID, Stripe keys, JWT secret, etc.).

5.  **Start the application** using Docker Compose:
    This command will start the frontend, backend, and MongoDB services.
    ```bash
    docker-compose up --build
    ```

### Access Points

* **Frontend**: `http://localhost:3000`
* **Backend API (Java/Spring Boot)**: `http://localhost:8080`
* **MongoDB**: `mongodb://localhost:27017`

### Development

#### Frontend - The frontend is built with Next.js and includes:
- Authentication flows
- Booking interface
- Blog display
- Payment integration

#### Backend - The backend API provides endpoints for:
- User management
- Booking management
- Blog management
- Payment processing

### Production Deployment

The application is containerized and prepared for deployment to large-scale orchestration platforms.

* **Kubernetes (K8s)**: Requires generating Deployment, Service, and Ingress YAML manifests.
* **AWS ECS/DigitalOcean**: Requires ECR/Registry setup, image push, and configuration of task definitions, services, and load balancing.
---
