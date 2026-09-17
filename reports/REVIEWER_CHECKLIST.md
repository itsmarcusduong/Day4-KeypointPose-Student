# Reviewer checklist - điền khi kiểm bài người khác

Người gán: Dương Minh Quang | Người kiểm: Tự review | Ngày kiểm chéo: 17/9/2026


Chạy trước khi soi bằng mắt:

```bash
python3 tools/check_pose_labels.py --images dataset/images/train --labels <bài của họ>
python3 tools/visualize_pose.py --images dataset/images/train --labels <bài của họ> --out /tmp/vis_review
python3 tools/visibility_report.py --labels dataset/labels/train --compare <bài của họ>
```

| | Mục kiểm | Đạt? | Ghi chú / ảnh nào |
| --- | --- | --- | --- |
| 1 | Mọi người trong ảnh đều có đủ 17 điểm, không ai bị thiếu | Đạt theo định dạng/gold | 29 skeleton đủ 17 điểm; gold ghép 29/29, thiếu/thừa 0. |
| 2 | Bật đường nối: không có xương nào cắt chéo ở vai hoặc hông | Cần sửa | Gold phát hiện đảo trái/phải train_02 #1; cảnh báo train_13 #3 và train_16 #2 cần soi thêm. |
| 3 | Không có xương nào kéo dài sang một cơ thể khác | Chưa xác nhận toàn bộ | Gold không báo nham_nguoi; chưa soi toàn bộ 20 ảnh cho kiểm chéo. |
| 4 | Khớp bị che dùng `v = 1` **và có chấm**, không phải `v = 0` | Cần sửa | train_04 #1 left_wrist: gold v=1, bài v=0. |
| 5 | `v = 0` chỉ xuất hiện ở khớp thật sự ra ngoài mép ảnh | Cần soi thêm | 4 cảnh báo ở train_04 #2, train_10 #1, train_11 #1, train_13 #1. |
| 6 | Không có dấu hiệu dùng `Hidden` (điểm `v = 2` nằm ở chỗ vô lý) | Chưa xác nhận | Chưa có lịch sử thao tác CVAT hoặc kiểm ảnh đầy đủ. |
| 7 | Export đúng **COCO Keypoints 1.0**: mảng `keypoints` có 51 số mỗi người | Đạt về cấu trúc | JSON export có 20 ảnh, 29 annotation; mọi mảng keypoints dài 51. |
| 8 | Bản YOLO Pose: mỗi dòng 56 số, `kpt_shape: [17, 3]` | Đạt | check chạy 0 lỗi; data.yaml dùng [17, 3]. |
| 9 | Visibility report đã nộp, và hai bảng đã được đặt cạnh nhau | Chưa đủ | Có report của bài hiện tại; thiếu bảng của bạn cùng nhóm, chưa xác nhận nộp. |
| 10 | Mọi ca không rõ đều được ghi trong `GUIDELINE_MINI.md` | Chưa xác nhận đầy đủ | Có 3 ca dẫn chứng; chưa có lịch sử tất cả ca mơ hồ hoặc screenshot CVAT. |
| 11 | `check_pose_labels.py` chạy 0 lỗi | Đạt định dạng | 20/20 file, 29 skeleton, 0 lỗi định dạng, 8 cảnh báo. |

## Lỗi tìm được

Chép sang `reports/review_partner.md`. Mỗi dòng một lỗi, đủ bốn cột - người sửa phải
mở đúng chỗ đó được mà không cần hỏi lại.

| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_02.jpg | 1 | Các cặp left/right | Đảo trái/phải theo gold | Kiểm theo cơ thể và đổi cặp bị đảo; chưa sửa. |
| train_04.jpg | 1 | left_wrist | Khớp bị che để v=0 | Đặt chấm ước lượng và v=1 sau khi soi ảnh; chưa sửa. |
| train_15.jpg | 1 | left_wrist / right_wrist | Lệch nhẹ 47 px / 31 px | Điều chỉnh theo cẳng tay/tay lái rồi chấm lại; chưa sửa. |

## Hai câu kết luận

- Lỗi có thể trừ OKS lặp nhiều nhất: lệch nhẹ, 17 phát hiện theo JSON gold. Hai lỗi ưu tiên là đảo trái/phải và xóa khớp bị che.
- Chưa xác nhận nguyên nhân thao tác hay guideline; cần kiểm lại ảnh và trao đổi với người gán. Đây chưa phải kết luận kiểm chéo bài bạn khác.
