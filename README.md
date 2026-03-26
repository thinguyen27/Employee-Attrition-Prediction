readme_content = """# 🏢 Dự đoán rủi ro nghỉ việc của nhân sự (IBM HR Analytics: Employee Attrition Prediction)

## 📖 Tổng quan dự án
Tình trạng nhân viên nghỉ việc (Attrition) không chỉ gây gián đoạn vận hành mà còn tiêu tốn nguồn lực khổng lồ cho việc tuyển dụng và đào tạo lại. Dự án này ứng dụng các kỹ thuật Phân tích dữ liệu (EDA) và Học máy (Machine Learning) để giải quyết bài toán nhân sự với hai mục tiêu cốt lõi:
1. **Dự báo sớm:** Nhận diện "Ai là người sắp nghỉ việc?" dựa trên các dữ liệu hành vi và nhân khẩu học.
2. **Phân tích nguyên nhân gốc rễ (Root Cause Analysis):** Trả lời câu hỏi "Tại sao họ lại rời đi?" nhằm giúp Ban lãnh đạo đưa ra chiến lược giữ chân nhân tài hiệu quả.

---

## 📊 Mô tả dữ liệu
* **Nguồn dữ liệu:** Bộ dữ liệu giả lập IBM HR Analytics Employee Attrition & Performance từ Kaggle.
* **Quy mô:** 1470 bản ghi, 35 thuộc tính.
* **Đặc điểm:** Dữ liệu hoàn toàn sạch (không có Null/NaN hay trùng lặp). Tỷ lệ nghỉ việc thực tế là **16.1%**, cho thấy sự mất cân bằng dữ liệu (Imbalanced Data).

---

## 🛠 Phương pháp và Kỹ thuật thực hiện

### 1. Kỹ thuật đặc trưng (Feature Engineering)
Thay vì chỉ dùng dữ liệu thô, dự án tập trung tạo ra các biến phái sinh mang đậm tính nghiệp vụ (Domain Knowledge):
* `Tenure_Ratio`: Tỷ lệ thời gian gắn bó tại công ty trên tổng thâm niên sự nghiệp.
* `Promotion_Stagnation`: Mức độ chững lại trong thăng tiến (Số năm không được thăng chức / Số năm làm việc).
* `Income_Age_Ratio`: Tỷ suất thu nhập trên tuổi đời.

### 2. Xử lý mất cân bằng dữ liệu (Handling Imbalanced Data)
Việc mô hình học máy thiên vị lớp đa số (người ở lại) là một rủi ro lớn. Dự án sử dụng thuật toán **SMOTENC** (Synthetic Minority Over-sampling Technique for Nominal and Continuous) trên tập Huấn luyện (Train set) để tạo ra các điểm dữ liệu tổng hợp cho nhóm nghỉ việc, giúp bảo toàn tính logic của các biến phân loại.

### 3. Lựa chọn và Đánh giá mô hình (Model Selection)
Triển khai song song 4 thuật toán để đối chiếu hiệu năng:
* Logistic Regression
* Random Forest Classifier (Tối ưu hóa siêu tham số với GridSearchCV)
* Support Vector Machine
