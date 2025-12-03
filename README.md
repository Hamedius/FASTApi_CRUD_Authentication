# FASTApi_CRUD_Authentication

A secure backend API built with **FastAPI**, demonstrating:

- User registration & login with JWT authentication
- Token-based authorization using OAuth2 Password Flow
- CRUD operations for users & products
- Secure endpoints that require valid JWT tokens
- Clean, modular project architecture (routers, repository layer, schemas, models)

This repository is intended as a practical template for building **production-ready FastAPI backends with authentication**.

---

## 🔐 Key Features

### **🔑 JWT Authentication**
- Login endpoint returns a **JWT access token**
- Expiration handled through token payload
- Secure routes require `Authorization: Bearer <token>`
- Passwords hashed using industry-standard algorithms (`hashing.py`)

### **👥 User Management**
- Register new users
- Login to receive token
- Fetch user data
- All password handling follows best practices (never stored as plain text)

### **📦 CRUD Operations**
#### Products
- Create new product
- Get single product
- List all products  
All product routes are **protected** and require authentication.

#### Users
- Create new users
- Get user list
- Get user by ID

### **🧱 Clean Architecture**
- `routers/` → API routing layer  
- `repository/` → business/database logic  
- `database.py` → SQLAlchemy session & engine  
- `models.py` → ORM definitions  
- `schemas.py` → Pydantic request/response models  
- `oauth2.py` → token generation + authentication helpers  
- `hashing.py` → password hashing utilities  

---

## 📁 Project structure

```text
FASTApi_CRUD_Authentication/
├─ README.md
├─ requirement.txt
└─ user/
    ├─ __init__.py
    ├─ database.py
    ├─ hashing.py
    ├─ main.py
    ├─ models.py
    ├─ oauth2.py
    ├─ repository/
    │   ├─ products.py
    │   └─ users.py
    ├─ routers/
    │   ├─ __init__.py
    │   ├─ authentication.py
    │   ├─ products.py
    │   └─ users.py
    ├─ schemas.py
    └─ token.py

This structure mirrors real-world FastAPI production apps.

⸻

⚙️ Installation

1. Clone the repository

git clone https://github.com/Hamedius/FASTApi_CRUD_Authentication.git
cd FASTApi_CRUD_Authentication

2. Create and activate virtual environment

python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

3. Install dependencies

pip install -r requirement.txt


⸻

🗄️ Database Configuration

Default DB: SQLite

You don’t need to do anything — DB file is created automatically.

To switch to PostgreSQL/MySQL, edit:

user/database.py

and replace the SQLALCHEMY connection string.

⸻

▶️ Running the App

Run with Uvicorn:

uvicorn user.main:app --reload

Open the interactive API docs:
	•	Swagger UI → http://127.0.0.1:8000/docs
	•	ReDoc → http://127.0.0.1:8000/redoc

⸻

🔐 Authentication Flow (How Login Works)

1️⃣ Register new user

POST /users/

Request body:

{
  "name": "hamed",
  "email": "hamed@example.com",
  "password": "1234"
}

2️⃣ Login

POST /login

If credentials are correct, the response contains a JWT:

{
  "access_token": "xxxxx.yyyyy.zzzzz",
  "token_type": "bearer"
}

3️⃣ Call protected endpoint

Send the token in the header:

Authorization: Bearer <access_token>

Example protected request:

curl -X GET "http://127.0.0.1:8000/product/" \
     -H "Authorization: Bearer <token>"


⸻

🧠 Token Internals (JWT)

Your tokens contain:
	•	user_id
	•	expiration time
	•	issued_at
	•	signed using a secret key in oauth2.py

Validation is handled automatically through FastAPI Depends().

⸻

💼 Example Endpoints

Users
	•	POST /users/ → create user
	•	GET /users/ → list users
	•	GET /users/{id} → get user

Auth
	•	POST /login → generate JWT
	•	GET /current-user → get authenticated user

Products (Protected)
	•	POST /product/
	•	GET /product/
	•	GET /product/{id}

⸻

🧱 Code Architecture Overview
	•	main.py → FastAPI app
	•	routers/ → API endpoints
	•	repository/ → business logic
	•	models.py → SQLAlchemy ORM
	•	schemas.py → Pydantic models
	•	oauth2.py → JWT + password flow
	•	hashing.py → bcrypt/sha256 password hashing

⸻

📌 Future Enhancements
	•	Add refresh tokens
	•	Add email verification
	•	Add role-based permissions (Admin/User)
	•	Add async SQLAlchemy engine
	•	Add unit tests (pytest + TestClient)
	•	Dockerize for deployment
	•	Deploy on Render / Fly.io
	•	Add rate limiting

⸻

👤 Author

Hamed Nahvi
GitHub: @Hamedius
