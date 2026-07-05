<div align="center">
  <img src="https://placehold.co/120x120/12121a/ff6b35?text=Y" alt="Yooperlanka Logo" width="80" height="80" style="border-radius: 12px; margin-bottom: 15px;" />
  <h1 align="center">Yooperlanka</h1>
  <p align="center">
    <strong>A Premium E-Commerce Platform for Yooperlite & Rare Gems</strong>
  </p>
  
  <p align="center">
    <a href="#features">Features</a> •
    <a href="#tech-stack">Tech Stack</a> •
    <a href="#authentication-system">Auth System</a> •
    <a href="#installation">Installation</a> •
    <a href="#admin-dashboard">Admin Dashboard</a>
  </p>
</div>

---

## 🌟 Overview

**Yooperlanka** is a modern, high-performance full-stack e-commerce application tailored for the sale of rare mineral specimens, specifically Yooperlite. The platform offers a sleek, dark-mode aesthetic with fluid micro-animations, a seamless shopping cart experience, multi-currency support, and a highly secure, self-hosted authentication system.

The application is split into two robust layers:
- **Frontend (Client)**: A dynamic React single-page application built with Vite, utilizing modern React hooks and Context for state management.
- **Backend (Server)**: A fast, scalable Express.js REST API handling product catalogs, order processing, secure authentication, and system health diagnostics.

---

## ✨ Features

- **Dynamic Product Catalog**: Browse specimens by category (Gems, Crystal, Jewelry, Yooperlite).
- **Multi-Currency Support**: Instantly toggle pricing between USD and LKR.
- **Shopping Cart & Checkout**: Persistent cart state with a streamlined checkout flow (Stripe/WhatsApp integration ready).
- **Secure Authentication**: Custom JWT-based auth with HTTP-only refresh tokens, bcrypt password hashing, and brute-force protection.
- **Password Recovery**: Secure, time-limited token generation delivered via email (Nodemailer).
- **Admin Dashboard**: Comprehensive control panel to manage products, track orders, monitor system health, and manage user roles.
- **Responsive Design**: Flawless experience across desktop, tablet, and mobile devices.

---

## 🛠 Tech Stack

### Frontend (Client)
- **Framework**: React 18 (Vite)
- **Routing**: React Router DOM v6
- **State Management**: React Context API
- **Styling**: Vanilla CSS (CSS Modules & Global Variables)
- **Icons**: Lucide React
- **HTTP Client**: Axios (with custom interceptors for JWT rotation)

### Backend (Server)
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database (Auth/Identity)**: Supabase PostgreSQL (via standard SQL/REST)
- **Database (Products/Orders)**: MongoDB (Mongoose)
- **Authentication**: JWT (JSON Web Tokens), bcryptjs
- **Security**: express-rate-limit, express-validator, cookie-parser
- **Email Service**: Nodemailer

---

## 🔐 Authentication System

Yooperlanka has migrated from external OAuth providers to a professional, self-hosted authentication infrastructure to ensure maximum data privacy and security control.

**Security Highlights:**
- **Dual-Token Architecture**: Short-lived Access Tokens (memory) and Long-lived Refresh Tokens (`httpOnly`, `sameSite: strict` cookies).
- **Brute-Force Protection**: IP-based rate limiting on all `/api/auth/*` routes.
- **Account Lockout**: Automatically locks accounts for 15 minutes after 5 consecutive failed login attempts.
- **Input Sanitization**: All incoming requests are strictly validated using `express-validator` to prevent injection attacks.
- **Secure Password Reset**: Generates SHA-256 hashed, time-limited (1-hour) recovery tokens.

---

## 💻 Installation & Setup

Follow these instructions to set up the project locally for development.

### Prerequisites
- Node.js (v16 or higher)
- MongoDB (Local or Atlas URL)
- Supabase Account (for PostgreSQL users table)

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/yooperlanka.git
cd yooperlanka
```

### 2. Backend Setup
Navigate to the server directory and install dependencies:
```bash
cd server
npm install
```

Create a `.env` file in the `server` directory:
```env
PORT=5000
MONGODB_URI=your_mongodb_connection_string
SUPABASE_URL=your_supabase_project_url
SUPABASE_ANON_KEY=your_supabase_anon_key

JWT_SECRET=your_super_secret_jwt_key
JWT_REFRESH_SECRET=your_super_secret_refresh_key
JWT_EXPIRES_IN=15m
JWT_REFRESH_EXPIRES_IN=7d

CLIENT_URL=http://localhost:5173

# Email Settings (for password recovery)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_specific_password
```

Run the database migration in your Supabase SQL editor:
Copy the contents of `server/migrations/create_users_table.sql` and execute it in Supabase to create the required authentication tables.

Start the development server:
```bash
npm run dev
```

### 3. Frontend Setup
Open a new terminal, navigate to the client directory, and install dependencies:
```bash
cd client
npm install
```

Create a `.env` file in the `client` directory (if needed):
```env
VITE_API_URL=http://localhost:5000/api
```

Start the Vite development server:
```bash
npm run dev
```

---

## 🛡️ Admin Dashboard

The Admin Dashboard is a protected route (`/admin`) accessible only to users with the `admin` role. 

### Accessing the Dashboard for the First Time
Since the hardcoded admin bypass has been removed for security, you must manually promote your first user to an admin via Supabase.

1. Register an account normally via the `/register` page.
2. Go to your Supabase SQL Editor and run the following command to promote your account:
```sql
UPDATE users SET role = 'admin' WHERE email = 'your_email@example.com';
```
3. Log out and log back in. The "Admin Panel" option will now appear in your profile dropdown.

### Dashboard Capabilities
- **Reports Overview**: High-level metrics, revenue tracking (USD/LKR), and categorical sales charts.
- **Product Management**: Full CRUD capabilities for the specimen catalog, including local image uploading.
- **Order Tracking**: Update fulfillment statuses (Pending, Confirmed, Shipped, Delivered, Cancelled) and view customer details.
- **User Control Panel**: Manage registered users, promote/demote roles, or ban/delete accounts.
- **System Diagnostics**: Real-time API latency tracking, database connection health, and server memory monitoring.

---

<div align="center">
  <p>Built with ❤️ by the Serendibware Team.</p>
</div>
