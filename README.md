﻿

# Oioi - Backend (Deno)

Welcome to the **Oioi** Backend repository! This project serves as the backend for a real-time messaging application similar to WhatsApp, built using **Deno**, **WebSockets**, and other modern web technologies. The backend handles user authentication, real-time messaging, media uploads, and more.

---

## Table of Contents

- [Oioi - Backend (Deno)](#oioi---backend-deno)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Features](#features)
  - [Tech Stack](#tech-stack)
  - [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
    - [Environment Variables](#environment-variables)
    - [Running the Application](#running-the-application)
  - [API Documentation](#api-documentation)
    - [Authentication](#authentication)
    - [User Management](#user-management)
    - [Chat Management](#chat-management)
    - [Media](#media)
  - [WebSocket Events](#websocket-events)
    - [Client-to-Server Events](#client-to-server-events)
    - [Server-to-Client Events](#server-to-client-events)
  - [Contributing](#contributing)
  - [License](#license)
  - [Contact](#contact)

---

## Overview

**Oioi** is a real-time messaging backend designed to handle user authentication, chat messaging, and media sharing for mobile applications. Built with **Deno**, it leverages modern features like WebSockets for real-time communication, JWT for secure user authentication, and MongoDB for data persistence.

---

## Features

- **Real-time Messaging**: Powered by **WebSockets** for instant communication between users.
- **User Authentication**: JWT-based authentication for secure login and session management.
- **1-on-1 and Group Chats**: Support for private messages and group conversations.
- **Media Support**: Allows users to send images, videos, and documents.
- **Push Notifications**: Integration with **Firebase Cloud Messaging (FCM)** to notify users about new messages.
- **Message Status**: Track the status of messages (sent, delivered, read).

---

## Tech Stack

- **Deno**: JavaScript and TypeScript runtime with security, modern standards, and native TypeScript support.
- **Oak**: A middleware framework for Deno, similar to Express.js, used for routing and request handling.
- **WebSockets**: For real-time, bidirectional communication between clients and the server.
- **MongoDB**: NoSQL database for storing user, chat, and message data.
- **JWT (JSON Web Tokens)**: Used for stateless, secure user authentication.
- **Firebase Cloud Messaging (FCM)**: For sending push notifications.

---

## Getting Started

### Prerequisites

To run this project, you’ll need:

- **Deno**: Ensure Deno is installed on your system. You can install it by running the following command in PowerShell (Windows):

  ```bash
  irm https://deno.land/install.ps1 | iex
  ```

  For other platforms (macOS, Linux), follow the [Deno installation guide](https://deno.land/manual/getting_started/installation).

- **MongoDB**: Either use a local MongoDB instance or a cloud-based MongoDB like **MongoDB Atlas**.

- **Firebase**: A Firebase account for managing push notifications using **Firebase Cloud Messaging (FCM)**.

### Installation

1. Clone this repository:

    ```bash
    git clone https://github.com/your-username/Oioi-backend.git
    cd Oioi-backend
    ```

2. Install Deno dependencies:

    Deno automatically handles dependencies from URLs, so you don’t need a package manager. When you run the code, Deno will fetch dependencies as needed.

### Environment Variables

Create a `.env` file in the root directory to store your environment variables. You can use the `deno-dotenv` module to load them into your application.

Here’s an example of the required environment variables:

```bash
# MongoDB connection string
MONGO_URI=mongodb://localhost:27017/oioi-db

# JWT Secret Key
JWT_SECRET=your_jwt_secret

# Firebase Cloud Messaging Key
FCM_SERVER_KEY=your_fcm_server_key

# Server Config
PORT=8000
```

### Running the Application

To start the server, run the following command:

```bash
deno run --allow-net --allow-read --allow-env --allow-write src/main.ts
```

Here’s what the permissions mean:
- **`--allow-net`**: Allows network access (needed for WebSockets and MongoDB).
- **`--allow-read`**: Allows reading files (needed for reading `.env` and media files).
- **`--allow-env`**: Allows access to environment variables.
- **`--allow-write`**: Allows writing files (e.g., media uploads).

---

## API Documentation

The Oioi backend provides a set of RESTful APIs for managing users, messages, and chats. These APIs are secured via JWT, and tokens must be provided in the `Authorization` header for protected routes.

### Authentication

- **POST** `/auth/register`: Register a new user.
- **POST** `/auth/login`: Authenticate a user and return a JWT token.

### User Management

- **GET** `/users`: Retrieve the list of users.
- **GET** `/users/:id`: Retrieve user profile information.

### Chat Management

- **GET** `/chats`: Retrieve all chats for a user.
- **POST** `/chats`: Create a new chat (1-on-1 or group).
- **GET** `/chats/:chatId/messages`: Retrieve chat messages for a specific chat.
- **POST** `/chats/:chatId/messages`: Send a message in a chat.

### Media

- **POST** `/media/upload`: Upload an image or video file to the server.

---

## WebSocket Events

**Oioi** uses WebSockets to enable real-time messaging between users. Below are the key WebSocket events supported by the server:

### Client-to-Server Events

- **`message:send`**: Sends a message to a specific chat.
  - Payload: `{ senderId, chatId, messageContent, mediaUrl }`
  
- **`typing:start`**: Notifies other users that a participant is typing.
  - Payload: `{ chatId, userId }`

- **`typing:stop`**: Notifies others when the user stops typing.
  - Payload: `{ chatId, userId }`

### Server-to-Client Events

- **`message:received`**: Delivers a new message to the recipient.
  - Payload: `{ chatId, messageContent }`
  
- **`message:delivered`**: Confirms that a message was delivered.
  - Payload: `{ messageId, chatId }`

- **`message:read`**: Indicates that a message was read.
  - Payload: `{ messageId, chatId }`

- **`user:online`**: Notifies when a user comes online.
  - Payload: `{ userId }`

- **`user:offline`**: Notifies when a user goes offline.
  - Payload: `{ userId }`

---

## Contributing

Contributions are welcome! If you’d like to contribute to this project, feel free to submit a pull request or open an issue. Please adhere to the standard code of conduct when contributing.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## Contact

For any questions or collaboration requests, feel free to contact:

- **Project Maintainer**: [Christian Bonafena](mailto:christianbonafena7@gmail.com)

---
