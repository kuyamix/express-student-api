<div align="center">

# 🎓 Student Directory API

### A RESTful API built with **Express**, **Mongoose**, and **MongoDB Atlas**

[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=for-the-badge&logo=mongoose&logoColor=white)](https://mongoosejs.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

A production-ready Student Directory API refactored from in-memory arrays to a persistent MongoDB database using Mongoose ODM.

[Features](#-features) • [Tech Stack](#-tech-stack) • [Getting Started](#-getting-started) • [API Endpoints](#-api-endpoints) • [Project Structure](#-project-structure)

</div>

---

## ✨ Features

- 🗄️ **Persistent Storage** — Data stored in MongoDB Atlas (cloud)
- 🔐 **Secure Configuration** — Credentials managed via `.env` and `dotenv`
- ✅ **Schema Validation** — Mongoose enforces data consistency
- ⚡ **Async/Await** — Clean, modern non-blocking code
- 🛡️ **Error Handling** — Proper HTTP status codes (200, 201, 400, 404, 500)
- 📦 **Modular Structure** — Separated models, routes, and server config
- 🌐 **RESTful Design** — Full CRUD operations

---

## 🧰 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Runtime** | [Node.js](https://nodejs.org/) |
| **Framework** | [Express.js](https://expressjs.com/) |
| **Database** | [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) |
| **ODM** | [Mongoose](https://mongoosejs.com/) |
| **Config** | [dotenv](https://www.npmjs.com/package/dotenv) |
| **Testing** | [Thunder Client](https://www.thunderclient.com/) / [Postman](https://www.postman.com/) |

---

## 🚀 Getting Started

### 📋 Prerequisites

Make sure you have the following installed:

- [Node.js](https://nodejs.org/) (v18 or later)
- [npm](https://www.npmjs.com/)
- A [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register) account (free tier)

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/express-student-api.git
cd express-student-api
```

### 2️⃣ Install Dependencies

```bash
npm install
```

### 3️⃣ Set Up MongoDB Atlas

1. Create a free **M0** cluster at [cloud.mongodb.com](https://cloud.mongodb.com)
2. Create a database user (Database Access → Add New Database User)
3. Whitelist your IP (Network Access → Add IP Address → `0.0.0.0/0` for dev)
4. Copy the connection string from **Connect → Drivers**

### 4️⃣ Configure Environment Variables

Create a `.env` file in the project root:

```env
MONGO_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/student_directory?retryWrites=true&w=majority
PORT=3000
```

> ⚠️ **Never commit `.env` to GitHub.** It's already listed in `.gitignore`.

### 5️⃣ Run the Server

**Development mode** (with nodemon):
```bash
npm run dev
```

**Production mode:**
```bash
npm start
```

Expected output:
```
◇ injected env (2) from .env
Server running on port 3000
MongoDB connected successfully
```

---

## 📡 API Endpoints

Base URL: `http://localhost:3000`

| Method | Endpoint | Description | Body |
|--------|----------|-------------|------|
| `GET` | `/students` | Fetch all students | — |
| `POST` | `/students` | Create a new student | `{ name, email, age, isActive }` |
| `PUT` | `/students/:id` | Update a student by ID | `{ age }` *(any fields)* |
| `DELETE` | `/students/:id` | Delete a student by ID | — |

### 📥 Request Body Schema

```json
{
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "age": 22,
  "isActive": true
}
```

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| `name` | String | ✅ | — |
| `email` | String | ✅ | Must be unique |
| `age` | Number | ❌ | — |
| `isActive` | Boolean | ❌ | — |

---

## 🧪 Example Requests

### ➕ Create a Student

```bash
curl -X POST http://localhost:3000/students \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice Johnson","email":"alice@example.com","age":22,"isActive":true}'
```

**Response `201 Created`:**

```json
{
  "_id": "674a1b2c3d4e5f6a7b8c9d0e",
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "age": 22,
  "isActive": true,
  "__v": 0
}
```

### 📖 Get All Students

```bash
curl http://localhost:3000/students
```

**Response `200 OK`:**

```json
[
  {
    "_id": "674a1b2c3d4e5f6a7b8c9d0e",
    "name": "Alice Johnson",
    "email": "alice@example.com",
    "age": 22,
    "isActive": true
  }
]
```

### ✏️ Update a Student

```bash
curl -X PUT http://localhost:3000/students/674a1b2c3d4e5f6a7b8c9d0e \
  -H "Content-Type: application/json" \
  -d '{"age":23}'
```

**Response `200 OK`:**

```json
{
  "_id": "674a1b2c3d4e5f6a7b8c9d0e",
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "age": 23,
  "isActive": true
}
```

### 🗑️ Delete a Student

```bash
curl -X DELETE http://localhost:3000/students/674a1b2c3d4e5f6a7b8c9d0e
```

**Response `200 OK`:**

```json
{
  "message": "Student deleted successfully",
  "deletedStudent": {
    "_id": "674a1b2c3d4e5f6a7b8c9d0e",
    "name": "Alice Johnson",
    "email": "alice@example.com",
    "age": 23,
    "isActive": true
  }
}
```

---

## 📁 Project Structure

```
express-student-api/
├── 📂 models/
│   └── 📄 Student.js          # Mongoose schema & model
├── 📂 routes/
│   └── 📄 students.js         # CRUD route handlers
├── 📂 node_modules/           # Dependencies (gitignored)
├── 📄 .env                    # Environment variables (gitignored)
├── 📄 .gitignore              # Git exclusions
├── 📄 package.json            # Project metadata & scripts
├── 📄 package-lock.json       # Locked dependency versions
├── 📄 server.js               # Express app + DB connection
└── 📄 README.md               # You are here 📍
```

---

## 🔄 Refactor Summary

| Operation | Before (Array) | After (Mongoose) |
|-----------|---------------|------------------|
| **Read all** | `res.json(studentsArray)` | `await Student.find()` |
| **Create** | `array.push(req.body)` | `await Student.create(req.body)` |
| **Update** | `students[index] = req.body` | `await Student.findByIdAndUpdate(id, body, { new: true, runValidators: true })` |
| **Delete** | `array.splice(index, 1)` | `await Student.findByIdAndDelete(id)` |

---

## 🛡️ Error Responses

| Status | Meaning | Example |
|--------|---------|---------|
| `400` | Bad Request | Invalid body or validation failed |
| `404` | Not Found | Student ID doesn't exist |
| `500` | Server Error | Database connection issue |

**Example error:**

```json
{ "error": "Student not found" }
```

---

## 🔒 Security Notes

- ✅ Credentials stored in `.env` — never hardcoded
- ✅ `.env` listed in `.gitignore`
- ✅ Mongoose schema validation prevents malformed data
- ✅ Unique index on `email` prevents duplicates

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!  
Feel free to check the [issues page](https://github.com/YOUR-USERNAME/express-student-api/issues).

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

## 👤 Author

**Your Name**

- GitHub: [@YOUR-USERNAME](https://github.com/YOUR-USERNAME)
- Email: your.email@example.com

---

## 🙏 Acknowledgments

- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) for free cloud hosting
- [Mongoose Docs](https://mongoosejs.com/docs/) for excellent documentation
- [Express.js](https://expressjs.com/) for the minimal web framework
- [Shields.io](https://shields.io/) for the badges

---

<div align="center">

### ⭐ If this project helped you, consider giving it a star!

Made with ❤️ and ☕ by [Your Name](https://github.com/YOUR-USERNAME)

</div>
