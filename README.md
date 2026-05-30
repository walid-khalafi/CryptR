# CryptR 🔐💬

> **A Secure, Zero-Knowledge, Real-Time Messaging Platform**

CryptR is a modern, mobile-friendly "Secret Chat" application inspired by the Telegram UI. It is engineered with a focus on absolute privacy, high performance, and scalable architecture. By combining the real-time power of **ASP.NET Core SignalR** with client-side **End-to-End Encryption (E2EE)**, CryptR ensures that your conversations remain entirely invisible to the server and database.

---

## 🚀 Key Features

*   **Absolute Privacy (E2EE):** Peer-to-peer End-to-End Encryption implemented on the client-side (JavaScript). The server and database only handle encrypted payloads; plaintext never touches the network.
*   **Real-Time Architecture:** Instant message delivery, typing indicators, and user presence management powered by **ASP.NET Core SignalR**.
*   **Telegram-Inspired UI:** A clean, responsive, and mobile-friendly user interface built with **Bootstrap 5**, featuring a classic dual-pane layout (chat list & active chat room).
*   **Rich Media Support:** Secure sharing of images and voice messages, optimized by uploading files via authenticated REST APIs rather than bloating the SignalR socket connection.
*   **Enterprise-Grade Foundation:** Built using **Domain-Driven Design (DDD)** and **Clean Architecture** to ensure maintainability, testability, and decoupling of core business logic.

---

## 🛠️ Tech Stack & Architecture

### Backend
*   **Framework:** .NET 9 (Web API)
*   **Real-Time:** ASP.NET Core SignalR
*   **Database ORM:** Entity Framework Core 9
*   **Database:** MySQL
*   **Design Pattern:** Mediator Pattern (using MediatR for CQRS)

### Frontend
*   **Styling & UI:** Bootstrap 5 (Responsive Layout)
*   **Client Communication:** Microsoft SignalR JavaScript Client
*   **Security:** Web Crypto API (Client-side key exchange & AES-GCM encryption)

### Architecture Layers (DDD Blueprint)
The project follows strict Clean Architecture guidelines:
*   **CryptR.Domain:** Contains core entities (`User`, `ChatRoom`, `EncryptedMessage`), value objects, and domain exceptions. Absolutely zero dependencies on external frameworks.
*   **CryptR.Application:** Implements use cases, CQRS commands/queries (via MediatR), and interface definitions for infrastructure.
*   **CryptR.Infrastructure:** Handles data persistence (EF Core, MySQL), security implementations, and external integrations.
*   **CryptR.Presentation.API:** The entry point. Manages REST Endpoints and hosts **SignalR Hubs** strictly as a delivery mechanism.

---

## 🔑 Security & E2EE Flow

CryptR operates on a **Zero-Knowledge** model:
1. **Key Exchange:** When a secret chat is initiated, clients securely exchange public keys using a Diffie-Hellman-based mechanism over SignalR.
2. **Encryption:** Messages, images, and voice metadata are encrypted in the browser using a shared symmetric key via **AES-GCM**.
3. **Transit & Storage:** The server receives only the encrypted payload (`Ciphertext`) and passes it along. MySQL stores nothing but hashes, IDs, timestamps, and encrypted blobs.

---

## 🏁 Getting Started

### Prerequisites
*   [.NET 9 SDK](https://dotnet.microsoft.com/download)
*   [MySQL Server](https://dev.mysql.com/downloads/installer/)

### Installation & Setup

1. **Clone the repository:**
```bash
   git clone [https://github.com/your-username/CryptR.git](https://github.com/your-username/CryptR.git)
   cd CryptR
```

2. **Configure the Database:**
Update the connection string in src/CryptR.Presentation.API/appsettings.json:

```bash
"ConnectionStrings": {
     "DefaultConnection": "Server=localhost;Database=cryptr_db;Uid=root;Pwd=your_password;"
   }
```

