# DTC245160031 — Website Quảng bá Sản phẩm

## 1. Thông tin sinh viên

- MSSV: DTC245160031
- GitHub: Thetai12
- Đề tài: Website Quảng bá Sản phẩm sử dụng WordPress

## 2. Giới thiệu

Dự án triển khai website quảng bá sản phẩm bằng WordPress và Docker Compose. Hệ thống sử dụng Nginx làm reverse proxy, Prometheus thu thập metrics, Grafana trực quan hóa dữ liệu, và Loki kết hợp Promtail để tập trung log.

## 3. Công nghệ sử dụng

- Docker và Docker Compose
- WordPress
- MySQL
- phpMyAdmin
- Nginx Reverse Proxy
- Prometheus
- Grafana
- Loki
- Promtail

## 4. Cấu trúc repository

```text
.
├── docker/
│   ├── docker-compose.yml
│   ├── nginx/default.conf
│   ├── prometheus/prometheus.yml
│   ├── grafana/provisioning/datasources/prometheus.yml
│   ├── loki/loki-config.yml
│   └── promtail/promtail-config.yml
├── docs/
├── screenshots/
├── .env.example
├── .gitignore
└── README.md
```

## 5. Cấu hình và khởi chạy

Yêu cầu: Docker và Docker Compose đã được cài đặt trên máy Linux.

1. Clone repository:

   ```bash
   git clone https://github.com/Thetai12/DTC245160031-wordpress-observability.git
   cd DTC245160031-wordpress-observability
   ```

2. Tạo file biến môi trường:

   ```bash
   cp docker/.env.example docker/.env
   ```

3. Mở `docker/.env`, thay các giá trị mẫu bằng mật khẩu mạnh và riêng biệt. Không commit file `.env` lên GitHub.

4. Kiểm tra cấu hình:

   ```bash
   cd docker
   docker-compose config -q
   ```

5. Khởi chạy các dịch vụ:

   ```bash
   docker-compose up -d
   ```

6. Kiểm tra container:

   ```bash
   docker-compose ps
   ```

Lưu ý: Cần bảo đảm các biến môi trường và cấu hình phù hợp với môi trường triển khai trước khi khởi chạy.

## 6. Địa chỉ truy cập khi triển khai trên máy hiện tại

- Website WordPress: http://192.168.131.128:8080
- Prometheus: http://192.168.131.128:9090
- Grafana: http://192.168.131.128:3000
- Loki API: http://192.168.131.128:3100
- phpMyAdmin: kiểm tra cổng đã publish trong cấu hình Compose thực tế.

Các địa chỉ trên phụ thuộc IP máy triển khai và cấu hình cổng. Tài khoản đăng nhập cần sử dụng thông tin đã cấu hình an toàn trong môi trường triển khai.

## 7. Giám sát và kiểm tra

- Prometheus: kiểm tra trạng thái target và truy vấn `up`.
- Grafana: sử dụng dashboard để trực quan hóa metrics.
- Loki: truy vấn log bằng LogQL.
- Promtail: thu thập và chuyển log đến Loki.

Ví dụ truy vấn LogQL:

```logql
{container=~".+"}
```

Lọc log chứa từ khóa lỗi:

```logql
{container=~".+"} |= "error"
```

Lọc log chứa từ khóa cảnh báo:

```logql
{container=~".+"} |= "warn"
```

Kết quả phụ thuộc vào log thực tế được thu thập trong khoảng thời gian chọn.

## 8. Minh chứng và báo cáo

Thư mục `screenshots/` dùng để lưu ảnh chụp thực tế của website, Docker, Prometheus, Grafana, Loki và GitHub.

Thư mục `docs/` dùng để lưu báo cáo và tài liệu triển khai.

## 9. Bảo mật

- Không commit mật khẩu thật, token, private key hoặc file `.env`.
- Chỉ đưa giá trị mẫu vào `.env.example`.
- Không công khai thông tin đăng nhập trong ảnh chụp hoặc báo cáo.
- Kiểm tra quyền truy cập và cấu hình cổng trước khi triển khai trên môi trường công khai.

## 10. Trạng thái dự án

Các dịch vụ chính đã được khởi chạy và kiểm tra tại môi trường phát triển. Cần kiểm thử lại toàn bộ luồng triển khai, thu thập metrics, thu thập log và các hướng dẫn trên một môi trường sạch trước khi xác nhận khả năng triển khai độc lập.

