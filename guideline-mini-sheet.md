# Phiếu quy tắc gán nhãn Day 5

## Chọn đúng loại trước khi vẽ

| Loại | Câu hỏi | Trong bài |
| --- | --- | --- |
| Semantic | Pixel này thuộc **loại vùng** nào? | Easy, `cp3_thin`, `cp4_curb`, `cp6_coverage` |
| Instance | Pixel này thuộc **vật nào**? | Medium, `cp1_holes`, `cp2_slice`, `cp5_occlusion` |
| Panoptic | Vùng thuộc loại nào **và** vật đếm được nào? | Hard |

Tên lớp phải giống từng chữ trong `classes.json` của task. `traffic sign` khác `traffic_sign`. Không dùng chung một danh sách lớp cho mọi task.

## Quy tắc hình học chung

- Vẽ sát **phần nhìn thấy**, không tự đoán phần bị che.
- Hai vật cùng lớp sát nhau vẫn là **hai instance**.
- Một vật bị cột hay vật khác che có thể có các vùng nhìn thấy rời nhau nhưng vẫn là **một instance**.
- Kính/chi tiết trên xe không tự động là lỗ phải khoét khỏi mask; theo quy tắc task.
- Ranh `road`–`sidewalk` xác định theo chức năng và bó vỉa, không chỉ theo màu.
- Phóng to kiểm nét mảnh và khe hở; Save rồi xem lại danh sách Objects.

## Tự kiểm trước export

1. Đúng ảnh và đúng loại semantic/instance/panoptic chưa?
2. Mọi tên lớp có khớp `classes.json` không?
3. Có vật thiếu, vật thừa, gộp hai vật hoặc tách sai một vật không?
4. Mask có tràn sang nền/bóng hoặc bỏ sót vùng rõ ràng không?
5. Đã Save và export đúng format của task chưa?

Khi không chắc, ghi ảnh/vị trí, dấu hiệu nhìn thấy, quy tắc đã dùng và điều cần hỏi trong `REPORT.md`. Không ép đoán cho đủ coverage.

## Áp dụng cho bài 2A202602060 — bản export mới nhất

Ngày kiểm: **17/09/2026**. Bản dùng để kiểm: `DAY05-2A202602060-LENGOCNAM.zip`. Các ghi nhận dưới đây là QC của bản export hiện tại, không xác nhận lịch sử tự vẽ trước khi dùng model.

Nơi lưu các ZIP đã nộp và kết quả kiểm: [fork GitHub cá nhân](https://github.com/duy12345-6789/K4-L2-Day05-LENGOCNAM-2A202602060-Segmentation). Trạng thái ZIP trong checklist bên dưới áp dụng cho fork.

### Lớp và định dạng của ba tier

| Task | Lớp đúng theo classes.json | Định dạng export và tên ZIP |
| --- | --- | --- |
| Easy — semantic | `road`, `sidewalk`, `building`, `vegetation`, `sky` | Segmentation mask 1.1 → `easy_semantic.zip` |
| Medium — instance | `person`, `bicycle`, `car`, `motorcycle`, `bus`, `truck` | COCO 1.0 → `medium_instance.zip` |
| Hard — panoptic | `road`, `sidewalk`, `building`, `vegetation`, `sky`, `person`, `car`, `bus`, `truck`, `motorcycle`, `bicycle`, `traffic light` | COCO 1.0 theo hợp đồng starter → `hard_panoptic.zip` |

Với Medium và các thing của Hard, mỗi vật đếm được là một object riêng. `car #1`, `car #2`, `car #3` là cách nhận diện các object, **class vẫn là `car`**, không tạo class mới có số. Chỉ Join các phần thuộc cùng một vật. Nếu model tạo mask, dùng Brush để thêm/sửa mask; các object tham gia Join phải cùng class và cùng loại hình học được CVAT hỗ trợ.

Với Hard, kiểm cả vùng stuff và từng thing, vẽ từ xa tới gần rồi kiểm chồng lấn và vùng chưa phủ. COCO 1.0 có mask chưa đủ để kết luận panoptic đúng. Nếu export không giữ mask đúng, báo coach; không sửa JSON/PNG trong ZIP bằng tay.

### Sáu checkpoint: đầu vào và file phải nộp

`data/checkpoints/` **đúng là thư mục sáu trạm**. Hiện mỗi trạm có một ảnh JPG, `classes.json` và `cvat-labels.json`; hai JSON là danh sách lớp để tạo task, không phải kết quả gán nhãn. Chưa tìm thấy export checkpoint trong thư mục này hoặc trong gói bài mới nhất.

| Trạm | Ảnh đầu vào | Lớp riêng của trạm | Format → tên ZIP trong submissions/ |
| --- | --- | --- | --- |
| `cp1_holes` | `000000144300.jpg` | `person`, `bicycle`, `car`, `motorcycle`, `bus`, `truck` | COCO 1.0 → `cp1_holes.zip` |
| `cp2_slice` | `000000017627.jpg` | `person`, `bicycle`, `car`, `motorcycle`, `bus`, `truck` | COCO 1.0 → `cp2_slice.zip` |
| `cp5_occlusion` | `000000336232.jpg` | `person`, `bicycle`, `car`, `motorcycle`, `bus`, `truck` | COCO 1.0 → `cp5_occlusion.zip` |
| `cp3_thin` | `839f7736-abe28069.jpg` | `pole`, `traffic sign`, `sky`, `road` | Segmentation mask 1.1 → `cp3_thin.zip` |
| `cp4_curb` | `7d83710e-4697c3b2.jpg` | `road`, `sidewalk` | Segmentation mask 1.1 → `cp4_curb.zip` |
| `cp6_coverage` | `7daa6479-67988f3f.jpg` | `road`, `sidewalk`, `building`, `vegetation`, `sky`, `car`, `person` | Segmentation mask 1.1 → `cp6_coverage.zip` |

Tạo từng task từ ảnh và `cvat-labels.json` của đúng trạm, vẽ, Save rồi export đúng format. Không nén thư mục ảnh/classes để thay cho export. CP1 kiểm lỗ/kính theo quy tắc task; CP2 giữ hai vật sát nhau riêng; CP5 giữ các phần nhìn thấy của cùng vật trong một instance; CP3 giữ nét mảnh; CP4 theo bó vỉa; CP6 kiểm phủ vùng xác định được.

### Kết quả QC hiện tại

- [x] Ba tier có export cho đúng 8 ảnh và danh sách lớp phù hợp; inspector báo 0 lỗi cấu trúc.
- [x] Ba native ZIP được đặt đúng tên trong `submissions/` của fork, giữ nguyên nội dung CVAT.
- [x] Ghi một lỗi đóng gói thực tế và cách sửa, cùng ba ca cần cân nhắc, vào [reports/REPORT.md](reports/REPORT.md).
- [ ] Medium: kiểm lại object thiếu/thừa, gộp/tách và biên. Hiện có 112 mask; scorer ghi 55 khớp, 57 chưa khớp và 16 object tham chiếu chưa khớp. Không tự động xóa các mask chưa khớp.
- [ ] Hard: kiểm chồng lấn, đủ thing và phủ stuff. Hiện có 99 mask; hai mask sidewalk chưa khớp tại ngưỡng IoU, lớp bicycle chưa có annotation nộp.
- [ ] Easy: kiểm biên vegetation và vùng chưa phủ; mIoU hiện tại 0,820, coverage theo tham chiếu 89,4%.
- [ ] Xác nhận object Medium đầu tiên tự vẽ trước gợi ý, class/quy tắc biên và một quyết định sửa/giữ gợi ý thực tế.
- [ ] Hoàn thành hoặc cung cấp export cho sáu checkpoint. Không đánh dấu hoàn thành chỉ vì đã có ảnh đầu vào.

Phản hồi cục bộ của **bản mới nhất**: Easy **18,7/20**, Medium **13,3/32**, Hard **12,7/30**, tổng **44,7/82**; tham chiếu là `tiers_gt.zip` do người làm bài cung cấp. Đây không phải điểm chính thức và chưa gồm 18 điểm checkpoint. Ground truth được giữ ngoài fork. GitHub Actions chỉ chấm /82 khi release đáp án chính thức khả dụng; lần chạy xanh không chứng nhận PASS, bonus hoặc top 3.

