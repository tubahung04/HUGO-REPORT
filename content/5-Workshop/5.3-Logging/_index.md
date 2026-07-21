---
title: "3. Building the Web App (MERN Stack)"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

This section details how I built the SOC Dashboard application using MERN Stack.

### 1. Backend Setup (Node.js + Express + MongoDB)

**Backend Directory Structure:**
```
backend/
├── server.js          # Entry point, API routes
├── models/
│   ├── User.js        # User schema (username, password, role)
│   ├── Alert.js       # Alert schema (alert_type, severity, geo_location, audit_logs)
│   └── TrafficLog.js  # Traffic log schema (source_ip, destination_ip, bytes, protocol)
├── middleware/
│   └── auth.js        # JWT verify & Role-based middleware
└── package.json
```

**MongoDB Connection:**
```javascript
import mongoose from 'mongoose';
const MONGODB_URI = 'mongodb://127.0.0.1:27017/aws_monitor';
mongoose.connect(MONGODB_URI)
  .then(() => console.log('MongoDB connected successfully!'));
```

### 2. Role-Based Access Control (RBAC)

I designed 4 user roles with different permissions:

| Role | Permissions |
|------|------------|
| **NetAdmin** | View Dashboard, Traffic Logs |
| **SecOps** | View Dashboard, **manage alert statuses** (New → In Progress → Resolved) |
| **Manager** | View overview Dashboard |
| **SystemAdmin** | Full access (including changing alert statuses) |

**Code Snippet - RBAC Middleware:**
```javascript
// middleware/auth.js
export const checkRole = (allowedRoles) => (req, res, next) => {
  if (!allowedRoles.includes(req.user.role)) {
    return res.status(403).json({ error: 'Access denied' });
  }
  next();
};

// Usage: Only SecOps or SystemAdmin can change Alert status
app.put('/api/security/alerts/:id/status', 
  verifyToken, 
  checkRole(['SecOps', 'SystemAdmin']), 
  async (req, res) => { ... }
);
```

### 3. Main API Endpoints

| Method | Endpoint | Function |
|--------|----------|----------|
| POST | `/api/auth/login` | Login, returns JWT Token |
| GET | `/api/dashboard/overview` | KPI overview (total traffic, alert count) |
| GET | `/api/dashboard/traffic` | Network traffic chart data |
| GET | `/api/security/alerts` | Latest 10 security alerts |
| GET | `/api/dashboard/map` | IP coordinates for attack map |
| GET | `/api/dashboard/protocols` | Protocol distribution stats |
| GET | `/api/infrastructure/health` | CPU, RAM, Disk usage |
| GET | `/api/dashboard/anomaly` | AI anomaly detection data |
| GET | `/api/traffic/top-ips` | Top 10 bandwidth-consuming IPs |
| PUT | `/api/security/alerts/:id/status` | Change alert status (requires SecOps role) |

### 4. Frontend React - 9 Components

**Frontend Directory Structure:**
```
frontend/src/
├── App.jsx               # Main router, 3 tabs (Dashboard, Security, Traffic)
├── pages/
│   └── Login.jsx          # Login page
├── components/
│   ├── Sidebar.jsx        # Left navigation bar
│   ├── KPICards.jsx       # 3 KPI cards (Total Traffic, Alerts, Anomalies)
│   ├── TrafficChart.jsx   # Line chart for Sent/Received traffic
│   ├── AlertTable.jsx     # Security alerts table
│   ├── AttackMap.jsx      # Global attack map
│   ├── ProtocolPieChart.jsx # Protocol pie chart
│   ├── InfraHealth.jsx    # CPU/RAM/Disk progress bars
│   ├── AIAnomalyChart.jsx # Forecast vs Actual anomaly chart
│   └── TopIPConsole.jsx   # Top 10 IPs, filterable by protocol
└── contexts/
    └── AuthContext.jsx    # Global auth state management
```

The interface uses TailwindCSS with a Dark Theme (#030712), Glassmorphism effects, and micro-animations.

*(Insert your Dashboard screenshot here)*
![Dashboard UI](/images/Workshop/dashboard.jpg)

*(Insert your Security Alerts screenshot)*
![Security Alerts UI](/images/Workshop/security.png)

*(Insert your Traffic Logs screenshot)*
![Traffic Logs UI](/images/Workshop/traffic.png)
