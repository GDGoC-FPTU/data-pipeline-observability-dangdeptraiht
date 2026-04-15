[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572416&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** haidanght291003@gmail.com
**Name:** Nguyen Hai Dang

---

## Mo ta

Bài lab này yêu cầu xây dựng một ETL pipeline đơn giản để trích xuất dữ liệu từ file JSON (`raw_data.json`), kiểm tra tính hợp lệ của dữ liệu (loại bỏ giá âm và danh mục trống), chuyển đổi định dạng theo yêu cầu (tính giá sau giảm, chuẩn hóa tên danh mục), và lưu kết quả cuối cùng ra file CSV (`processed_data.csv`). Ngoài ra, tôi cũng đã thực hiện stress test bằng cách sinh dữ liệu tạp và đánh giá phản hồi của AI/RAG Agent khi xử lý kết quả nhiễu.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Tao file garbage_data.csv
python generate_garbage.py

# Mo phong Agent de kiem tra su khac biet
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

- **Trích xuất:** Đã load thành công toàn bộ records từ thư mục nguồn.
- **Làm sạch (Validation):** Đã loại bỏ các record lỗi (như giá < 0 hoặc category rỗng).
- **Chuyển đổi (Transform):** Xử lý giảm 10% giá sản phẩm và chuyển category thành định dạng Title Case.
- **Tải (Load):** Lưu toàn bộ dữ liệu hợp lệ ra `processed_data.csv`. Quá trình kiểm nghiệm mô phỏng Agent cho thấy sự suy giảm đáng kể độ chính xác khi dùng dữ liệu đầu vào chứa nhiều dạng nhiễu (garbage data).
