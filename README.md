# 🛡️ Dự án: Phát hiện Xâm nhập Mạng Thời gian Thực bằng Machine Learning

## 📌 Mô tả

Dự án xây dựng một hệ thống phát hiện xâm nhập mạng (IDS) hoạt động thời gian thực dựa trên mô hình học máy. Mục tiêu là phân tích dữ liệu mạng và phát hiện các gói tin bất thường hoặc có dấu hiệu tấn công, từ đó hỗ trợ cảnh báo sớm trong môi trường mạng nội bộ.

---

## 🧱 Kiến trúc tổng quan

1. **Thu thập dữ liệu:**
   - Dữ liệu huấn luyện: file `KDDTrain` (từ bộ dữ liệu NSL-KDD).
   - Dữ liệu giám sát thời gian thực: bắt trực tiếp từ card mạng bằng `Zeek`.

2. **Tiền xử lý:**
   - Loại bỏ cột dư thừa, mã hóa nhãn, chuẩn hóa đặc trưng.

3. **Huấn luyện mô hình:**
   - Mô hình sử dụng: **XGBoost**
   - Tinh chỉnh tham số bằng `GridSearchCV`
   - Lưu mô hình bằng `joblib` vào thư mục `models/`

4. **Giám sát thời gian thực:**
   - Bắt gói bằng `Zeek`, trích xuất đặc trưng, tính toán các đặc trưng còn thiếu  .
   - Áp dụng mô hình học máy đã huấn luyện để phân loại.
   - Dùng ELK Stack để lưu trữ , trực quan dữ liệu .
     

---

## 📘 Các kiến thức sử dụng

- **Học máy (Machine Learning):**
  - Mô hình XGBoost
  - Huấn luyện, đánh giá, lưu mô hình
- **Tiền xử lý dữ liệu:**
  - `pandas`, `scikit-learn`
- **Giám sát mạng:**
  - `Zeek` để đọc gói tin mạng
- **Lập trình Python:**
  - Tổ chức mã theo module
  - Giao tiếp giữa các file mã nguồn

- **Hệ thống SIEM:**
   - Elasticsearch : lưu trữ log , dữ liệu
   - Kibana: trực quan hóa dữ liệu
   - Filebeat : chuẩn hóa logs Zeek   

---



## 📂 Cấu trúc thư mục
```
IDS-using-Machine-Learning/
│
├── dataset/                # Thư mục chứa dữ liệu training 
│   ├── NSL-KDD/                        
│
├── models/                 # Các model đã train
│   ├── preprocessor.pkl    # Tiền xử lý
│   └── xgb_model.pkl       # Model XGBoost
│
├── src/                    # Mã nguồn chính
│   ├── __init__.py         # Khởi tạo package
│   ├── config.py           # Cấu hình
│   ├── preprocess.py       # Tiền xử lý dữ liệu
│   ├── train_model.py      # Training
│   ├── zeek_feature_extractor.py #Chuẩn hóa đặc trưng từ Zeek 
│   ├── explain_model.py    # Giải thích model (SHAP)
│   └── stream_monitor.py   # Giám sát real-time
│
├── logs/                   # File log (nên ignore)
│   └── app.log             # Log ứng dụng
│
├── venv/                  # Virtual Environment  
├── requirements.txt       # Thư viện cần thiết
├── main.py                # File chạy chính
└── README.md              # Mô tả dự án
```
