# Báo cáo Day 5 — 2A202602060

- Mã học viên theo lớp: **2A202602060**.
- Ngày / CVAT local: **17/09/2026 — http://localhost:8080**.
- Bản export dùng trong báo cáo: **DAY05-2A202602060-LENGOCNAM.zip**, bản mới nhất được cung cấp.
- Nơi lưu ZIP và kết quả kiểm: [fork GitHub cá nhân](https://github.com/duy12345-6789/K4-L2-Day05-LENGOCNAM-2A202602060-Segmentation). Bảng bài nộp bên dưới mô tả file trong fork; thư mục tải về trên máy chỉ được cập nhật hai tài liệu ở lượt này.
- Công cụ đã dùng: **CVAT local và gợi ý tự động**, theo thông tin người làm bài đã cung cấp. Chưa xác nhận công cụ vẽ tay cụ thể là Brush hay Polygon; bản export không lưu thông tin này.
- Công cụ QC: `scripts/inspect_submissions.py` và scorer nguyên bản của starter. Điểm dưới đây là đối chiếu cục bộ với `tiers_gt.zip` được cung cấp, sau khi đã nhận gói đáp án.

## 1. Bài đã nộp

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

Theo xác nhận của người làm bài, đã vẽ và export ba tier; bản mới nhất có nhãn cho đủ 8 ảnh. Sáu checkpoint chưa có ZIP trong gói mới nhất; không xác nhận đã hoàn thành những trạm này. Ba tier qua kiểm cấu trúc với **0 lỗi** về tên ảnh, danh sách lớp và cấu trúc export. Hard có mask RLE trong COCO 1.0; kiểm cấu trúc không chứng minh các vùng panoptic không chồng lấn, phủ đủ, đúng số object hoặc đúng biên.

Đã kiểm trực tiếp `data/checkpoints/`: mỗi trạm chỉ có một JPG, `classes.json` và `cvat-labels.json`. Hai JSON định nghĩa lớp để tạo task CVAT, **không chứa mask đã vẽ**. Thư mục này là đầu vào sáu checkpoint, không phải ZIP bài làm. Xem [phiếu quy tắc và danh sách export checkpoint](guideline-mini-sheet.md).

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: **chưa xác nhận**. Bản COCO hiện tại có mask và thuộc tính `occluded`, nhưng không lưu nguồn manual/auto hoặc thứ tự xem gợi ý đủ để chứng minh bước này.
- Class và quy tắc tôi dùng để chọn biên của object đó: **chưa có thông tin xác nhận từ người làm bài**. Không suy ra từ ID annotation hoặc số liệu evaluator.
- Nếu dùng gợi ý sau đó: người làm bài đã cho biết có sử dụng model, nhưng **chưa xác nhận vùng đề xuất cụ thể đã sửa/giữ và lý do**. Chỉ số của bản export cuối không chứng minh quyết định trước khi xem gợi ý.
- Quy tắc dùng trong lượt QC hiện tại: mỗi người/xe nhìn thấy là một instance riêng; các mảnh nhìn thấy của cùng một vật bị che giữ chung một instance; chỉ vẽ phần nhìn thấy. Đây là quy tắc kiểm bản export mới, không phải xác nhận đã làm bước tự vẽ trước model.

Mục này cần người làm bài xác nhận theo trải nghiệm thực tế trước khi nộp cuối.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: **cách nộp ZIP của ba tier**, áp dụng toàn bộ 8 ảnh trong gói mới nhất.
- Lỗi thuộc loại: **khác — tên và vị trí file nộp chưa khớp hợp đồng starter**. Gói tổng chứa ba thư mục `essy/`, `medium/`, `hard/`; các native export tương ứng mang tên `essy.zip`, `medium.zip`, `hard.zip`.
- Bằng chứng tôi nhìn thấy: đối chiếu nội dung gói tổng với từng native export; byte của JSON/PNG khớp chính xác. Native export Easy là Segmentation mask 1.1; Medium và Hard là COCO 1.0.
- Quy tắc và hành động sửa: đặt ba ZIP đúng tên `easy_semantic.zip`, `medium_instance.zip`, `hard_panoptic.zip` vào `submissions/`. **Giữ nguyên byte của các bản export CVAT**, không chỉnh JSON/PNG bên trong.
- Sau sửa đã Save và export lại chưa? Đã dùng bản export mới do người làm bài cung cấp; lần sửa tên/vị trí file này không thay đổi nhãn nên không cần export lại. Chưa có bằng chứng xác nhận một lỗi mask cụ thể đã được sửa trong CVAT ở lượt QC này.

Kết quả liên quan lỗi đóng gói đã sửa: ba tier có **0 lỗi cấu trúc**, ZIP đã đúng tên trong `submissions/` của fork. Medium có **112 mask** trên ba ảnh; Hard có **99 mask** trên hai ảnh. Việc đổi tên/vị trí ZIP giữ nguyên mask nên không làm tăng chỉ số segmentation. Nếu coach yêu cầu lỗi annotation đã sửa, cần bổ sung một lỗi và hành động thực tế trong CVAT.

[Scorecard của bản mới nhất trên fork](https://github.com/duy12345-6789/K4-L2-Day05-LENGOCNAM-2A202602060-Segmentation/blob/main/reports/local_evaluation/SCORECARD.md):

| Tier | Metric | Điểm đối chiếu cục bộ |
| --- | ---: | ---: |
| Easy semantic | mIoU 0,820 | 18,7 / 20 |
| Medium instance | mean matched IoU × recall 0,588 | 13,3 / 32 |
| Hard panoptic | PQ 0,391 | 12,7 / 30 |
| **Tổng ba tier** | | **44,7 / 82** |

**Những điểm còn cần QC trong bản mới nhất:**

- Easy: coverage 89,4%; vegetation có IoU 0,589, thấp nhất trong năm lớp.
- Medium: 55 mask khớp tại IoU ≥ 0,5, 57 mask nộp chưa khớp, 16 object tham chiếu chưa khớp. Mean matched IoU 0,759, precision 49,1%, recall 77,5%.
- Hard: car có 24 segment khớp, 45 chưa khớp; sidewalk có 0 khớp, 2 mask nộp và 2 segment tham chiếu chưa khớp; bicycle có 1 segment tham chiếu chưa khớp và chưa có annotation nộp. Kiểm mask cùng một vật chồng nhau, sai lớp, thiếu vùng hoặc lệch biên; không tự động xóa mọi mask chưa khớp.

Đây là điểm đối chiếu sau khi đã nhận gói đáp án, không phải điểm chính thức, PASS, bonus hoặc top 3. Chỉ số không chứng minh chất lượng bản làm độc lập trước lúc xem đáp án. GitHub Actions dùng workflow sẵn có để kiểm cấu trúc; bước chấm /82 phụ thuộc release đáp án chính thức của repo lớp. Gói `tiers_gt.zip` được giữ ngoài fork; chỉ ZIP annotation và báo cáo được nộp.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Các ca dưới đây được ghi từ **lượt QC hiện tại** trên ảnh và bản export mới; không diễn giải thành lịch sử tự annotation trước model.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Hard `000000460147.jpg`, xe chở xe ở giữa tiền cảnh | Toàn bộ cụm là một truck / các xe được chở là car riêng cùng phần truck nhìn thấy | Cụm có cabin/khung chở và các thân xe, cửa kính nhìn thấy riêng; luật thing yêu cầu từng vật đếm được | Tách car thật khỏi phần truck nhìn thấy khi xác định được; không gộp cả cụm vào car. Phần không xác định được cabin hay xe chở cần hỏi coach, không bịa instance. |
| Hard `000000350023.jpg`, dải xám bên trái lòng đường sát hàng cây và các xe gần mép đường | Dải này thuộc road / thuộc sidewalk | Màu hai vùng gần nhau; ranh chức năng và bó vỉa quan trọng hơn màu. Hai mask sidewalk hiện tại chưa khớp tại ngưỡng IoU | Kiểm và dừng sidewalk theo bó vỉa, không kéo mask theo toàn bộ mảng xám; cần xác nhận lại vùng biên trong CVAT trước khi sửa/export. |
| Hard `000000460147.jpg`, khe giữa lá/tán cây và nền phía trên hoặc cạnh dải cây giữa đường | Tô kín tán cây là vegetation / giữ các khe có sky, building hoặc road nhìn thấy | Có vùng nền nhìn xuyên giữa các nhánh và mép tán; quy tắc chỉ vẽ phần nhìn thấy, không phủ nền cho đủ coverage | Giữ vegetation theo phần cây nhìn thấy; phân lớp nền ở khe xác định được. Pixel quá nhỏ hoặc mơ hồ ghi để hỏi coach, không ép vegetation. |

Ba ca là ghi nhận QC, không xác nhận các lỗi biên đã được sửa trong CVAT. Bản nộp vẫn cần kiểm lại object/vùng và biên; sáu checkpoint cùng xác nhận ở mục 2 còn thiếu.
