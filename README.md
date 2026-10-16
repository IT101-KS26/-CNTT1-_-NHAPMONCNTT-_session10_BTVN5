# Bài tập thực hành 
### 5.Yêu cầu đầu ra
**Phần 1**.**Phân tích**: Xác định Input/Output và sơ đồ phối hợp phần cứng của hệ thống trang trại 
- Input: dự án "Smart-Farm" tích hơp IoT 
- Cảm biến độ ẩm đất 
- cảm biến ảnh sáng 
- Cảm biến nhiệt độ và độ ẩm không khí 
- Output: 
- máy bơm nước mini: Thực hiện tưới nước khi độ ẩm thấp 
- Màn hình led còi báo động: hiển thị trạng thái và cảnh báo khi có sự cố 

**2.Sơ đồ phối hợp phần cứng của hệ thống trang trại**:
- Hệ thống trang trại hoạt trên mô hình IPO:

Input: Các cảm biến thu thập dữ liệu thô từ môi trường (Độ ẩm, nhiệt độ) gửi về SoC.

Process: Vi điều khiển xử lý tín hiệu, so sánh với ngưỡng cài đặt, quyết định xem có cần kích hoạt lệnh tưới hay không.

Output: SoC truyền tín hiệu điện qua mạch chuyển mạch (Relay) để kích hoạt máy bơm nước hoạt động.

***Phần 2***:***Triển khai***- File [README.md](http://README.md) hoàn chỉnh theo chuẩn kỹ sư phần mềm chuyên nghiệp.

#  Dự án Smart-Farm (Hệ thống Tự động hóa Vườn Lan IoT)

> Giải pháp công nghệ thông minh ứng dụng Internet of Things (IoT) nhằm tối ưu hóa quy trình chăm sóc và tưới tiêu tự động cho trang trại lan.

---

## Hướng dẫn cài đặt

```bash
# 1. Clone repository dự án về máy
git clone [link](https://github.com/username/Smart-Farm.git)

# 2. Di chuyển vào thư mục dự án
cd Smart-Farm

# 3. Cài đặt thư viện và upload mã nguồn lên bo mạch SoC
pio run --target upload
```
***Phần 3***:- Giả định RAM bị đầy dữ liệu nhật ký, hãy cập nhật mục "Lưu ý" trong README cách xử lý an toàn.

Bổ sung phần sau vào mục **"Lưu ý & Xử lý sự cố"** trong tài liệu:

```markdown
## ⚠️ Lưu ý & Xử lý sự cố: Tràn bộ nhớ RAM do dữ liệu nhật ký (Log)

* **Vấn đề:** Lưu trữ quá nhiều nhật ký hoạt động trực tiếp trên RAM sẽ làm thiết bị nhanh chóng bị tràn bộ nhớ, dẫn đến hiện tượng treo máy hoặc khởi động lại liên tục.
* **Cách xử lý an toàn:**
  1. **Cơ chế Ring Buffer:** Giới hạn dung lượng lưu log trên RAM (chỉ giữ lại các dòng log gần nhất), tự động ghi đè khi đầy.
  2. **Ghi định kỳ ra bộ nhớ Flash (SPIFFS / LittleFS):** Xả (flush) dữ liệu log xuống bộ nhớ ngoài thay vì giữ toàn bộ trên RAM.
  3. **Cơ chế Watchdog Timer (WDT):** Tự động khởi động lại SoC an toàn nếu phát hiện tiến trình bị kẹt do tràn bộ nhớ.
