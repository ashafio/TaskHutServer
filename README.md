# TaskHut — Server

The backend REST API for TaskHut, a full-stack task marketplace application. Built with Node.js and Express, using MongoDB as the database, and deployed on Vercel.

> Forked from [Mahbub2027/task-hut-server](https://github.com/Mahbub2027/task-hut-server)  
> Paired with: [TaskHutClient](https://github.com/ashafio/TaskHutClient)

---

## Overview

This server handles all data operations for the TaskHut platform — task management, user data, bids/applications, and protected routes secured with JWT authentication. It exposes a RESTful API consumed by the React frontend via Axios.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Framework | Express `^4.18` |
| Database | MongoDB `^6.3` (native driver) |
| Authentication | JSON Web Tokens (`jsonwebtoken ^9`) |
| CORS | `cors ^2.8` |
| Config | `dotenv ^16.3` |
| Deployment | Vercel (Serverless) |

---

## Project Structure

```
TaskHutServer/
├── index.js        # App entry point — Express setup, DB connection, all routes
├── vercel.json     # Vercel deployment config (routes all methods to index.js)
├── .gitignore
└── package.json
```

---

## Getting Started

### Prerequisites

- Node.js (≥ 18 recommended)
- A MongoDB database (MongoDB Atlas recommended)
- npm

### Install and run locally

```bash
git clone https://github.com/ashafio/TaskHutServer.git
cd TaskHutServer
npm install
node index.js
```

The server will start on `http://localhost:5000` (or whichever port is set in your `.env`).

---

## Environment Variables

Create a `.env` file in the project root with the following:

```env
PORT=5000
DB_USER=your_mongodb_username
DB_PASS=your_mongodb_password
ACCESS_TOKEN_SECRET=your_jwt_secret
```

Never commit your `.env` file — it is already listed in `.gitignore`.

---

## API Overview

All routes are defined in `index.js`. The server supports standard CRUD operations across the following resource areas:

| Resource | Methods | Description |
|---|---|---|
| Tasks | GET, POST, PUT, PATCH, DELETE | Create, read, update, and remove tasks |
| Bids / Applications | GET, POST, PATCH, DELETE | Manage task applications from workers |
| Users | GET, POST | User profile management |
| Auth | POST | JWT token issuance for verified users |

Protected routes require a valid JWT passed in the `Authorization` header as a Bearer token.

---

## Deployment

The server is deployed on Vercel using the `@vercel/node` runtime. The `vercel.json` config routes all incoming HTTP methods to `index.js`:

```json
{
  "version": 2,
  "builds": [{ "src": "./index.js", "use": "@vercel/node" }],
  "routes": [{ "src": "/(.*)", "dest": "/", "methods": ["GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"] }]
}
```

To redeploy, push to `main` or run:

```bash
vercel --prod
```

Set all environment variables in the Vercel project dashboard under **Settings → Environment Variables**.

---

## Related Repository

The frontend client for this project: [TaskHutClient](https://github.com/ashafio/TaskHutClient)

---

## Author

**Shafi** — GitHub: [@ashafio](https://github.com/ashafio)
