# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Ở `temperature` thấp như 0.0 và 0.5, câu trả lời ổn định hơn, khá giống nhau về cấu trúc và thiên về thông tin an toàn, quen thuộc. Khi tăng lên 1.0 và 1.5, cách diễn đạt đa dạng hơn và chọn chi tiết linh hoạt hơn, nhưng với prompt mang tính sự thật như câu này thì khác biệt không quá lớn. Nói ngắn gọn, temperature càng cao thì mức độ ngẫu nhiên và sáng tạo càng tăng, còn độ nhất quán thường giảm.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt khoảng `0.2–0.4`, ví dụ `0.3`, vì chatbot hỗ trợ khách hàng cần câu trả lời nhất quán, rõ ràng và ít bịa đặt hơn là quá sáng tạo. Mức này vẫn đủ tự nhiên khi diễn đạt, nhưng giảm rủi ro trả lời lan man hoặc không đúng chính sách.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Khoảng `33,3 lần`. Với 10.000 người dùng × 3 lần gọi/ngày × 350 token, tổng workload là khoảng `10,5 triệu token/ngày`; theo bảng giá trong `template.py`, GPT-4o vào khoảng `$131,25/ngày` còn GPT-4o-mini khoảng `$3,94/ngày` nếu giả sử input/output chia tương đối đều.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi xử lý các yêu cầu phức tạp, nhiều ngữ cảnh và cần chất lượng trả lời rất cao, ví dụ hỗ trợ khách hàng cho các ca escalated hoặc tư vấn sản phẩm quan trọng. GPT-4o-mini phù hợp hơn cho FAQ, tóm tắt, phân loại, hoặc chatbot lưu lượng lớn nơi tốc độ và chi phí quan trọng hơn sự khác biệt nhỏ về chất lượng.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các trải nghiệm tương tác trực tiếp như chatbot, trợ lý viết, hoặc coding assistant, nơi người dùng đang chờ phản hồi và việc thấy câu trả lời hiện dần sẽ làm cảm giác nhanh hơn nhiều, giảm sốt ruột và tăng tính “đối thoại”. Ngược lại, non-streaming phù hợp hơn khi hệ thống cần nhận toàn bộ kết quả rồi mới xử lý tiếp, chẳng hạn kiểm duyệt nội dung, parse JSON, lưu log hoàn chỉnh, hoặc chạy các tác vụ nền mà người dùng không cần theo dõi từng token xuất hiện.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
