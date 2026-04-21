<div align="center">

# Streamline ERP

**A modern, full-stack Enterprise Resource Planning system built with the MERN stack**

[![React](https://img.shields.io/badge/React-18.3.1-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Vite](https://img.shields.io/badge/Vite-5.4.0-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![MUI](https://img.shields.io/badge/MUI-v6-007FFF?style=for-the-badge&logo=mui&logoColor=white)](https://mui.com/)

Streamline is a comprehensive, multi-tenant ERP solution that centralizes business operations — inventory, orders, customers, warehouses, sales, support tickets, and financial reconciliation — into a single, unified platform.

[Features](#features) · [Quick Start](#quick-start) · [Installation](#installation) · [API Reference](#api-reference) · [Deployment](#deployment)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Quick Start](#quick-start)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [API Reference](#api-reference)
- [Database Models](#database-models)
- [Frontend Routes](#frontend-routes)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [Contact](#contact)

---

## Overview

Streamline is designed for businesses that need a centralized system to manage day-to-day operations. It supports **multiple tenants**, enforces **role-based access control**, and provides **real-time dashboards** so teams stay aligned across departments.

| Module | What it does |
|---|---|
| **Dashboard** | Live KPI cards — users, orders, tickets, warehouses |
| **Inventory** | Product catalog, stock levels, bulk edits, CSV import/export |
| **Orders** | Full order lifecycle with email notifications |
| **Customers** | Customer profiles, credit limits, contact history |
| **Warehouses** | Capacity tracking and stock utilization |
| **Sales** | Sales pipeline from order to payment |
| **Tickets** | Support ticketing with priority, assignment, and audit trail |
| **Reconciliation** | Monthly/yearly financial income & expense reconciliation |

---

## Features

### Authentication & Access Control

- JWT-based authentication with persistent sessions via `localStorage`
- Password hashing with `bcryptjs`
- Multi-tenant login — users select their organization at login
- Role-based access: `admin`, `manager`, `sales`, `user`
- User statuses: `active`, `inactive`, `suspended`
- Auto-logout on token expiration with fully protected routes

### Dashboard

- Real-time metrics: total users, orders, customers, warehouses, and tickets
- Warehouse summary cards showing capacity and current stock
- Fast aggregation via a dedicated dashboard API endpoint

### Inventory Management

- Full product catalog with category, make, description, cost, and price
- Supplier and warehouse associations per item
- Stock status tracking: `in stock`, `out of stock`, `discontinued`
- Expiry date support for perishable items
- **Bulk edit** — update multiple records in a single action
- Advanced search and column-level filtering with server-side pagination
- **CSV import/export** powered by PapaParse
- **PDF report generation** via `html2canvas` and `jsPDF`

### Order Management

- Create orders linked to customers with full line-item detail
- Order statuses: `pending`, `shipped`, `delivered`, `cancelled`
- Payment methods: Credit Card, PayPal, Cash on Delivery
- Payment statuses: `paid`, `unpaid`, `pending`
- Tax, shipping, and net amount calculations
- Separate shipping and billing address fields
- **Automated email notifications** triggered on every order status change
- Per-order detail page with complete change history
- Pagination and status-based filtering

### Customer Management

- Customer profiles for both `individual` and `corporate` types
- Full contact and address information
- Credit limit and outstanding balance tracking
- Internal notes per customer record
- Create, edit, and delete operations with paginated list view

### Warehouse Management

- Multiple warehouse support with unique warehouse IDs
- Location, capacity, and current stock level tracking
- Manager assignment linked to a user record
- Status flags: `active` / `inactive`
- Referenced in inventory item assignments

### Sales Tracking

- Sales order list tied to customer data
- Item-level breakdown (product, quantity, unit price, line total)
- Payment and order status per sale
- Paginated table with customer name resolution

### Ticket & Incident Management

- Submit support tickets from the Raise Ticket page
- Issue types: Bug, Billing, Feature Request, UI Issues, Performance, Other
- Departments: Support, Sales, Billing, Technical, Other
- Priority levels: `low`, `medium`, `high`, `critical`
- Statuses: `open`, `in progress`, `resolved`, `closed`
- Assign tickets to any active user in the tenant
- Full **audit trail** — every status change, assignment, or edit is recorded with timestamp and actor
- **Automated email notifications** on ticket creation
- Dedicated incident detail page with chronological change history

### Financial Reconciliation

- Monthly and yearly reconciliation records
- Total income, total expenses, and reconciled total per period
- Filter by specific month and year
- Created-by / updated-by tracking for auditability
- Paginated list view

### User & Profile Management

- User list with search, role filter, and status filter
- Admin can view all users across the tenant
- Profile page with picture upload (stored server-side via Multer)
- Last login timestamp tracked per user

---

## Tech Stack

### Frontend

| Technology | Version | Purpose |
|---|---|---|
| React | 18.3.1 | UI framework |
| Vite | 5.4.0 | Build tool & dev server |
| Material-UI (MUI) | v6.1.1 | Component library |
| MUI X Data Grid | v7 | Paginated data tables |
| MUI X Charts | v7 | Dashboard visualizations |
| React Router DOM | 6.26.0 | Client-side routing |
| Axios | 1.7.3 | HTTP client |
| jwt-decode | — | Decode JWT tokens client-side |
| PapaParse | — | CSV parsing and export |
| html2canvas + jsPDF | — | PDF report generation |
| date-fns | — | Date formatting utilities |
| Emotion / Styled Components | — | CSS-in-JS styling |

### Backend

| Technology | Version | Purpose |
|---|---|---|
| Node.js + Express | 4.19.2 | REST API server |
| MongoDB + Mongoose | 8.5.2 | Database & ODM |
| jsonwebtoken | 9.0.2 | JWT generation & verification |
| bcryptjs | 2.4.3 | Password hashing |
| Multer | 1.4.5-lts | Profile picture file uploads |
| Nodemailer | 6.9.15 | Transactional email via Gmail |
| CORS | 2.8.5 | Cross-origin request handling |
| dotenv | 16.4.5 | Environment variable management |
| Nodemon | 3.1.4 | Hot-reload during development |

### Infrastructure

| Service | Role |
|---|---|
| MongoDB Atlas | Cloud-hosted database |
| Render.com | Backend API hosting |
| Netlify | Frontend static hosting |

---

## Project Structure

```
Streamline-main/
├── client/                         # React frontend (Vite)
│   ├── src/
│   │   ├── pages/                  # One component per route
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   ├── Profile.jsx
│   │   │   ├── Users.jsx
│   │   │   ├── Inventory.jsx
│   │   │   ├── Orders.jsx
│   │   │   ├── OrderDetails.jsx
│   │   │   ├── Sales.jsx
│   │   │   ├── Warehouses.jsx
│   │   │   ├── Customers.jsx
│   │   │   ├── RaiseTicket.jsx
│   │   │   ├── Incidents.jsx
│   │   │   ├── IncidentDetails.jsx
│   │   │   └── FinancialReconciliation.jsx
│   │   ├── parts/                  # Shared UI components
│   │   │   ├── Navbar.jsx
│   │   │   └── BreadcrumbsComponent.jsx
│   │   ├── context/
│   │   │   └── UserContext.jsx     # Global auth & user state
│   │   ├── App.jsx                 # Root component & route definitions
│   │   └── main.jsx                # React entry point
│   ├── assets/
│   │   └── duplo30.jpg             # Auth page background image
│   ├── vite.config.js
│   └── package.json
│
└── server/                         # Node.js + Express backend
    ├── models/                     # Mongoose schemas
    │   ├── user.model.js
    │   ├── customers.models.js
    │   ├── inv.models.js           # Inventory
    │   ├── orders.models.js
    │   ├── warehouse.models.js
    │   ├── sales.model.js
    │   ├── tickets.models.js
    │   ├── recon.models.js         # Financial reconciliation
    │   ├── suppliers.models.js
    │   └── tenants.models.js
    ├── routes/                     # Express route handlers
    │   ├── auth.routes.js
    │   ├── user.routes.js
    │   ├── customers.routes.js
    │   ├── inv.routes.js
    │   ├── orders.routes.js
    │   ├── warehouse.routes.js
    │   ├── sales.routes.js
    │   ├── tickets.routes.js
    │   ├── recon.routes.js
    │   └── dashboard.routes.js
    ├── utils/
    │   └── utils.js                # Nodemailer email helper
    ├── uploads/                    # Profile picture storage
    ├── index.js                    # Server entry point
    ├── .env                        # Environment config (not committed)
    └── package.json
```

---

## Quick Start

> **Prerequisites:** Node.js 18+, a running MongoDB instance (local or Atlas), and a Gmail account for email notifications.

```bash
# 1. Clone the repository
git clone https://github.com/nachiketgalande1609/Streamline.git
cd Streamline

# 2. Set up and start the backend
cd server
npm install
cp .env.example .env          # then fill in your values — see Environment Variables below
npm start

# 3. In a new terminal, set up and start the frontend
cd ../client
npm install                   # or: pnpm install
npm run dev
```

| Service | Local URL |
|---|---|
| Frontend | http://localhost:5173 |
| Backend API | http://localhost:3001 |

---

## Installation

### Backend Setup

Navigate to the `server/` directory and install dependencies:

```bash
cd server
npm install
```

**Development mode** (auto-restarts on file changes):

```bash
npm run dev
```

**Production mode:**

```bash
npm start
```

The API server starts on **port 3001**.

---

### Frontend Setup

Navigate to the `client/` directory and install dependencies:

```bash
cd client
npm install       # or: pnpm install
```

**Start the development server:**

```bash
npm run dev
```

**Build for production:**

```bash
npm run build
# Output is generated in client/dist/
```

**Preview the production build locally:**

```bash
npm run preview
```

**Run ESLint:**

```bash
npm run lint
```

---

## Environment Variables

Create a `.env` file inside the `server/` directory. The file is not committed to version control — you must create it manually.

```env
# ─── Database ────────────────────────────────────────────────────────────────

# MongoDB Atlas connection string (used in production)
MONGO_CONN_STRING=mongodb+srv://<username>:<password>@cluster0.mongodb.net/Streamline

# Local MongoDB connection string (used in development)
MONGO_CONN_STRING_LOCAL=mongodb://localhost:27017/Streamline

# ─── Email (Nodemailer / Gmail) ───────────────────────────────────────────────

# Gmail account used to send order and ticket notification emails
HOST_EMAIL=your-app-email@gmail.com

# Gmail App Password — NOT your regular Gmail password
# How to generate: Google Account > Security > 2-Step Verification > App passwords
EMAIL_PASS=your-16-character-app-password
```

> **Note on Gmail App Passwords:** Standard Gmail passwords are rejected by Nodemailer. You must generate a dedicated App Password from your Google account's security settings.

---

## API Reference

All endpoints are prefixed with `/api`. Authenticated endpoints require a `Bearer <token>` header.

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/register` | Register a new user |
| `POST` | `/api/login` | Login and receive a JWT |
| `POST` | `/api/logout` | Logout (client clears token) |
| `GET` | `/api/verify-token` | Validate an existing JWT |
| `GET` | `/api/tenants` | List all available tenants |

### Users

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/users` | List users with pagination, role and status filters |
| `GET` | `/api/users/roles` | Get all available roles |
| `POST` | `/api/users/profile` | Get a user's profile by ID |
| `PUT` | `/api/users/:id` | Update user details or upload a profile picture |

### Inventory

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/inventory` | List items with search, filter, and pagination |
| `POST` | `/api/inventory` | Add a new inventory item |
| `GET` | `/api/inventory/options` | Get available statuses, suppliers, and categories |
| `PATCH` | `/api/inventory/bulk-edit` | Bulk update multiple inventory items |

### Orders

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/orders` | List orders with status filter and pagination |
| `POST` | `/api/orders` | Create a new order |
| `GET` | `/api/orders/status` | Get available order statuses |
| `GET` | `/api/orders/customers-items` | Get customers and inventory for the order form |
| `GET` | `/api/orders/:orderId` | Get full order details and history |
| `PUT` | `/api/orders/:orderId/status` | Update order status (triggers email notification) |

### Customers

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/customers` | List customers with pagination |
| `POST` | `/api/customers` | Add a new customer |
| `PUT` | `/api/customers/:id` | Update customer details |
| `POST` | `/api/customers/delete` | Delete a customer |

### Warehouses

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/warehouse` | List warehouses with pagination |
| `POST` | `/api/warehouse` | Create a new warehouse |
| `GET` | `/api/warehouse/status` | Get available warehouse statuses |
| `GET` | `/api/warehouse/lov` | List of values for warehouse dropdowns |

### Sales

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/sales` | List sales with customer info and pagination |

### Tickets

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/tickets` | List all tickets |
| `POST` | `/api/tickets` | Create a ticket (triggers email notification) |
| `GET` | `/api/tickets/assignees` | Get users available for ticket assignment |
| `GET` | `/api/tickets/:ticketId` | Get ticket details with full change history |
| `PUT` | `/api/tickets/:ticketId` | Update ticket status or assignment |

### Financial Reconciliation

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/recon` | List reconciliations with month/year filter and pagination |

### Dashboard

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/dashboard` | Get KPI counts and warehouse summary |

---

## Database Models

### User

```
first_name, last_name, email, password (bcrypt hash)
phone_number, profile_picture, age
tenant        → ObjectId ref: tenants
role          → enum: admin | manager | sales | user
status        → enum: active | inactive | suspended
last_login, created_at, updated_at
```

### Customer

```
customer_name, contact_number, email
address, city, state, zip_code, country
company_name
customer_type → enum: individual | corporate
credit_limit, balance_due
notes, created_at, updated_at
```

### Inventory Item

```
name, description, make, category
on_hand_quantity, cost, price
supplier      → ObjectId ref: suppliers
warehouse     → ObjectId ref: warehouses
expiryDate
status        → enum: in stock | out of stock | discontinued
createdAt, updatedAt
```

### Order

```
orderId (unique), customerId
orderDate, shippingDate
status        → enum: pending | shipped | delivered | cancelled
totalAmount, taxAmount, netAmount
paymentMethod → enum: credit card | PayPal | cash on delivery
paymentStatus → enum: paid | unpaid | pending
paymentDate, shippingAddress, billingAddress
items[]       → [ itemId, itemName, quantity, price ]
createdBy, updatedBy, notes
```

### Warehouse

```
warehouse_id (unique), name, location
capacity, current_stock
manager_id    → ObjectId ref: users
contact_number
status        → enum: active | inactive
created_at, updated_at
```

### Sales

```
orderNumber, customerId
items[]       → [ productId, productName, quantity, price, total ]
totalAmount, paymentStatus, orderStatus
createdAt, updatedAt
```

### Ticket

```
ticketId, userId
issueType     → Bug | Billing | Feature Request | UI Issues | Performance | Other
department    → Support | Sales | Billing | Technical | Other
subject, description
priority      → low | medium | high | critical
status        → open | in progress | resolved | closed
assignedTo    → ObjectId ref: users
history[]     → [ action, performedBy, timestamp ]
createdAt, updatedAt
```

### Financial Reconciliation

```
recon_month, recon_year
totalIncome, totalExpenses, totalReconciled
createdBy, updatedBy
createdAt, updatedAt
```

---

## Frontend Routes

| Path | Component | Description |
|---|---|---|
| `/` | Dashboard | KPI overview and warehouse summary |
| `/login` | Login | Tenant selection and user authentication |
| `/register` | Register | New user registration |
| `/profile` | Profile | View and edit personal profile |
| `/users` | Users | User management (admin) |
| `/inventory` | Inventory | Product catalog with bulk edit and CSV tools |
| `/orders` | Orders | Order list with status filtering |
| `/order/:orderId` | OrderDetails | Full order details and change history |
| `/sales` | Sales | Sales pipeline view |
| `/warehouses` | Warehouses | Warehouse list and capacity info |
| `/customers` | Customers | Customer database |
| `/raise-ticket` | RaiseTicket | Submit a new support ticket |
| `/incidents` | Incidents | All support tickets |
| `/incidents/:ticketId` | IncidentDetails | Ticket detail with audit trail |
| `/recon` | FinancialReconciliation | Monthly/yearly reconciliation records |

---

## Deployment

### Backend — Render.com

1. Push the `server/` directory to your GitHub repository.
2. Create a new **Web Service** on [Render.com](https://render.com).
3. Set the **Build Command** to `npm install` and **Start Command** to `node index.js`.
4. Add the environment variables (`MONGO_CONN_STRING`, `HOST_EMAIL`, `EMAIL_PASS`) under the Render service's **Environment** settings.
5. In your MongoDB Atlas cluster, go to **Network Access** and allow connections from `0.0.0.0/0` (or Render's static outbound IPs).

### Frontend — Netlify

1. Build the frontend:
   ```bash
   cd client
   npm run build
   ```
2. Drag and drop the generated `dist/` folder onto [Netlify](https://netlify.com), **or** connect your GitHub repo for automatic deploys on push.
3. Set the **Publish directory** to `client/dist`.

### MongoDB Atlas

1. Create a free cluster at [mongodb.com/atlas](https://www.mongodb.com/atlas).
2. Create a database user and copy the connection string into `MONGO_CONN_STRING`.
3. Under **Network Access**, add `0.0.0.0/0` to allow inbound connections from your hosted backend.

---

## Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Commit your changes:
   ```bash
   git commit -m "feat: describe what this adds or changes"
   ```
4. Push the branch:
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a Pull Request against `main`.

---

## Contact

For questions or feedback, reach out at [nachiketgalande1609@gmail.com](mailto:nachiketgalande1609@gmail.com).

---

<div align="center">

Built with the MERN stack &nbsp;·&nbsp; Deployed on Render & Netlify &nbsp;·&nbsp; Database on MongoDB Atlas

</div>
