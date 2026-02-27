# Fast-Food Backend Server

Chào mừng đến với hệ thống Back-end của dự án **Fast-Food**. Đây là nền tảng API cung cấp dữ liệu, xử lý nghiệp vụ chính, bảo mật và tương tác theo thời gian thực.

## 🚀 1. Giới thiệu Project

**Fast-Food Server** là hệ thống API được xây dựng theo kiến trúc Module mạnh mẽ của NestJS. Dự án xử lý toàn bộ logic nghiệp vụ (business logic), tích hợp đa dạng service bên thứ 3 và đảm bảo dữ liệu toàn vẹn cho nền tảng Fast-Food.

## 🛠️ 2. Tài liệu kỹ thuật và công nghệ sử dụng

Hệ thống Back-end sử dụng các công nghệ, database và thư viện hiện đại:

- **Core & Framework:**
  - **🐈 NestJS 11:** Framework chủ đạo cho kiến trúc backend có khả năng mở rộng (scalable). Tận dụng OOP, FP và FRP.
  - **⚙️ Node.js & TypeScript:** Nền tảng thực thi JS vững chắc và bắt trọn lỗi trong quá trình phát triển (static typing).

- **Database & ORM:**
  - **🛡️ Prisma ORM (v6):** Công cụ tiên tiến giúp định nghĩa Schema và Query Database một cách dễ dàng, type-safe (tránh lỗi truy vấn).
  - **⚡ Redis (v5.6):** Caching data tốc độ cao, hỗ trợ queueing và session.

- **Background Jobs & Queue:**
  - **📦 BullMQ:** Xử lý hàng đợi mạnh mẽ và đáng tin cậy. Xử lý các tác vụ nền tảng (background tasks/jobs) mà không chặn luồng chính.
  - **⏱️ @nestjs/schedule (Cronjobs):** Thiết lập và tự động hóa các tác vụ lặp lại định kỳ (Cron jobs).

- **Features & Integrations:**
  - **🔌 WebSockets (Socket.io):** Giao tiếp thời gian thực, cho các tính năng Notification hoặc Streaming từ Server xuống Client.
  - **☁️ AWS S3:** Dịch vụ lưu trữ Object storage đám mây lớn (Images, Documents, Static Assets) thông qua `@aws-sdk`.
  - **💳 VNPay:** Tích hợp bộ cổng thanh toán trung gian lớn tại Việt Nam thông qua module `nestjs-vnpay`, `vnpay`.
  - **📧 Resend:** Dịch vụ gửi email (Transactional Emails) mạnh mẽ dành cho dev.
  - **🔑 JWT (JSON Web Tokens) & Bcrypt:** Băm mật khẩu (hashing) và cấp quyền truy cập bảo mật.
  - **✅ Zod & nestjs-zod:** Schema validation trên dữ liệu đầu vào.
  - **🌐 Google APIs:** Tích hợp với hệ sinh thái của Google.
  - **📁 Multer:** Quản lý upload file.

## 📂 3. Cấu trúc dự án

Dưới đây là một phần tổ chức thư mục của mã nguồn chính `src/`:

```text
src/
 ├── consumers/           # Các Worker Functions bắt events từ BullMQ Queue
 ├── cronjobs/            # Các tiến trình nền (Scheduled tasks/CronJobs định kỳ)
 ├── routes/              # Chứa các Module API, định nghĩa Controllers & Services cho từng Feature:
 │    ├── address/        # API địa chỉ khách hàng
 │    ├── auth/           # Xác thực người dùng (Login, Register, Token...)
 │    ├── cart/           # Quản lý giỏ hàng
 │    ├── category/       # Quản lý danh mục sản phẩm
 │    ├── coupon/         # Cấu hình mã giảm giá (Vouchers)
 │    ├── district/       # Dữ liệu quận/huyện
 │    ├── draft-item/     # Lưu trữ bản nháp (Draft)
 │    ├── media/          # Hình ảnh/tệp tin đính kèm
 │    ├── order/          # Xử lý luồng đặt hàng
 │    ├── payment/        # Xử lý thanh toán (VNPay...)
 │    ├── permission/     # Quản lý và khai báo quyền truy cập
 │    ├── product/        # Quản lý chi tiết món ăn/thực đơn
 │    ├── profile/        # Quản lý hồ sơ người dùng
 │    ├── province/       # Dữ liệu tỉnh/thành phố
 │    ├── recommendation/ # Gợi ý món ăn thông minh
 │    ├── reservation/    # Quản lý quá trình đặt bàn
 │    ├── review/         # Xem đánh giá/phản hồi thực khách
 │    ├── role/           # Nhóm quyền (Roles)
 │    ├── statistics/     # Báo cáo thống kê (Doanh thu, v.v)
 │    ├── table/          # Quản lý danh sách bàn ăn thực tế
 │    ├── tag/            # Quản lý nhãn món ăn (Tags)
 │    ├── user/           # Quản lý người dùng hệ thống
 │    └── ward/           # Dữ liệu phường/xã
 ├── shared/              # Tầng dùng chung: Constants, Helpers, Decorators, Prisma Service, Redis config
 ├── websockets/          # Xử lý các sự kiện thời gian thực (Gateway của Socket.io)
 ├── app.controller.ts    # Entry controller thử của Nest
 ├── app.module.ts        # Root Module của toàn platform backend
 ├── app.service.ts       # Root Service của toàn platform
 ├── main.ts              # Entry point bootstrap application của NestJS
 └── types.ts             # Các Data Transfer Objects và Interfaces mở rộng
```

Các thư mục phụ trợ bên ngoài:

- `initSeedData/` : Chứa các kịch bản chạy seed data/mocking database.
- `prisma/` : Điểm định nghĩa Schema cho cơ sở dữ liệu (schema.prisma, migrations, v.v).
- `test/` : Chứa môi trường kiểm thử E2E (End-To-End) và Testing configurations của Jest.

## ⚙️ 4. Hướng dẫn cài đặt và sử dụng

### 📌 Yêu cầu môi trường

- NodeJS.
- Một Database tương thích mà Prisma hỗ trợ (ví dụ PostgreSQL, MySQL).
- Redis (Cấu hình chạy thông qua Docker là cách tốt nhất).

### 🚀 Các bước cài đặt và vận hành Server

**1. Khởi tạo & Cài đặt:**

```bash
npm install
```

**2. Cấu hình Biến Môi trường:**
Tạo tệp `.env` ở thư mục gốc (root) và đảm bảo bạn điền đầy đủ cấu hình cho Database/Redis và API keys:

- `DATABASE_URL` (cho Prisma)
- Keys/Secrets cho VNPay, Resend, JWT, AWS S3,...

**3. Khởi tạo Database (Migration & Generation):**
Sau khi cấu hình URL xong, hãy đồng bộ models của Prisma xuống Database của bạn:

```bash
npx prisma generate
npx prisma db push
```

_(Nếu muốn quản lý lịch sử version DB, có thể thay đổi sang dùng `npx prisma migrate dev`)_

**4. Khởi tạo Data mặc định (Seeders):**
Project bao gồm các script khởi tạo sẵn các giá trị cấu hình ở thư mục `initSeedData`. Bạn có thể tuân theo trình tự khởi tạo:

```bash
npm run create:base-data
npm run create:locations
npm run create:permissions
```

**5. Khởi chạy Server ở môi trường Development:**

```bash
npm run start:dev
```

Lệnh này sẽ kèm cờ `--watch` để theo dõi các file TypeScript thay đổi và build lại.

**6. Khởi chạy Build & Production:**

```bash
npm run build
npm run start:prod
```

Build source code từ TS sang JS trong thư mục `dist/`, rồi chạy Node thuần túy trên `main.js`.
