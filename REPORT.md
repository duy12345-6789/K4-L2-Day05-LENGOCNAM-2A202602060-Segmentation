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

- Task/ảnh/vùng: `medium_instance`, ba ảnh `000000181542.jpg`, `000000373353.jpg`, `000000458325.jpg`.
- Lỗi thuộc loại: thiếu vật trong bản nộp trước rework; cần kiểm tách từng instance.
- Bằng chứng: Bản export trước có 9 mask, trong khi gói đáp án được cung cấp có 71 object. Mỗi người hoặc xe nhìn thấy cần một instance riêng; một mask theo lớp không thay cho nhiều vật.
- Quy tắc và hành động sửa: Nhận và thay bằng `medium_instance.zip` mới, gồm 84 mask trên đúng ba ảnh và sáu lớp, format COCO 1.0. Giữ nguyên nội dung bản export CVAT; chỉ đổi bản ZIP được nộp. Số mask mới theo ảnh là 30, 26, 28; chỉ số đối chiếu được tính lại bằng cùng scorer và cùng gói đáp án.
- Sau sửa đã Save và export lại chưa? Đã có bản export mới. Ba ZIP tier đạt kiểm cấu trúc với 0 lỗi. Easy và Hard giữ nguyên bản export trước.

| Chỉ số đối chiếu cục bộ | Trước thay Medium | Sau thay Medium |
| --- | ---: | ---: |
| Mask Medium | 9 | 84 |
| Metric Medium (mean matched IoU × recall) | 0,034 | 0,559 |
| Điểm Medium | 0/32 | 11,3/32 |
| Tổng ba tier | 30,3/82 | 41,6/82 |

[Scorecard hiện tại](reports/local_evaluation/SCORECARD.md) và [mốc trước rework](reports/local_evaluation/history/before_medium_rework/SCORECARD.md). Easy vẫn 18,4/20 (metric 0,815); Hard vẫn 11,9/30 (PQ 0,378).

**Kết quả còn cần QC:** Medium có 52 mask khớp tại IoU ≥ 0,5, mean matched IoU 0,763, precision 0,619, recall 0,732. Còn 32 mask nộp chưa khớp và 19 object tham chiếu chưa khớp. Các số này giúp tìm thiếu vật, sai lớp, trùng vật hoặc lệch biên; chưa đủ để quyết định xóa mask nào. Chín mask gốc vẫn có trong bản mới cùng 75 mask bổ sung, nên cần kiểm trực quan chồng lấn và định danh object.

Đây là phản hồi cục bộ sau khi nhận `tiers_gt.zip`, không phải điểm chính thức hay bằng chứng chất lượng bản làm độc lập trước lúc xem đáp án. GitHub Actions dùng workflow sẵn có và chờ release đáp án chính thức; [lần chạy thủ công đã kiểm](https://github.com/duy12345-6789/K4-L2-Day05-LENGOCNAM-2A202602060-Segmentation/actions/runs/35212450941) thành công nhưng bỏ qua chấm điểm.

Lỗi đóng gói ban đầu cũng đã sửa: `easy_semantic/` chứa bài Pose Day 4, `medium_instance/` chứa Easy, `hard_panoptic/` chứa Medium. Bản nộp hiện tại dùng ZIP đúng task trong `submissions/`. Gói đáp án được giữ ngoài fork. Sáu checkpoint chưa có ZIP; mục 2 và mục 4 vẫn cần thông tin thực tế từ người làm bài. PASS, bonus và top 3 do người phụ trách xác nhận.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | … | … | … |
| 2 | … | … | … |
| 3 | … | … | … |
