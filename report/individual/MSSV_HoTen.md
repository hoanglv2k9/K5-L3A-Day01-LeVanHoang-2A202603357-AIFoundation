# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:**
- **Họ và tên:**
- **SEED** (in ở ô đầu notebook):

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☐ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính

*Chép bảng so sánh cuối Phần 5 (F1 test, F1 SUB 40, p95 ms/tin, USD/1k tin) của chính bạn.*
Mô hình	F1 Test	F1 SUB 40	p95 (ms/tin)
BoW + LogReg	0.886	0.889	0.147
BoW + MLP	0.935	0.974	0.605
MiniLM + kNN	0.924	1.000	70.215
MiniLM + LogReg	0.963	0.974	39.361
MiniLM + MLP Head	0.974	1.000	39.969

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*
Tin nhắn ngụy trang: BoW đúng 4/6, Embedding + LogReg đúng 6/6.

Stress test: BoW + LogReg đạt accuracy 0.48, thấp hơn dự đoán ban đầu.

LLM: không có kết quả thực nghiệm vì notebook không có API key.

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*

Embedding + kNN tốt nhất với accuracy 0.70 và F1 0.746. BoW + LogReg giảm mạnh, F1 còn 0.278. Các mô hình thường nhầm spam giả giọng tin nhắn cá nhân và tin ham có từ khóa như “free”, “win”, OTP.

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*
SEED 6004 tương ứng Đề #5 — Embedding. Tôi tạo 2 tin spam né từ khóa và 2 tin ham có từ “free” hoặc “win”. Cell 96 chưa có output nên chưa thể kết luận mô hình nào dự đoán đúng hơn.

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

Chọn BoW + MLP nếu ưu tiên tốc độ (p95 = 0.605 ms); chọn MiniLM + MLP Head nếu ưu tiên F1 (0.974, p95 = 39.969 ms). Với 10 triệu tin/ngày cần kiểm thử tải và mở rộng nhiều máy; số đo notebook chưa chứng minh một máy đáp ứng đủ lưu lượng.

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*

Tôi dùng AI để tổng hợp kết quả và trình bày báo cáo, sau đó đối chiếu lại với output notebook. Qua bài lab, tôi hiểu BoW dựa vào từ khóa nên dễ sai khi câu chữ bị biến đổi hoặc thay đổi ngữ cảnh; Embedding hiểu ngữ nghĩa tốt hơn nhưng tốn thời gian xử lý hơn. Điểm số trên tập test thông thường chưa đảm bảo mô hình xử lý tốt các tình huống spam khó.
