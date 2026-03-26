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
* Support Vector Machine (SVM)
* Neural Network (MLPClassifier)

**Tiêu chí đánh giá:** Trọng tâm được đặt vào **Recall** (Độ phủ rủi ro) và **F1-Score** cho lớp thiểu số (Nghỉ việc), thay vì Accuracy tổng thể, nhằm tối thiểu hóa rủi ro "bỏ lọt" nhân sự sắp nghỉ.

---

## 📈 Kết quả nổi bật

* **Mô hình triển khai chính (Dự báo):** **Logistic Regression** đạt hiệu năng tối ưu nhất trên tập kiểm thử với F1-Score: 0.460 và Recall: 0.426 (tăng gấp 4 lần so với khi chưa dùng SMOTENC). 
* **Mô hình phân tích nguyên nhân:** Giữ lại **Random Forest** để trích xuất `Feature Importance`.
* **Insights kinh doanh:** * Quyền lợi tài chính dài hạn (StockOptionLevel) là yếu tố giữ chân nhân sự mạnh nhất.
  * Sự hài lòng về môi trường/công việc và xung đột với quản lý trực tiếp đóng vai trò then chốt.
  * Nhân sự thường xuyên phải làm thêm giờ (OverTime) có tỷ lệ nghỉ việc cao bất thường.

---

## 🚀 Đóng gói và Triển khai (Deployment)
Dự án được thiết kế dưới dạng một luồng phân tích hoàn chỉnh (Pipeline), sẵn sàng tích hợp vào hệ thống doanh nghiệp:
1. Xuất tập dữ liệu sau xử lý (`HR_Attrition_Advanced_for_PowerBI.csv`) cung cấp Data Source sạch cho đội ngũ BI xây dựng Dashboard.
2. Lưu trữ toàn bộ mô hình (`.pkl` files) và bộ chuẩn hóa (`StandardScaler`) để đội ngũ IT có thể nhúng trực tiếp API vào hệ thống Quản trị Nhân sự (HRIS).

---

## 💻 Tech Stack
* **Ngôn ngữ:** Python
* **Thư viện thao tác dữ liệu:** Pandas, NumPy
* **Trực quan hóa:** Matplotlib, Seaborn
* **Học máy (Machine Learning):** Scikit-learn (Logistic Regression, Random Forest, SVM, MLP, GridSearchCV)
* **Xử lý dữ liệu mất cân bằng:** Imbalanced-learn (SMOTENC)

---

## 👨‍💻 Thông tin tác giả
**Quốc Thi** *Sinh viên năm 3, chuyên ngành Hệ thống Thông tin* *University of Technology and Engineering (GPA: 3.26)* Dự án được xây dựng với tư duy kết hợp chặt chẽ giữa khả năng lập trình mô hình học máy và tư duy phân tích nghiệp vụ, định hướng ứng dụng thực tiễn trong mảng Data Analytics.
"""

# Tạo và ghi file README.md
with open("README.md", "w", encoding="utf-8") as file:
    file.write(readme_content)

print("✅ Đã tạo thành công file README.md trong thư mục hiện tại!")
