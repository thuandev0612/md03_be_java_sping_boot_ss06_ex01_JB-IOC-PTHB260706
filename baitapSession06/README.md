# Session06 - Bài 1: Quan hệ thực thể bãi đỗ xe

Java 21, Spring Boot, JPA và PostgreSQL.

## Chạy

1. Mở project bằng IntelliJ, chọn JDK 21.
2. Chạy `BaitapSession06Application`.
3. Trong pgAdmin, mở database `parking_management_session06` → Schemas → public → Tables → Refresh.

Database và kết nối đã được chuẩn bị trên máy hiện tại. Mật khẩu nằm ngoài project tại `../.local-config/baitapSession06.properties`.

Máy khác cần tạo database bằng `CREATE DATABASE parking_management_session06;`, rồi đặt biến môi trường `DB_USERNAME`, `DB_PASSWORD` cho tài khoản PostgreSQL của máy đó. Có thể dùng `DB_URL` để đổi URL kết nối. Hibernate tự tạo bảng khi khởi động nhờ `ddl-auto=update`.

## Mapping

- `Zone` → `zones`: id, name, capacity, occupied_spots.
- `Vehicle` → `vehicles`: id, license_plate, color, type (CAR/BIKE).
- `ParkingTicket` → `parking_tickets`: id, check_in_time, check_out_time, vehicle_id, zone_id.
- Zone và Vehicle có `@OneToMany(mappedBy = ...)` trỏ về ParkingTicket.
- ParkingTicket dùng hai `@ManyToOne`, khóa ngoại vehicle_id và zone_id.
- check_out_time cho phép NULL khi xe chưa ra bãi.

Bài này thực hiện entity/mapping, chưa có API. Không cần có dữ liệu mẫu để Hibernate tạo bảng và khóa ngoại.
