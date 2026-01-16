# 📘 TÀI LIỆU KỸ THUẬT & PHÂN CÔNG NHIỆM VỤ (TECH STACK & TASK ASSIGNMENT)

## 1. TỔNG QUAN (INTRODUCTION)
Để xây dựng một nền tảng E-learning hiện đại, có khả năng mở rộng (scalable) và bảo trì dễ dàng (maintainable), dự án được xây dựng dựa trên kiến trúc **Microservices** và tuân thủ các nguyên lý của **Domain-Driven Design (DDD)**. Hệ thống được chia thành các dịch vụ độc lập, giao tiếp với nhau qua giao thức chuẩn, đảm bảo hiệu năng cao và trải nghiệm người dùng tối ưu.

---

## 2. KIẾN TRÚC HỆ THỐNG (SYSTEM ARCHITECTURE)

### 2.1. Mô hình tổng quát
*   **Client Side:** Next.js (Web App)
*   **API Gateway:** Đóng vai trò cửa ngõ duy nhất, điều hướng request từ Client đến các Service.
*   **Microservices:** Các dịch vụ backend độc lập (Auth, Course, Payment, etc.) chạy trên FastAPI.
*   **Database:** Mô hình *Database per Service* (Mỗi service có DB riêng).
*   **Inter-service Communication:**
    *   **Synchronous (Đồng bộ):** RESTful API / gRPC (cho các tác vụ cần phản hồi ngay).
    *   **Asynchronous (Bất đồng bộ):** RabbitMQ / Kafka (cho các xử lý nền, decoupling hệ thống).

### 2.2. Giao thức & Hạ tầng
| Hạng mục | Công nghệ sử dụng | Ghi chú |
| :--- | :--- | :--- |
| **API Gateway** | Kong / Traefik | Quản lý routing, rate limiting, auth guard. |
| **Communication** | REST (FastAPI), gRPC | REST cho Client-Server, gRPC cho Service-Service (nếu cần hiệu năng cao). |
| **Message Broker** | RabbitMQ / Kafka | Xử lý sự kiện (Order Placed -> Unlock Course -> Send Email). |
| **Containerization** | Docker | Đóng gói ứng dụng. |
| **Orchestration** | Kubernetes (K8s) | Quản lý, scaling container. |
| **CI/CD** | GitLab CI / GitHub Actions | Tự động hóa quy trình build & deploy. |
| **Monitoring** | Prometheus & Grafana | Theo dõi metrics, sức khỏe hệ thống. |
| **Logging** | ELK Stack (Elastic-Logstash-Kibana) | Tập trung và phân tích log. |

---

## 3. CÔNG NGHỆ SỬ DỤNG (TECHNOLOGY STACK)

### 3.1. Frontend (Web Application)
*   **Framework:** **Next.js** (React) - Tối ưu SEO và Performance (SSR/ISR).
*   **State Management:** **Redux Toolkit** - Quản lý trạng thái ứng dụng phức tạp.
*   **Styling:** **Tailwind CSS** - Utility-first CSS framework.
*   **UI Components:** **ShadcnUI** - Bộ component hiện đại, dễ tùy biến.

### 3.2. Backend (Microservices)
*   **Framework:** **FastAPI** (Python) - Hiệu năng cao, hỗ trợ tốt async/await.
*   **ORM:** **SQLModel** - Kết hợp sức mạnh của SQLAlchemy và Pydantic.
*   **Validation:** **Pydantic** - Kiểm soát chặt chẽ dữ liệu đầu vào/ra.

### 3.3. Cơ sở dữ liệu & Lưu trữ (Databases & Storage)
| Loại | Công nghệ | Mục đích sử dụng |
| :--- | :--- | :--- |
| **Relational DB** | **PostgreSQL** | Lưu dữ liệu có cấu trúc (User, Order, Transaction). Yêu cầu tính nhất quán cao (ACID). |
| **NoSQL** | **MongoDB** | Lưu dữ liệu bán cấu trúc (Exam, Quiz, Chat Logs, Comments). Linh hoạt thay đổi schema. |
| **Cache** | **Redis** | Caching session, thông tin khóa học phổ biến để giảm tải DB. |
| **Search Engine** | **Elasticsearch** | Tìm kiếm Full-text siêu tốc cho khóa học và nội dung phụ đề video. |
| **Object Storage** | **AWS S3 / MinIO** | Lưu trữ video gốc và các tệp tin tĩnh (Static Assets). |

### 3.4. Video Streaming & Processing
*   **Processing:** **FFmpeg** - Transcode video sang định dạng stream.
*   **Streaming Protocol:** **HLS (HTTP Live Streaming)** hoặc DASH.
*   **Adaptive Bitrate:** Tự động điều chỉnh chất lượng (720p, 1080p, 4K) dựa trên băng thông người dùng.
*   **CDN:** **AWS CloudFront** - Phân phối nội dung nhanh chóng toàn cầu.
*   **DRM:** Mã hóa video token-based để bảo vệ bản quyền (chống IDM/download).

---

## 4. DANH SÁCH THÀNH VIÊN (MEMBER LIST)
*Điền tên thành viên vào bảng dưới đây:*

| Mã (Code) | Vai trò (Role) | Họ và tên (Full Name) |
| :--- | :--- | :--- |
| **M1** | Team Leader / Architect / DevOps | [Điền tên M1] |
| **M2** | Backend Dev (Course & Media) | [Điền tên M2] |
| **M3** | Frontend Lead & Architect | [Điền tên M3] |
| **M4** | Fullstack Dev (Learning Logic) | [Điền tên M4] |
| **M5** | Fullstack Dev (Interaction) | [Điền tên M5] |
| **M6** | Backend Dev (Payment) | [Điền tên M6] |

---

## 5. PHÂN CÔNG NHIỆM VỤ CHI TIẾT (DETAILED RESPONSIBILITIES)
Mô hình phát triển theo **Domain-Driven Design (DDD)**. Hệ thống chia làm 6 thành viên (M1 - M6).

### 🏷️ Nhóm 1: Core & Infrastructure (Nền tảng)
**Phụ trách: M1 (Team Leader / Architect)**

*   **Backend (FastAPI):**
    *   **Auth Service:** Đăng ký, Đăng nhập, SSO, JWT Management, RBAC (Phân quyền).
    *   **Shared Libraries:** Xây dựng core modules (Logger, Error Handler, Base Models) cho cả team dùng lại.
    *   **API Gateway Config:** Cấu hình routing và bảo mật cơ bản.
*   **Frontend (Next.js):**
    *   **Giao diện Authentication (Login/Register).**
*   **DevOps:**
    *   Setup Docker Compose, Dockerfile chuẩn.
    *   Thiết lập CI/CD Pipeline cơ bản.

### 🎥 Nhóm 2: Course & Media (Khoá học & Video)
**Phụ trách: M2 (Backend) & M3 (Frontend Lead & Architect)**

*   **M2 - Backend Developer:**
    *   **Course Service:** CRUD Khóa học, Chương, Bài giảng. Tích hợp Elasticsearch.
    *   **Media Service:** Xử lý upload video (Upload -> Transcode -> S3 -> Notification). Xử lý FFmpeg background tasks.
*   **M3 - Frontend Lead & Architect:**
    *   **Architecture & DevOps:** Thiết kế toàn bộ kiến trúc Frontend, quyết định công nghệ. Setup CI/CD, deploy Frontend lên Vercel/Docker.
    *   **Core UI:** Thiết kế Layout chính, Landing Page, Design System (ShadcnUI).
    *   **Video Player Custom:** Phát triển trình phát video hỗ trợ HLS, Adaptive Bitrate, lưu tiến trình xem, chặn download.
    *   Hỗ trợ định nghĩa API specs cho M2.

### Tóm tắt phân công nhiệm vụ
| Thành viên | Vai trò chính | Nhiệm vụ Backend | Nhiệm vụ Frontend |
| :--- | :--- | :--- | :--- |
| **M1 (Lead)** | Architect / DevOps | **Auth Service**, API Gateway, Shared Libs | Authen UI |
| **M2** | Backend Dev | **Course Service**, **Media Service** (Video processing) | *(Hỗ trợ API cho M3)* |
| **M3** | Frontend Lead & Architect | *(Hỗ trợ định nghĩa API cho M2)* | **Entire System Design**, Core UI, Video Player, Landing Page, CI/CD Frontend |

### 🎓 Nhóm 3: Learning & Assessment (Học tập & Kiểm tra)
**Phụ trách: M4 (Fullstack - Logic)**

*   **Backend (FastAPI) - Learning Service:**
    *   **Progress Tracking:** Theo dõi tiến độ học (ví dụ: hoàn thành 80%).
    *   **Quiz/Exam Core:** Logic tạo đề, trộn đề, chấm điểm tự động.
    *   **Certificate:** Sinh chứng chỉ PDF tự động.
    *   *Sử dụng MongoDB cho dữ liệu bài thi.*
*   **Frontend (Next.js):**
    *   Giao diện làm bài thi (Countdown timer, auto-submit).
    *   Dashboard học viên (Tiến độ, chứng chỉ).

### 💬 Nhóm 4: Social & Interactive (Tương tác)
**Phụ trách: M5 (Fullstack - Realtime)**

*   **Backend (FastAPI) - Interaction Service:**
    *   **WebSockets:** Xử lý Chat Real-time, Notifications.
    *   **Q&A System:** Hỏi đáp trong bài học.
    *   **Support Tickets:** Hệ thống tích hợp hỗ trợ cho TA (Trợ giảng).
    *   *Sử dụng MongoDB cho log chat.*
*   **Frontend (Next.js):**
    *   Floating Chatbox, Notification Center.
    *   Dashboard dành cho Trợ giảng (TA).

### 💰 Nhóm 5: Payment & Sales (Kinh doanh)
**Phụ trách: M6 (Backend - Payment)**

*   **Backend (FastAPI) - Payment Service:**
    *   **Order System:** Giỏ hàng, Quản lý đơn hàng.
    *   **Payment Gateway:** Tích hợp Stripe/VnPay/Momo. Xử lý Webhook an toàn.
    *   **Financial Reports:** Thống kê doanh thu.
    *   *Sử dụng PostgreSQL để đảm bảo ACID.*
*   **Billing Frontend:**
    *   Phối hợp với M3 để làm trang Checkout, Payment Success/Failure.
    *   Admin Dashboard (Phần Thống kê doanh thu).

---

## 6. QUY CHUẨN PHÁT TRIỂN (DEVELOPMENT GUIDELINES)

1.  **Code Consistency:**
    *   Tuân thủ cấu trúc thư mục do M1 quy định.
    *   Mọi API phải có document (Swagger/OpenAPI) tự động từ FastAPI.
2.  **Data Integrity:**
    *   Không gọi trực tiếp Database của Service khác. Dùng API hoặc Messaging.
    *   Xử lý giao dịch phân tán (Payment -> Unlock Course) cẩn thận, ưu tiên dùng Event-driven (RabbitMQ).
3.  **Frontend UX/UI:**
    *   Sử dụng chung bộ UI Kit (ShadcnUI) để đồng bộ trải nghiệm.
    *   M3 chịu trách nhiệm review UI code của các thành viên khác.
