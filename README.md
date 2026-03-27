#  Đại Học Lạc Hồng - 🧠 Lab NLP: Tự động gán nhãn & phân tách từ cho bình luận Facebook tiếng Việt
Cơ Sở Ngôn Ngữ Học – Hỗ Trợ Xử Lý Ngôn Ngữ Tiếng Việt

**Thông tin sinh viên:**

| STT | Mã Số Sinh Viên | Họ và Tên            |
|-----|-----------------|----------------------|
| 1   | 123000007       | Trần Văn Hội         |
| 2   |                 |                      |

## Mô tả dự án
Ứng dụng Streamlit sử dụng thư viện **underthesea** để xử lý ngôn ngữ tự nhiên tiếng Việt: phân tách từ (word segmentation), gán nhãn cảm xúc (sentiment analysis) và phát hiện spam trên tập bình luận Facebook.

---

## 📁 Cấu trúc thư mục

```
.
├── app_auto_label.py                  # File ứng dụng chính (đã hoàn thành TODO)
├── app_auto_label_todo.py             # File bài tập gốc (sinh viên tự làm)
├── facebook_comments_vi_unlabeled.csv # Dữ liệu mẫu (3500 bình luận tiếng Việt)
└── README.md                          # File hướng dẫn này
```

---

## ⚙️ Yêu cầu hệ thống

- Python >= 3.8
- pip

---

## 🚀 Cài đặt

**1. Clone hoặc tải project về máy**

**2. Cài đặt các thư viện cần thiết**

```bash
pip install streamlit pandas underthesea
```

> Lần đầu chạy, `underthesea` sẽ tự động tải model về máy. Cần kết nối Internet.

---

## ▶️ Chạy ứng dụng

```bash
streamlit run app_auto_label.py
```

Trình duyệt sẽ tự mở tại `http://localhost:8501`.

---

## 🗂️ Định dạng file CSV đầu vào

File CSV phải có **đúng hai cột**:

| Cột  | Mô tả                     |
|------|---------------------------|
| `id` | Mã định danh bình luận    |
| `text` | Nội dung bình luận tiếng Việt |

Ví dụ:

```csv
id,text
1,"Khóa học rất hay, mình rất hài lòng!"
2,"Dịch vụ kém quá, không recommend."
3,"Inbox mình để nhận ưu đãi giá rẻ nhé!"
```

---

## 🔍 Các tính năng chính

### 1. Phân tách từ (Word Segmentation)
Sử dụng `word_tokenize` của underthesea để tách từ ghép tiếng Việt.

```
"học tiếng Anh" → "học tiếng_Anh"
```

### 2. Gán nhãn cảm xúc (Sentiment Analysis)
Sử dụng `sentiment` của underthesea, phân loại mỗi bình luận thành:

| Nhãn tiếng Anh | Nhãn tiếng Việt |
|----------------|-----------------|
| `positive`     | Tích cực        |
| `negative`     | Tiêu cực        |
| `neutral`      | Trung lập       |

### 3. Phát hiện Spam
Hàm `detect_spam()` kiểm tra 4 tiêu chí:

| Tiêu chí | Ví dụ |
|----------|-------|
| Chứa link | `http://bit.ly/abc`, `www.example.com` |
| Chứa số điện thoại | `0912345678` |
| Từ khóa quảng cáo | `inbox`, `giá rẻ`, `tăng like`, `miễn phí` |
| Ký tự lặp bất thường | `aaaaaaa`, `!!!!!!` |

---

## 📊 Kết quả đầu ra

Sau khi xử lý, ứng dụng hiển thị:
- **Biểu đồ thống kê** phân bố cảm xúc và tỉ lệ spam
- **Bảng kết quả** chi tiết với các cột:

| Cột | Mô tả |
|-----|-------|
| `id` | ID bình luận |
| `text` | Văn bản gốc |
| `tokenized` | Văn bản sau phân tách từ |
| `spam_label` | `spam` / `không spam` |
| `spam_label_vn` | `Spam` / `Không spam` |
| `sentiment_label` | `positive` / `negative` / `neutral` |
| `sentiment_label_vn` | `Tích cực` / `Tiêu cực` / `Trung lập` |

- **Nút tải về** file CSV kết quả (`auto_labels_output.csv`)

---

## 📝 Hướng dẫn làm bài tập (TODO)

Mở file `app_auto_label_todo.py`, tìm các dòng `# TODO` và hoàn thành theo thứ tự:

| TODO | Nội dung |
|------|----------|
| 1 | Import `word_tokenize`, `sentiment` từ `underthesea` |
| 2 | Regex phát hiện link |
| 3 | Regex phát hiện số điện thoại |
| 4 | Danh sách từ khóa spam |
| 5 | Regex phát hiện ký tự lặp |
| 6 | `st.file_uploader()` |
| 7 | `pd.read_csv()` |
| 8 | Kiểm tra cột `id`, `text` |
| 9 | `word_tokenize(text, format="text")` |
| 10 | `sentiment(text)` |
| 11 | Tạo cột `spam` |
| 12 | Tạo cột `spam_label` |
| 13 | Tạo cột `spam_label_vn` |
| 14 | Map sang `sentiment_label_vn` tiếng Việt |
| 15 | Hiển thị biểu đồ thống kê |
| 16 | Nút download CSV |

---

## 📚 Tài liệu tham khảo

- [underthesea GitHub](https://github.com/undertheseanlp/underthesea)
- [Streamlit Documentation](https://docs.streamlit.io)
- [pandas Documentation](https://pandas.pydata.org/docs)
