# Store Rating Platform

A full-stack web application that allows users to register stores, submit and manage ratings, and administer the platform—all in one place.

## Table of Contents

1. [Tech Stack](#tech-stack)
2. [Features](#features)
3. [Prerequisites](#prerequisites)
4. [Getting Started](#getting-started)

   * [Clone the Repo](#clone-the-repo)
   * [Backend Setup](#backend-setup)
   * [Frontend Setup](#frontend-setup)
   * [Database Setup](#database-setup)
5. [Database Schema](#database-schema)
6. [Form Validations](#form-validations)
7. [Folder Structure](#folder-structure)
8. [Scripts](#scripts)
9. [Contributing](#contributing)

---

## Tech Stack

* **Backend:** Express.js (or LoopBack / NestJS)
* **Database:** PostgreSQL (or MySQL)
* **Frontend:** React.js
* **Authentication:** JWT
* **Styling:** CSS Modules or Tailwind CSS

---

## Features

### 1. System Administrator

* Create new stores, normal users, and admin users
* Dashboard with:

  * Total users, stores, and ratings
* Manage users (Name, Email, Address, Role)
* Manage stores (Name, Email, Address, Overall Rating)
* Filter & sort listings by Name, Email, Address, Role
* View detailed user profiles (Store Owners include their store rating)
* Secure logout

### 2. Normal User

* Sign up & log in
* Update password
* Browse all registered stores
* Search stores by Name & Address
* View store listings (Name, Address, Overall Rating, Your Rating)
* Submit & modify ratings (1–5)
* Secure logout

### 3. Store Owner

* Log in & update password
* Dashboard:

  * List of users who rated this store
  * Average rating of the store
* Secure logout

---

## Prerequisites

* Node.js v14+ & npm
* PostgreSQL (or MySQL) instance
* Git

---

## Getting Started

### Clone the Repo

```bash
git clone https://github.com/<your-username>/store-rating-platform.git
cd store-rating-platform
```

### Backend Setup

1. Install dependencies

   ```bash
   cd backend
   npm install
   ```
2. Configure environment variables
   Create a `.env` file with:

   ```env
   PORT=4000
   DB_HOST=localhost
   DB_PORT=5432
   DB_USER=<your-db-user>
   DB_PASS=<your-db-password>
   DB_NAME=store_ratings
   JWT_SECRET=<your-secret-key>
   ```
3. Run migrations & seed (if any)

   ```bash
   npx sequelize db:migrate
   npx sequelize db:seed:all
   ```
4. Start the server

   ```bash
   npm run dev
   ```

### Frontend Setup

1. Install dependencies

   ```bash
   cd ../frontend
   npm install
   ```
2. Configure API endpoint
   In `src/config.js`, set:

   ```js
   export const API_BASE_URL = 'http://localhost:4000/api';
   ```
3. Start the React app

   ```bash
   npm start
   ```

### Database Setup

* Create the database:

  ```sql
  CREATE DATABASE store_ratings;
  ```
* Ensure your `.env` credentials match.

---

## Database Schema

| Table       | Columns                                                                            |      |          |
| ----------- | ---------------------------------------------------------------------------------- | ---- | -------- |
| **users**   | id, name, email, password\_hash, address, role (\`admin                            | user | owner\`) |
| **stores**  | id, owner\_id (FK → users.id), name, email, address, created\_at                   |      |          |
| **ratings** | id, user\_id (FK → users.id), store\_id (FK → stores.id), score (1–5), updated\_at |      |          |

* **Relations**

  * `users (1) ↔ (M) ratings`
  * `stores (1) ↔ (M) ratings`
  * `users (1) ↔ (1) stores` (for store owners)

---

## Form Validations

* **Name:** 20–60 characters
* **Address:** max 400 characters
* **Password:** 8–16 chars, at least one uppercase letter & one special character
* **Email:** must be a valid email format

All validation errors are returned in JSON with appropriate HTTP status codes.

---

## Folder Structure

```
├── backend
│   ├── controllers
│   ├── middlewares
│   ├── models
│   ├── routes
│   ├── services
│   ├── utils
│   └── app.js
└── frontend
    ├── public
    ├── src
    │   ├── components
    │   ├── hooks
    │   ├── pages
    │   ├── services
    │   └── App.js
```

---

## Scripts

* **Backend**

  * `npm run dev` — start server in watch mode
  * `npm test` — run unit/integration tests

* **Frontend**

  * `npm start` — run React dev server
  * `npm run build` — build for production

---

## Contributing

1. Fork this repo
2. Create your feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m 'Add my feature'`)
4. Push to branch (`git push origin feature/my-feature`)
5. Open a Pull Request

Please follow code style and include tests for any new functionality.

---
