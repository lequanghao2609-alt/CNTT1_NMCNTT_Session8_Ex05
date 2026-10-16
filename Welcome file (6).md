# BÀI 5: XÂY DỰNG BỘ TÀI LIỆU KĨ THUẬT CHO DỰ ÁN SMARTFARM

# Phần 1: Phân tích
### 1. Xác định Input/Ouput:


-   **Input:**
    -   Tín hiệu điện và thông số thô từ các cảm biến: Độ ẩm không khí, nhiệt độ, độ ẩm đất, cường độ ánh sáng, chỉ số EC/pH.
    -   Thao tác điều khiển trực tiếp từ ứng dụng của nông dân (bật/tắt bơm, cài đặt ngưỡng).
-   **Output;**
    -   Giao diện App Smart-Farm trực quan cho nông dân (màu xanh = Tốt, vàng = Cảnh báo, đỏ = Nguy hiểm).
    -   Lệnh kích hoạt thiết bị ngoại vi tự động: Rơ-le bật/tắt máy bơm phun sương, quạt thông gió, đèn quang hợp, mái che.
    -   Báo cáo lịch sử dữ liệu dạng biểu đồ và file xuất Excel/PDF.

### 2. Sơ đồ phối hợp phần cứng:

```
[Cảm biến DHT22 / Ánh sáng]
        │ (Thu thập dữ liệu thô)
        ▼
[SoC / Mạch điều khiển ESP32 / Raspberry Pi]
        │ (Xử lý ban đầu & Đóng gói)
        ▼
[Gateway / Router Internet]
        │ (Truyền tải dữ liệu)
        ▼
[Nền tảng Cloud Smart-Farm]
        ├──► [Ứng dụng trên Smartphone] (Hiển thị & Cảnh báo cho nông dân)
        └──► [Thiết bị điều khiển] (Tự động kích hoạt Bơm / Quạt / Đèn)

```


# PHẦN 3: KIỂM THỬ & XỬ LÝ SỰ CỐ (EDGE CASE: RAM BỊ ĐẦY)


### Quy trình xử lý an toàn cho nông dân & kỹ sư:

**HƯỚNG DẪN XỬ LÝ KHI BỘ NHỚ RAM BỊ ĐẦY:** > > 1. **Khởi chạy công cụ dọn dẹp bộ nhớ:** Chạy lệnh xóa nhật ký cũ để giải phóng RAM:    `smartfarm-cli clear-logs --days=7` > 2. **Khởi động lại ứng dụng       Smart-Farm:** `smartfarm-cli restart-service` > 3. **Xử lý thủ công      an toàn:** > - Ngắt nguồn điện máy bơm trước để tránh máy bơm chạy       liên tục ngoài ý muốn. > - Nhấn nút Reset cứng trên mạch SoC (hoặc       rút phích cắm nguồn 12V, chờ 10 giây rồi cắm lại). > - Tất cả cấu       hình ngưỡng tưới đã được lưu cố định trong bộ nhớ Flash nên sẽ **hoàn    toàn không bị mất**.

