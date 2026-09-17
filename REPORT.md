# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602060
- Ngày / CVAT local: 17/09/2026 — http://localhost:8080
- Công cụ đã dùng: CVAT local; kiểm cấu trúc export bằng `scripts/inspect_submissions.py`.

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | chưa có ZIP | chưa xác nhận / 1 | 3 |
| cp2_slice | chưa có ZIP | chưa xác nhận / 1 | 3 |
| cp5_occlusion | chưa có ZIP | chưa xác nhận / 1 | 3 |
| cp3_thin | chưa có ZIP | chưa xác nhận / 1 | 3 |
| cp4_curb | chưa có ZIP | chưa xác nhận / 1 | 3 |
| cp6_coverage | chưa có ZIP | chưa xác nhận / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

**Trạng thái hiện tại:** Đã nhận đủ export ba tier (8 ảnh). Sáu checkpoint chưa có ZIP trong bản nộp hiện tại; chưa xác nhận trạng thái annotation. Mục 2 và mục 4 cần người làm bài cung cấp thông tin thật trước khi nộp VLearn. Kiểm cấu trúc chỉ xác nhận hợp đồng file, không xác nhận mask đúng.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: …
- Class và quy tắc tôi dùng để chọn biên: …
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: …
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Gói nộp `2A202602060-LENGOCNAM.zip`, ba thư mục tier.
- Lỗi thuộc loại: khác — nhầm task/định dạng khi đóng gói kết quả.
- Bằng chứng tôi nhìn thấy: `easy_semantic/` chứa COCO keypoints Day 4 với ảnh `train_01.jpg`–`train_20.jpg`; `medium_instance/` chứa ba mask semantic Easy; `hard_panoptic/` chứa ba ảnh COCO Medium thay vì hai ảnh Hard.
- Quy tắc và hành động sửa: Đối chiếu tên ảnh, lớp và định dạng với từng task. Dùng đúng export CVAT job 8 cho `easy_semantic.zip`, job 9 cho `medium_instance.zip`, job 10 cho `hard_panoptic.zip`; đặt ba ZIP vào `submissions/`. Nội dung ZIP giữ nguyên byte từ các bản export gốc.
- Sau sửa đã Save và export lại chưa? Ba tier đã được vẽ và export từ CVAT. Lượt sửa này sửa cách chọn, đặt tên và vị trí ZIP nộp; dùng các bản export đã có. Kiểm cấu trúc ba ZIP: 0 lỗi; Medium có 9 mask trên 3 ảnh, Hard có 72 mask trên 2 ảnh. Chất lượng biên, số vật và phủ vùng cần kiểm trực quan.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | … | … | … |
| 2 | … | … | … |
| 3 | … | … | … |
