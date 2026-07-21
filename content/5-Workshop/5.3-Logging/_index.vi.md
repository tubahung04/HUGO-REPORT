---
title: "3. Xây dựng Web App (MERN Stack)"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Phần này trình bày chi tiết cách tôi xây dựng ứng dụng SOC Dashboard bằng MERN Stack.

### 1. Khởi tạo Backend (Node.js + Express + MongoDB)

**Cấu trúc thư mục Backend:**
```
backend/
├── server.js          # Entry point, API routes
├── models/
│   ├── User.js        # Schema người dùng (username, password, role)
│   ├── Alert.js       # Schema cảnh báo (alert_type, severity, geo_location, audit_logs)
│   └── TrafficLog.js  # Schema log lưu lượng (source_ip, destination_ip, bytes, protocol)
├── middleware/
│   └── auth.js        # JWT verify & Role-based middleware
└── package.json
```

**Kết nối MongoDB:**
```javascript
import mongoose from 'mongoose';
const MONGODB_URI = 'mongodb://127.0.0.1:27017/aws_monitor';
mongoose.connect(MONGODB_URI)
  .then(() => console.log('Đã kết nối MongoDB thành công!'));
```

### 2. Hệ thống phân quyền (Role-Based Access Control)

Tôi thiết kế 4 vai trò người dùng với quyền hạn khác nhau:

| Vai trò | Quyền hạn |
|---------|-----------|
| **NetAdmin** | Xem Dashboard, Traffic Logs |
| **SecOps** | Xem Dashboard, **quản lý trạng thái cảnh báo** (New → In Progress → Resolved) |
| **Manager** | Xem Dashboard tổng quan |
| **SystemAdmin** | Toàn quyền (bao gồm cả thay đổi trạng thái cảnh báo) |

**Code Snippet - Middleware phân quyền:**
```javascript
// middleware/auth.js
export const checkRole = (allowedRoles) => (req, res, next) => {
  if (!allowedRoles.includes(req.user.role)) {
    return res.status(403).json({ error: 'Bạn không có quyền truy cập' });
  }
  next();
};

// Áp dụng: Chỉ SecOps hoặc SystemAdmin mới đổi được trạng thái Alert
app.put('/api/security/alerts/:id/status', 
  verifyToken, 
  checkRole(['SecOps', 'SystemAdmin']), 
  async (req, res) => { ... }
);
```

### 3. Các API Endpoint chính

| Method | Endpoint | Chức năng |
|--------|----------|-----------|
| POST | `/api/auth/login` | Đăng nhập, trả về JWT Token |
| GET | `/api/dashboard/overview` | Lấy KPI tổng quan (tổng traffic, số alert) |
| GET | `/api/dashboard/traffic` | Dữ liệu biểu đồ lưu lượng mạng |
| GET | `/api/security/alerts` | Danh sách 10 cảnh báo mới nhất |
| GET | `/api/dashboard/map` | Tọa độ IP cho bản đồ tấn công |
| GET | `/api/dashboard/protocols` | Thống kê phân bổ giao thức |
| GET | `/api/infrastructure/health` | CPU, RAM, Disk usage |
| GET | `/api/dashboard/anomaly` | Dữ liệu AI phát hiện bất thường |
| GET | `/api/traffic/top-ips` | Top 10 IP tiêu thụ băng thông |
| PUT | `/api/security/alerts/:id/status` | Đổi trạng thái cảnh báo (cần quyền SecOps) |

### 4. Frontend React - 9 Components

**Cấu trúc thư mục Frontend:**
```
frontend/src/
├── App.jsx               # Router chính, 3 tab (Dashboard, Security, Traffic)
├── pages/
│   └── Login.jsx          # Trang đăng nhập
├── components/
│   ├── Sidebar.jsx        # Thanh điều hướng bên trái
│   ├── KPICards.jsx       # 3 thẻ KPI (Total Traffic, Alerts, Anomalies)
│   ├── TrafficChart.jsx   # Biểu đồ đường lưu lượng Sent/Received
│   ├── AlertTable.jsx     # Bảng cảnh báo bảo mật
│   ├── AttackMap.jsx      # Bản đồ tấn công toàn cầu
│   ├── ProtocolPieChart.jsx # Biểu đồ tròn giao thức
│   ├── InfraHealth.jsx    # Thanh tiến trình CPU/RAM/Disk
│   ├── AIAnomalyChart.jsx # Biểu đồ Forecast vs Actual
│   └── TopIPConsole.jsx   # Top 10 IP, lọc theo protocol
└── contexts/
    └── AuthContext.jsx    # Quản lý trạng thái đăng nhập toàn cục
```

Giao diện sử dụng TailwindCSS với Dark Theme tông màu tối (#030712), hiệu ứng Glassmorphism và micro-animation.

*(Chèn ảnh giao diện Dashboard của bạn tại đây)*
![Giao diện Dashboard](/images/Workshop/webapp_dashboard.png)

*(Chèn ảnh giao diện Security Alerts)*
![Giao diện Security Alerts](/images/Workshop/webapp_security.png)

*(Chèn ảnh giao diện Traffic Logs)*
![Giao diện Traffic Logs](/images/Workshop/webapp_traffic.png)
