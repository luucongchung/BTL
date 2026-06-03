# BTL

# T2 — PoseAlert: Cảnh báo tư thế ngồi học

Dự án thuộc môn học **Nhập môn AIoT**, sử dụng trí tuệ nhân tạo để nhận diện và đưa ra cảnh báo khi người dùng ngồi học sai tư thế qua camera.

---

## 📦 Demo1.html: Khởi tạo dự án & Kết nối Teachable Machine

tập trung vào việc thiết lập nền tảng và thử nghiệm kết nối mô hình AI.

### Các công việc đã hoàn thành:
* **Khởi tạo cấu trúc:** Tạo bộ khung HTML cơ bản cho ứng dụng (`demo1.html`).
* **Tích hợp Camera:** Kích hoạt thành công tính năng mở camera/webcam trực tiếp trên trình duyệt.
* **Kết nối AI Model:** Tích hợp và kết nối thành công với mô hình nhận diện tư thế (Pose Model) từ Teachable Machine.
* **Đọc dữ liệu:** Trích xuất và in ra được các kết quả dự đoán (nhận diện) của AI trên giao diện.
* Phiên bản này hiện tại chưa có logic xử lý cảnh báo nâng cao và chưa được tối ưu giao diện (CSS).*
## Bản 2: Vẽ khung xương (Skeleton) & Logic phân loại cơ bản

Phiên bản này tập trung vào việc trực quan hóa bộ khung xương người dùng và xử lý logic để phân biệt tư thế ngồi đúng/sai theo thời gian thực.

### Các công việc đã hoàn thành:
* **Hiển thị khung xương:** Triển khai hàm `drawPose` kết hợp với Canvas để vẽ các điểm chốt (keypoints) và đường nối xương (skeleton) trực tiếp lên luồng video từ webcam.
* **Xây dựng logic phân loại tư thế:** Viết hàm `handlePostureLogic` để bắt nhãn có tỷ lệ chính xác cao nhất từ mô hình Teachable Machine và xử lý giao diện:
  * Nếu kết quả trùng với nhãn "Ngồi đúng" hoặc "Normal": Cập nhật trạng thái thành "Tư thế chuẩn" (chữ màu xanh).
  * Nếu rơi vào các nhãn khác: Báo lỗi "Sai tư thế" kèm theo tên tư thế sai cụ thể (chữ màu đỏ).
* **Tối ưu luồng xử lý:** Sử dụng `window.requestAnimationFrame` để duy trì vòng lặp cập nhật liên tục từ webcam và đưa vào mô hình nhận diện mà không gây giật lag trình duyệt.
