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
