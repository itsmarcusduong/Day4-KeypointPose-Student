# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 15.93 khớp có v > 0 mỗi người
- Tổng: v=2 315 | v=1 147 | v=0 31

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 7 | 0 | 24% |
| 1 | left_eye | 20 | 9 | 0 | 31% |
| 2 | right_eye | 20 | 9 | 0 | 31% |
| 3 | left_ear | 10 | 19 | 0 | 66% |
| 4 | right_ear | 13 | 16 | 0 | 55% |
| 5 | left_shoulder | 25 | 4 | 0 | 14% |
| 6 | right_shoulder | 26 | 3 | 0 | 10% |
| 7 | left_elbow | 20 | 9 | 0 | 31% |
| 8 | right_elbow | 23 | 6 | 0 | 21% |
| 9 | left_wrist | 17 | 12 | 0 | 41% |
| 10 | right_wrist | 17 | 11 | 1 | 38% |
| 11 | left_hip | 21 | 7 | 1 | 24% |
| 12 | right_hip | 20 | 8 | 1 | 28% |
| 13 | left_knee | 18 | 6 | 5 | 21% |
| 14 | right_knee | 19 | 5 | 5 | 17% |
| 15 | left_ankle | 13 | 7 | 9 | 24% |
| 16 | right_ankle | 11 | 9 | 9 | 31% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
