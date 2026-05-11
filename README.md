# Vaccination-Booking-System

## Mô Tả Dự Án

Hệ thống Đặt Lịch Tiêm Chủng (Vaccination-Booking-System) là một ứng dụng web hiện đại được xây dựng bằng Spring Boot, giúp người dùng dễ dàng đặt lịch tiêm chủng, quản lý thông tin tiêm chủng, và theo dõi lịch sử tiêm chủng. Hệ thống hỗ trợ xác thực người dùng, quản lý tài khoản, và cung cấp các tính năng quản lý toàn diện cho nhân viên y tế.

## Tính Năng Chính

- **Xác Thực & Bảo Mật**: Xác thực người dùng bằng JWT (JSON Web Token), mã hóa mật khẩu an toàn
- **Đặt Lịch Tiêm**: Người dùng có thể dễ dàng đặt lịch tiêm chủng tại các cơ sở y tế
- **Quản Lý Tài Khoản**: Quản lý thông tin cá nhân, lịch sử tiêm chủng
- **Thông Báo Email**: Gửi thông báo xác nhận, nhắc nhở lịch tiêm qua email
- **Ghi Chép Tiêm**: Quản lý hồ sơ tiêm chủng chi tiết
- **Dashboard**: Giao diện trực quan để xem lịch sử và trạng thái đặt lịch
- **API RESTful**: Cung cấp các endpoint API đầy đủ với tài liệu Swagger/OpenAPI

## Công Nghệ Sử Dụng

### Backend

| Công Nghệ | Phiên Bản | Mục Đích |
|-----------|----------|---------|
| **Java** | 17 | Ngôn ngữ lập trình chính |
| **Spring Boot** | 3.4.2 | Framework chính |
| **Spring Web** | Latest | Xây dựng RESTful API |
| **Spring Security** | Latest | Xác thực và phân quyền |
| **Spring Data MongoDB** | Latest | ORM cho MongoDB |
| **Spring Mail** | Latest | Gửi email |
| **JWT (JJWT)** | 0.11.5 | Token xác thực |
| **Lombok** | Latest | Giảm boilerplate code |
| **Jackson** | 2.15.0 | JSON processing |
| **SpringDoc OpenAPI** | 2.3.0 | Tài liệu API (Swagger) |

### Database

- **MongoDB**: Cơ sở dữ liệu NoSQL để lưu trữ dữ liệu người dùng, lịch tiêm, và thông tin y tế

### Build Tool

- **Maven**: Quản lý dependency và build project
- **Heroku**: Deployment và hosting

## Yêu Cầu Hệ Thống

- Java 17 trở lên
- Maven 3.6 hoặc cao hơn
- MongoDB (local hoặc cloud như MongoDB Atlas)
- Email service (SMTP) để gửi thông báo

## Cài Đặt & Chạy

### 1. Clone Repository

```bash
git clone https://github.com/HLocLe/Vaccination-Booking-System.git
cd Vaccination-Booking-System
```

### 2. Cấu Hình Môi Trường

Tạo file `application.properties` hoặc `application.yml` trong thư mục `src/main/resources`:

```properties
# Database Configuration
spring.data.mongodb.uri=mongodb+srv://username:password@cluster.mongodb.net/vaccination_db

# Email Configuration
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=your-email@gmail.com
spring.mail.password=your-app-password
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true

# JWT Configuration
jwt.secret=your-secret-key-here
jwt.expiration=86400000
```

### 3. Build Project

```bash
./mvnw clean package
```

Trên Windows:

```bash
mvnw.cmd clean package
```

### 4. Chạy Ứng Dụng

```bash
./mvnw spring-boot:run
```

Hoặc chạy file JAR trực tiếp:

```bash
java -jar target/Swp_Project-0.0.1-SNAPSHOT.jar
```

Ứng dụng sẽ chạy tại `http://localhost:8080`

## API Documentation

API documentation được tạo tự động bằng Swagger/OpenAPI. Truy cập tại:

```
http://localhost:8080/swagger-ui.html
```

Hoặc xem chi tiết API:

```
http://localhost:8080/v3/api-docs
```

## Cấu Trúc Dự Án

```
Vaccination-Booking-System/
├── src/
│   ├── main/
│   │   ├── java/com/example/
│   │   │   ├── controller/          # Controllers xử lý request
│   │   │   ├── service/             # Business logic
│   │   │   ├── repository/          # Data access layer
│   │   │   ├── entity/              # Entity models
│   │   │   ├── dto/                 # Data Transfer Objects
│   │   │   ├── config/              # Configuration classes
│   │   │   ├── security/            # Security configuration
│   │   │   └── exception/           # Exception handlers
│   │   └── resources/
│   │       └── application.properties
│   └── test/
├── pom.xml                          # Maven configuration
├── Procfile                         # Deployment configuration
├── mvnw                             # Maven wrapper (Linux/Mac)
├── mvnw.cmd                         # Maven wrapper (Windows)
└── README.md                        # File này
```

## Endpoints Chính

### Authentication (Xác Thực)
- `POST /api/auth/register` - Đăng ký người dùng mới
- `POST /api/auth/login` - Đăng nhập
- `POST /api/auth/refresh` - Làm mới token JWT

### User (Người Dùng)
- `GET /api/users/profile` - Lấy thông tin cá nhân
- `PUT /api/users/profile` - Cập nhật thông tin cá nhân
- `GET /api/users/{id}` - Lấy thông tin người dùng theo ID

### Vaccination (Tiêm Chủng)
- `GET /api/vaccinations` - Danh sách tất cả các loại vaccine
- `POST /api/vaccinations/book` - Đặt lịch tiêm
- `GET /api/vaccinations/bookings` - Lịch sử đặt lịch
- `GET /api/vaccinations/bookings/{id}` - Chi tiết đặt lịch
- `PUT /api/vaccinations/bookings/{id}` - Cập nhật đặt lịch
- `DELETE /api/vaccinations/bookings/{id}` - Hủy đặt lịch

### Health (Sức Khỏe)
- `GET /api/health` - Kiểm tra sức khỏe server

## Security

- Sử dụng **Spring Security** để bảo vệ endpoints
- **JWT Token** cho xác thực không trạng thái
- **Password Encoding** bằng BCrypt
- **CORS** configuration cho frontend integration

## Email Service

Hệ thống gửi email tự động cho:
- Xác nhận đăng ký
- Nhắc nhở lịch tiêm
- Thông báo kết quả tiêm

## Deployment

### Deploy lên Heroku

```bash
# Login Heroku
heroku login

# Create Heroku app
heroku create vaccination-booking-system

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

### Environment Variables trên Heroku

```bash
heroku config:set SPRING_DATA_MONGODB_URI="your-mongodb-uri"
heroku config:set SPRING_MAIL_USERNAME="your-email"
heroku config:set SPRING_MAIL_PASSWORD="your-app-password"
heroku config:set JWT_SECRET="your-secret-key"
```

## Testing

Chạy unit tests:

```bash
./mvnw test
```

Chạy integration tests:

```bash
./mvnw verify
```

## Troubleshooting

### MongoDB Connection Error
- Kiểm tra kết nối MongoDB URI
- Đảm bảo IP whitelist trong MongoDB Atlas
- Kiểm tra username/password

### Email Not Sending
- Bật "Less secure app access" nếu dùng Gmail
- Sử dụng App Password thay vì password thực
- Kiểm tra SMTP configuration

### JWT Token Issues
- Đảm bảo JWT secret key đã được đặt
- Kiểm tra expiration time
- Xác nhận header Authorization đúng format: `Bearer <token>`

## Contribution

Nếu bạn muốn đóng góp cho dự án:

1. Fork repository
2. Tạo branch feature (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Mở Pull Request

## License

Dự án này chưa được gán license cụ thể. Để biết thêm chi tiết, vui lòng liên hệ tác giả.

## Author

**HLocLe** - [GitHub Profile](https://github.com/HLocLe)

## Support

Nếu có câu hỏi hoặc gặp vấn đề, vui lòng:
- Tạo [Issue](https://github.com/HLocLe/Vaccination-Booking-System/issues) trên GitHub
- Liên hệ qua email hoặc message

## Changelog

### Version 0.0.1-SNAPSHOT
- Initial project setup
- Basic authentication system
- Vaccination booking features
- Email notification service
- API documentation with Swagger/OpenAPI
- MongoDB integration

---

**Cập nhật lần cuối**: 11/05/2026

Cảm ơn bạn đã sử dụng Hệ thống Đặt Lịch Tiêm Chủng!
