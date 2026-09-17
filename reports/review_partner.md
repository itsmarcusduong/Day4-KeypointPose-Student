# Kiểm chéo Ngày 4 - trạng thái và lỗi cần đối chiếu

Người gán: Chưa cung cấp | Người kiểm: Chưa cung cấp | Ngày kiểm chéo: Chưa cung cấp

**Chưa có bài của bạn cùng nhóm để kiểm chéo.** Không có căn cứ ghi các lỗi dưới đây là lỗi của bạn khác hoặc kết quả đã được nhóm xác nhận. Bảng sau tổng hợp lỗi của chính bài hiện tại từ gold, dùng chuẩn bị rework.

| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_02.jpg | 1 | Các cặp left/right | Gold phát hiện đảo trái/phải, OKS 0.4864 | Kiểm theo cơ thể và đổi lại các cặp bị đảo; chưa sửa trong lần lập báo cáo. |
| train_04.jpg | 1 | left_wrist | Nhãn v=0, gold v=1: xóa khớp bị che | Kiểm cổ tay trong ảnh, đặt chấm ước lượng và chọn Occluded; chưa sửa. |
| train_15.jpg | 1 | left_wrist / right_wrist | Lệch nhẹ 47 px / 31 px | Điều chỉnh theo cẳng tay và tay lái; export lại rồi chấm; chưa sửa. |

Nguồn: [eval_vs_gold.json](../outputs/eval_vs_gold.json). Số người tính từ 1 theo trường `your_person` trong JSON.

## Cảnh báo tự kiểm cần soi thêm

- `train_04` người #2, `train_10` người #1, `train_11` người #1, `train_13` người #1: mỗi skeleton có 4 khớp v=0 dù hộp nằm giữa ảnh. Đây là cảnh báo heuristic, không tự chứng minh lỗi; cần xem cơ thể có bị mép ảnh cắt không.
- `train_13` người #3 và `train_16` người #2: vai/hông ngược chiều hai mắt. Đây là nghi vấn cần soi ảnh, không gộp thành lỗi đảo trái/phải đã xác nhận bởi gold.

## Hai câu kết luận

- Trong các phát hiện có thể trừ OKS của bài hiện tại, lệch nhẹ xuất hiện nhiều nhất (17); lỗi ưu tiên sửa là 1 đảo trái/phải và 1 xóa khớp bị che.
- Chưa đủ căn cứ quy tất cả lỗi cho thao tác hoặc guideline. Trái/phải cần kiểm cách đặt tên; v=0/v=1 cần làm rõ bị che và ngoài ảnh. Kết luận về bài của bạn cùng nhóm phải chờ kiểm chéo thật.

## Việc cần có để hoàn thành kiểm chéo

1. Tên người gán/người kiểm và nhãn của bạn cùng nhóm.
2. Chạy check, visualize và visibility compare trên hai bài; lưu `reports/visibility_compare.md`.
3. Soi ảnh, ghi lỗi của bài được kiểm vào bảng, điền [checklist](REVIEWER_CHECKLIST.md) cho đúng bài đó.
4. Thống nhất luật, cập nhật guideline rồi ghi kết quả vào mục 3 của [báo cáo](REPORT.md).
