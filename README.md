# SORTD - Problems, sorted.

An enterprise-grade complaint management and resolution tracking web application built with modern architecture, real-time audit trails, role-based workflows, and analytics.

---

## 🛠 Tech Stack

- **Frontend**: React 19 (Vite) + React Router 7 + Tailwind CSS v4 + Axios + Recharts + Lucide Icons
- **Backend**: Node.js + Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (Access Token) + bcrypt password hashing
- **Validation**: express-validator
- **File Uploads**: Multer (Images & PDFs up to 5MB)
- **Security & Reliability**: Helmet, CORS, Rate Limiting (`express-rate-limit`), Morgan logging

---

## 👥 User Roles & Access Control

| Role | Access Scope | Key Capabilities |
| :--- | :--- | :--- |
| **Complainant (User)** | Own complaints | Registers grievances with attachments, tracks real-time progress via ticket ID, reopens resolved tickets, rates resolution quality (1–5 ★). |
| **Staff** | Assigned complaints | Inspects assigned tickets, tracks SLA due dates, flags overdue items, advances status (`In Progress` ➔ `Resolved`), leaves audit remarks. |
| **Admin** | Global system | Global table with search/filters/pagination, assigns/reassigns staff, sets target due dates, creates staff accounts, manages categories, views Recharts visual analytics. |

---

## 🔑 Demo Credentials

All seeded accounts use password: `Password@123`

| Role | Email | Password | Description |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@example.com` | `Password@123` | Executive Admin (Full system oversight) |
| **Staff 1** | `staff1@example.com` | `Password@123` | Sarah Jenkins (IT & Systems Support) |
| **Staff 2** | `staff2@example.com` | `Password@123` | Mike Ross (Facilities & Safety) |
| **User 1** | `user1@example.com` | `Password@123` | Alice Johnson (Complainant) |
| **User 2** | `user2@example.com` | `Password@123` | Bob Martinez (Complainant) |
| **User 3** | `user3@example.com` | `Password@123` | Charlie Chen (Complainant) |

*Note: You can also use the 1-Click fast demo login buttons on the Login page and Landing page.*

---

## 🚀 Getting Started

### 1. Prerequisites
- Node.js (v18+)
- MongoDB running locally on `mongodb://127.0.0.1:27017` or a MongoDB Atlas URI

### 2. Environment Variables Configuration
In `server/.env`:
```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/complaint_agent_db
JWT_SECRET=super_secret_jwt_complaint_agent_key_2026_xyz
CLIENT_URL=http://localhost:5173
EMAIL_HOST=
EMAIL_PORT=587
EMAIL_USER=
EMAIL_PASS=
EMAIL_FROM=Complaint System <no-reply@complaint.local>
```

### 3. Install Dependencies & Seed Database
From the root project directory:
```bash
# Install Server dependencies
cd server
npm install

# Run database seed script (creates admin, staff, users, categories & complaints)
npm run seed

# Install Client dependencies
cd ../client
npm install
```

### 4. Run the Application
In separate terminal windows:
```bash
# Terminal 1: Backend Server (Port 5000)
cd server
npm start

# Terminal 2: Frontend Client (Port 5173)
cd client
npm run dev
```

Open your browser at `http://localhost:5173`.

---

## 📡 REST API Reference (`/api`)

### Authentication (`/api/auth`)
- `POST /api/auth/register` - Register a new Complainant user
- `POST /api/auth/login` - Authenticate and obtain JWT token
- `GET /api/auth/me` - Get profile of authenticated user
- `POST /api/auth/create-staff` - (Admin) Create staff member account

### Complaints (`/api/complaints`)
- `GET /api/complaints` - List complaints (scoped by role with search, status, category, priority, date filters & pagination)
- `POST /api/complaints` - Submit new complaint with Multer file attachments (Max 5MB)
- `GET /api/complaints/:id` - Fetch complaint details with populated timeline history
- `GET /api/complaints/track/:complaintId` - Public tracking endpoint by ID (e.g. `CMP-2026-0001`)
- `PUT /api/complaints/:id/assign` - (Admin) Assign or reassign complaint to staff with SLA due date
- `PUT /api/complaints/:id/status` - Update status (`Submitted` ➔ `Assigned` ➔ `In Progress` ➔ `Resolved` ➔ `Closed` / `Reopened`)
- `POST /api/complaints/:id/comments` - Post comment / remark to complaint timeline
- `POST /api/complaints/:id/feedback` - (Complainant) Submit 1-5 star rating & review comment

### Administration (`/api/users` & `/api/categories`)
- `GET /api/users` - (Admin) List users with role filter & pagination
- `GET /api/users/staff` - Active staff members list for assignment dropdown
- `POST /api/users` - (Admin) Create staff or admin account
- `PUT /api/users/:id` - (Admin) Toggle active state or update profile
- `GET /api/categories` - List active grievance categories
- `POST /api/categories` - (Admin) Create new category
- `PUT /api/categories/:id` - (Admin) Update category
- `DELETE /api/categories/:id` - (Admin) Delete category

### Analytics & Notifications (`/api/dashboard` & `/api/notifications`)
- `GET /api/dashboard/stats` - Role-tailored metrics and aggregation data for Recharts
- `GET /api/notifications` - Get user activity notifications
- `PUT /api/notifications/:id/read` - Mark single notification as read
- `PUT /api/notifications/read-all` - Mark all notifications as read

---

## 🎨 Design & UX Highlights

- **Visual Transparency**: Formatted IDs (`CMP-2026-0001`) with copy-to-clipboard button and immediate tracking confirmation.
- **Audit Timelines**: Vertical animated timeline detailing every actor, department, status movement, timestamp, and remark.
- **Executive Analytics**: Recharts bar charts, pie charts, and workload distribution metrics for operations management.
- **Glassmorphism & Micro-animations**: Modern UI built with Tailwind CSS, clear error states, and responsive navigation drawer on mobile.
