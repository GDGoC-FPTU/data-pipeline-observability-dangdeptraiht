# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600157
**Name:** Nguyen Hai Dang
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200.0. | 10 | Trả lời chính xác và tự tin |
| Garbage Data (`garbage_data.csv`) | Agent Error: I'm choking on the data! (could not convert string to float: 'ten dollars') | 1 | Agent gặp lỗi crash khi xử lý chuỗi ở cột giá |

---

## 2. Phan tich & nhan xet

### Tại sao Agent trả lời sai hoặc gặp lỗi khi dùng Garbage Data?

Agent gặp lỗi do chất lượng dữ liệu kém ("garbage data") gây ra các vấn đề nghiêm trọng:
1. **Wrong Data Types:** Dữ liệu chứa chuỗi ("ten dollars") ở cột giá (price) vốn yêu cầu kiểu số, khiến panda không thể chuyển đổi kiểu dữ liệu hiệu quả và gây crash.
2. **Extreme Outliers:** Dù Agent không bị crash bởi lỗi này trong kịch bản test nhưng khi tìm "highest price", giá trị ngoại lai khổng lồ như "Nuclear Reactor" ở giá 999999 có thể khiến kết quả gợi ý bị sai lệch hoàn toàn so với thực tế.
3. **Null Values & Duplicates:** Việc thiếu kiểm soát dữ liệu dẫn đến dữ liệu rỗng (null) hoặc trùng lặp ID làm loạn quá trình truy xuất dữ liệu nội bộ.
Như vậy, sự thiếu sót bước Validate và Clean trong ETL pipeline đã làm hỏng hoàn toàn RAG simulation.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Đồng ý)

Tôi hoàn toàn đồng ý. Một prompt dù chi tiết và tuyệt vời đến đâu cũng không thể khắc phục được những dữ liệu đầu vào bị lỗi cú pháp, sai kiểu dữ liệu hay nhiễm các giá trị ngoại lai. Mô hình ngôn ngữ hay Agent sẽ chỉ tốt khi dữ liệu dùng để RAG (Retrieval-Augmented Generation) đáp ứng đủ tiêu chuẩn chất lượng. Việc làm sạch dữ liệu trước khi đưa vào Agent là cốt lõi để đảm bảo hệ thống AI bảo đảm độ chính xác.
