# Day-5 Segmentation — Scorecard

> Kết quả đối chiếu cục bộ sau khi thay export Medium ngày 17/09/2026 bằng scorer nguyên bản và `tiers_gt.zip` được cung cấp. Đây là phản hồi ba tier /82, chưa phải điểm từ GitHub Actions hoặc điểm chính thức; chưa bao gồm sáu checkpoint.

**Total: 41.6 / 82**

| Task | Group | Type | Metric | Points |
| --- | --- | --- | ---: | ---: |
| easy_semantic | tiers | semantic | 0.815 | 18.4 / 20 |
| medium_instance | tiers | instance | 0.559 | 11.3 / 32 |
| hard_panoptic | tiers | panoptic | 0.378 | 11.9 / 30 |

## So với trước khi thay Medium

| Chỉ số | Trước | Sau |
| --- | ---: | ---: |
| Mask Medium | 9 | 84 |
| Metric Medium | 0,034 | 0,559 |
| Điểm Medium | 0/32 | 11,3/32 |
| Tổng ba tier | 30,3/82 | 41,6/82 |

Medium: 52 mask khớp tại IoU ≥ 0,5; 32 mask nộp chưa khớp; 19 object tham chiếu chưa khớp. Hai nhóm chưa khớp cần xem lại trong CVAT, không phải danh sách mask cần xóa tự động.

[Báo cáo trước rework](history/before_medium_rework/SCORECARD.md).
