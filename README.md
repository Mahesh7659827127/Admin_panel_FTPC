# FTPC INDIA — Enterprise Admin Panel with Role-Based Access Control (RBAC)

A complete, responsive, production-ready React.js Admin Portal built with professional enterprise architecture, JWT-based authentication, granular Role-Based Access Control (RBAC), and modern aesthetic styling inspired by FTPC India.

---

## 🚀 Tech Stack

- **Frontend Core**: React 18 (ES6+) with Vite
- **Routing**: React Router DOM v6
- **Global State**: Redux Toolkit (`@reduxjs/toolkit` + `react-redux`)
- **API Client**: Axios with Request/Response Interceptors & Mock Adapter
- **UI Framework**: Bootstrap 5 + React-Bootstrap + Bootstrap Icons
- **Visual Analytics**: Chart.js v4 + React-Chartjs-2
- **Authentication**: JWT (JSON Web Tokens) with automated expiration handling and Bearer token injection

---

## 🛡️ RBAC Architecture

The application enforces a dual-tier security model:

1. **Role Layer**: 4 standard roles (`ADMIN`, `MANAGER`, `STAFF`, `USER`)
2. **Permission Layer**: 16 granular action capabilities grouped into 6 modules:
   - **Dashboard**: `dashboard:view`, `analytics:view`
   - **User Management**: `users:view`, `users:create`, `users:edit`, `users:delete`
   - **Role Management**: `roles:view`, `roles:create`, `roles:edit`, `roles:delete`
   - **Activity Logs**: `activity:view`, `activity:export`
   - **Personal Profile**: `profile:view`, `profile:edit`
   - **System Settings**: `settings:view`, `settings:edit`

### Role Privileges Matrix

| Role | User CRUD | Role Management | Analytics | Audit Logs | System Settings |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Admin** | Full (Create, Read, Update, Delete) | Full (Create, Read, Update, Delete) | Full | Full + CSV Export | Full |
| **Manager** | View, Create, Update (No Delete) | View Only | Full | Full + CSV Export | View Only |
| **Staff** | View Only | None | Limited | View Only | None |
| **User** | None | None | Personal | None | None |

---

## 🔑 Demo Credentials

Quick 1-click autofill buttons are provided on the login page for instant testing:

| Role | Email | Password | Access Capabilities |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@ftpcindia.com` | `password123` | Full superuser access to all pages and settings |
| **Manager** | `manager@ftpcindia.com` | `password123` | User directory management, analytics & logs |
| **Staff** | `staff@ftpcindia.com` | `password123` | Read-only user directory and operations |
| **User** | `user@ftpcindia.com` | `password123` | Member dashboard, self-profile & credentials |

---

## 📁 Project Architecture

```
mahesh/
├── .env                         # Local runtime environment variables
├── .env.example                 # Production environment template
├── index.html                   # HTML entry point with Google Fonts
├── vite.config.js               # Vite configuration with chunk splitting
├── package.json                 # Dependencies and scripts
├── test-rbac.js                 # Automated RBAC verification suite
└── src/
    ├── assets/                  # CSS stylesheets, brand badges, and SVGs
    ├── components/
    │   ├── common/              # Badge, LoadingSpinner, Pagination, SearchInput, ConfirmationModal
    │   ├── rbac/                # PermissionGuard, RoleGuard, HasPermission
    │   └── charts/              # MetricStatsCard, ActivityChart, RoleDistributionChart
    ├── layouts/                 # MainLayout, AuthLayout, Navbar, Sidebar, Footer
    ├── pages/
    │   ├── auth/                # Login page with demo autofill
    │   ├── dashboard/           # Role-aware dashboard with KPI cards and charts
    │   ├── users/               # UserList, UserFormModal, UserDetailsDrawer
    │   ├── roles/               # RoleList, RoleFormModal, PermissionMatrix
    │   ├── profile/             # Profile overview, edit details, password reset, permissions list
    │   ├── activity/            # ActivityLogs with search, severity filter & CSV export
    │   ├── settings/            # SystemSettings (security policies & database reset)
    │   └── errors/              # NotFound (404), Forbidden (403)
    ├── routes/                  # AppRoutes, ProtectedRoute (guards)
    ├── services/
    │   ├── api/                 # axiosClient, authApi, userApi, roleApi, dashboardApi, activityApi
    │   └── mock/                # In-browser mock server with localStorage persistence
    ├── store/                   # Redux store & slices (auth, users, roles, logs, ui)
    ├── hooks/                   # useAuth, usePermission, useDebounce, useNotification
    ├── constants/               # roles.js, permissions.js, navItems.js
    └── utils/                   # jwt.js, formatters.js, storage.js
```

---

## ⚙️ Getting Started

### 1. Installation
```bash
npm install
```

### 2. Start Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

### 3. Run Automated RBAC Test Suite
```bash
npm test
```

### 4. Build for Production
```bash
npm run build
```
Generates optimized chunks in `dist/`.

---

## 🔌 Switching to a Real Backend API

To connect the application to an external backend REST API:
1. Open `.env`
2. Set `VITE_USE_MOCK_API=false`
3. Point `VITE_API_BASE_URL` to your backend endpoint (e.g. `https://api.yourdomain.com/api`)
4. Ensure your backend accepts the standard Bearer token header (`Authorization: Bearer <token>`) and returns JSON responses in `{ success: true, data: ... }` format.
