# Estate API Setup Guide

This is the backend API for the Full-Stack Estate application. It is built using Node.js, Express, and Prisma with MongoDB as the database.

## Prerequisites

Before starting, ensure you have the following installed on your machine:
- [Node.js](https://nodejs.org/) (v16.x or higher recommended)
- [npm](https://www.npmjs.com/) (normally bundled with Node.js)
- A [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account or a local MongoDB instance running.

---

## Setup Instructions

Follow these step-by-step instructions to get the API running locally:

### 1. Navigate to the API Directory
From the root of the project, change your directory to the `api` folder:
```bash
cd full-stack-estate/api
```

### 2. Install Dependencies
Install all the required npm packages:
```bash
npm install
```

### 3. Configure Environment Variables
Create a file named `.env` in the root of the `api` folder:
```bash
# On Linux/macOS:
touch .env

# On Windows (PowerShell):
New-Item .env
```

Open the `.env` file and populate it with the following environment variables:

```env
# Connection string for your MongoDB database (replace with your credentials)
DATABASE_URL="mongodb+srv://<username>:<password>@cluster0.mongodb.net/estate?retryWrites=true&w=majority"

# A secure secret key used to sign and verify JSON Web Tokens (JWT)
JWT_SECRET_KEY="your_jwt_secret_key_here"

# The URL of the client application (used to configure CORS)
CLIENT_URL="http://localhost:5173"
```

> [!NOTE]
> Make sure to replace `<username>`, `<password>`, and `cluster0.mongodb.net` in the `DATABASE_URL` with your actual MongoDB Atlas connection details.

### 4. Database Setup & Prisma Client Generation
This project uses **Prisma ORM** to interact with MongoDB. You need to generate the Prisma client and sync the schema with your database.

1. **Generate Prisma Client:**
   ```bash
   npx prisma generate
   ```

2. **Push the Schema to MongoDB:**
   ```bash
   npx prisma db push
   ```
   *This command creates the collections and index structures defined in [schema.prisma](file:///f:/EsayEstate2026/full-stack-estate/api/prisma/schema.prisma) in your MongoDB database.*

### 5. Start the Server
Start the Express API server by running:
```bash
node app.js
```

The server should start successfully and display:
```
Server is running!
```
By default, the server runs on port `8800`. You can access it at `http://localhost:8800`.

---

## Project Structure & API Endpoints

- **Entry Point:** [app.js](file:///f:/EsayEstate2026/full-stack-estate/api/app.js)
- **Database Schema:** [schema.prisma](file:///f:/EsayEstate2026/full-stack-estate/api/prisma/schema.prisma)

### Route Prefixes
- **Authentication:** `/api/auth` (Register, Login, Logout)
- **Users:** `/api/users` (Profile updates, fetching users, saving posts)
- **Posts:** `/api/posts` (Property listings - CRUD)
- **Chats:** `/api/chats` (Private user chats)
- **Messages:** `/api/messages` (Chat messages)
- **Testing:** `/api/test` (Authentication tests)
