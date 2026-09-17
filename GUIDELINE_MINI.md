# Mini guideline - nhóm: T51 | người gán: Dương Minh Quang | ngày: 17/9/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

> Bản này được bổ sung khi lập báo cáo từ dữ liệu hiện có, chưa xác nhận đã ghi trong lúc gán hoặc được nhóm thống nhất. Ảnh minh họa là ảnh vẽ từ nhãn YOLO, chưa thay thế screenshot CVAT. Số người #1, #2 tính theo dòng nhãn, bắt đầu từ 1 như kết quả gold.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm (dự thảo cần xác nhận)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Khi vị trí khớp bị trang phục che, ước lượng theo thân và đùi, đặt chấm v=1; không dùng v=0 nếu còn trong khung. | Vẫn có khớp dù không thấy trực tiếp; train_15, người #1. |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | v=2 khi vị trí khớp nhìn rõ; v=1 khi phải ước lượng phần bị che; không dùng Outside chỉ vì tóc/mũ che. | Mũ không làm tai ra ngoài ảnh; train_06, người #1, hai tai v=1. |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Xét từng khớp: ngoài ảnh dùng v=0, bị vật che trong ảnh dùng v=1. Không đánh Outside toàn bộ phần dưới chỉ vì không nhìn thấy. | train_04, người #1 có phần dưới bị cắt; left_wrist cần xem riêng theo gold. |
| Cổ tay nằm sau tay lái / sau thân mình | Nếu còn trong ảnh, đặt chấm v=1 dựa trên khuỷu, hướng cẳng tay và tay lái. | train_06, người #1, right_wrist hiện v=1. |
| Hai người chồng lên nhau | Theo dõi chuỗi vai–khuỷu–cổ tay và hông–gối–mắt cá của từng người. Không kéo khớp sang người bên cạnh; bị người khác che trong ảnh dùng v=1. | Chưa có ca chồng thân được xác nhận để làm ảnh mẫu; train_04 chỉ minh họa hai người gần nhau. |
| Người nhỏ đến mức nào thì không gán nữa | Không tự đặt ngưỡng bỏ người; luật lớp yêu cầu mọi người có đủ 17 điểm. Khớp nhỏ không thấy rõ nhưng trong ảnh dùng v=1 và ghi ca khó. | Chưa có ảnh mẫu người quá nhỏ được xác nhận trong train; cần bổ sung nếu gặp. |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

Các luật trên là tiêu chí kiểm lại; nhãn hiện tại chưa tuân thủ hoàn toàn, chẳng hạn có hông vẫn v=2 và cảnh báo v=0 cần soi bằng mắt.

Ảnh tham chiếu cho hông bị che:

![train_15 - người #1 bên trái, hông v=1](outputs/vis_train/train_15.jpg)

Ảnh tham chiếu cho tai, cổ tay và hông bị che:

![train_06 - người #1, tai và right_wrist/right_hip v=1](outputs/vis_train/train_06.jpg)

Ảnh tham chiếu cho cơ thể bị cắt ở mép và phân biệt từng người:

![train_04 - người #1 bên trái, người #2 bên phải](outputs/vis_train/train_04.jpg)

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_06`, người #1, khớp `right_hip`

- Mơ hồ: hông phía xa bị tư thế ngồi và phần ghế/tựa xe che, không có bề mặt khớp nhìn rõ.
- Quyết định trong nhãn hiện tại: v=1, vẫn có chấm, khoảng (0.649, 0.572) theo tọa độ chuẩn hóa.
- Vì sao: vùng hông trong khung, có thể suy vị trí từ thân, đùi và ghế; bị che không đồng nghĩa ngoài ảnh.
- Nếu quyết ngược: v=0 bỏ giám sát khớp còn trong ảnh; v=2 mô tả sai trạng thái nhìn thấy.

### Ca 2 - ảnh `train_06`, người #1, khớp `right_ear`

- Mơ hồ: mũ bảo hiểm và góc quay đầu che tai, khó định vị bằng bề mặt tai nhìn rõ.
- Quyết định trong nhãn hiện tại: v=1, đặt chấm khoảng (0.593, 0.329).
- Vì sao: đầu trong khung, tai bị mũ che chứ không bị mép ảnh cắt.
- Nếu quyết ngược: v=0 bỏ khớp còn trong ảnh; v=2 khiến cờ visibility không phản ánh sự che khuất.

### Ca 3 - ảnh `train_15`, người #1 bên trái, khớp `left_wrist`

- Mơ hồ: người cúi trên xe máy; vùng bàn tay/cổ tay khó tách khỏi áo và tay lái.
- Quyết định trong nhãn hiện tại: v=1, chấm khoảng (0.401, 0.387).
- Vì sao: khuỷu và hướng cẳng tay giúp ước lượng cổ tay trong ảnh, không dùng Outside.
- Kiểm lại: gold báo khớp này lệch nhẹ 47 px. Đúng cờ chưa có nghĩa đúng tọa độ; cần soi và điều chỉnh, chưa ghi là đã sửa.
- Nếu quyết ngược: v=0 bỏ giám sát cổ tay bị che; kéo chấm sai sang tay lái cung cấp mục tiêu định vị lệch.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Chưa có tên/nhãn bạn cùng nhóm hoặc bảng so sánh.
- Khớp lệch `%v=1` nhiều nhất: chưa xác định; không dùng gold thay bài bạn cùng nhóm.
- Nguyên nhân guideline hay gán sai: chưa đủ bằng chứng.
- Luật mới sau thống nhất: chưa xác nhận; mục 2 hiện là dự thảo.
