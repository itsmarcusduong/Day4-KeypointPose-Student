# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Dương Minh Quang   Nhóm: T51   Ngày: 16/9/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 315 / 147 / 31 |
| Thời gian trung bình mỗi ảnh | 3 |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. `left_ear` — 66% (19/29).
2. `right_ear` — 55% (16/29).
3. `left_wrist` — 41% (12/29).

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

Các khớp này thường bị che và cần chú ý khi gán. Trong `train_06`, mũ bảo hiểm che tai, còn trong `train_15`, cổ tay người ngồi trên xe khó tách khỏi áo và tay lái. Tai khó chọn cờ khi chỉ thấy một phần; cổ tay khó xác định vị trí giải phẫu khi phải ước lượng từ cẳng tay. Tỉ lệ bị che cao không đồng nghĩa khớp đó luôn khó định vị nhất.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.9035 | 0.9214 |
| OKS@0.50 | 0.9655 | 1.0000 |
| OKS@0.75 | 0.9310 | 1.0000 |
| Lỗi `dao_trai_phai` | 1 | 0 |
| Lỗi `nham_nguoi` | 0 | 1 |
| Lỗi `xoa_khop_bi_che` | 1 | 0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- `train_02.jpg`, người #1: sửa lại các cặp trái/phải ở vai, khuỷu, cổ tay, hông, gối và mắt cá theo cơ thể người; điều chỉnh tọa độ và cờ các điểm liên quan. OKS tăng từ **0.4864** lên **0.9652**, không còn lỗi đảo trái/phải theo gold.
- `train_04.jpg`, người bên trái (trước rework là người #1, sau export là người #2): đặt lại `left_wrist` từ `(0, 0, v=0)` thành khoảng `(0.600406, 0.795864, v=1)`. Lỗi xóa khớp bị che đã hết, OKS tăng từ **0.8030** lên **0.8242**; tuy nhiên gold vẫn báo **nhầm người** ở khớp này vì chấm gần cổ tay người khác hơn.
- `train_15.jpg`, người #1: di chuyển `left_elbow`, `left_wrist` và `right_wrist`, giữ cờ v=1. OKS tăng từ **0.7426** lên **0.7609**; `right_wrist` không còn trong danh sách lệch nhẹ, nhưng `left_elbow` và `left_wrist` vẫn lệch lần lượt **50 px** và **53 px**.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

Trước rework, lỗi xảy ra ở `train_02.jpg`, người #1 đứng bên xe đạp. Ảnh chỉ có một người nên dễ phân biệt danh tính, nhưng người đứng nghiêng và quay đầu khiến trái/phải dễ bị nhầm nếu nhìn theo phía khung ảnh thay vì cơ thể. Sau khi sửa trong CVAT và đánh giá lại, gold không còn phát hiện lỗi đảo trái/phải trong 20 ảnh. Script kiểm định dạng vẫn cảnh báo hướng vai/hông so với mắt ở ảnh này; đây là dấu hiệu cần xem bằng mắt, không phải kết luận đảo trái/phải của lần chấm gold.

## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

-

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 | 0.8450 | +0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6908 | +0.0055 |
| pose_precision | 0.9734 | 0.9792 | +0.0058 |
| pose_recall | 0.8462 | 0.8462 | +0.0000 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

   `pose_mAP50-95` tăng **0.0055**, từ **0.6853** lên **0.6908** (0,55 điểm phần trăm). Mức tăng nhỏ trên 10 ảnh test, chưa đủ kết luận model tốt hơn ở mọi tình huống. Chỉ số này không giảm nên không có bằng chứng để khẳng định 20 ảnh làm hỏng khả năng dự đoán pose; `box_mAP50-95` giảm **0.0078**.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

   Sau fine-tune, `box_mAP50-95 = 0.8041`, `pose_mAP50-95 = 0.6908`, chênh **0.1133**. Theo hai chỉ số trên tập test, model tìm người tốt hơn định vị khớp. Ô bao chỉ cần xác định vùng cơ thể; pose phải định vị 17 khớp, phân biệt trái/phải và xử lý khớp bị che.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

   Ảnh `test_07`: **trượt hẳn**. Người ngồi sau bàn nhưng các chấm hông trên ảnh dự đoán rơi xuống vùng bàn phía trước, thay vì vùng cơ thể hợp lý. Đây là nhận xét từ lưới ảnh dự đoán trong notebook.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

   Trong notebook cập nhật, `train_15` có OKS thấp nhất giữa model và nhãn của tôi: **0.554**. Gold sau rework cho người #1 của ảnh này OKS **0.7609**, vẫn báo `left_elbow` lệch 50 px và `left_wrist` lệch 53 px, nên nhãn của tôi còn điểm cần sửa. Chưa có ảnh hoặc tọa độ dự đoán train được lưu để xác nhận model đúng ở từng khớp; không thể chỉ dùng mức bất đồng 0.554 để kết luận model đúng hoàn toàn.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

   Sau rework, **có**, cùng là `train_15`: nhãn-vs-gold thấp nhất **0.7609** (người #1), model-vs-nhãn thấp nhất **0.554**. Ảnh có người cúi trên xe máy, cổ tay khó tách khỏi áo và tay lái; đây là vùng cần kiểm kỹ ở cả nhãn và dự đoán. Tuy nhiên, OKS model-vs-nhãn thấp nhất chỉ thể hiện bất đồng, chưa chứng minh model kém nhất khi so với gold. Trước rework, ảnh nhãn-vs-gold thấp nhất là `train_02` với **0.4864**.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

Trong `train_06.jpg`, người #1 đi xe máy, khớp `right_hip` được gán **v=1** tại tọa độ chuẩn hóa khoảng **(0.649, 0.572)**. Phía hông này bị tư thế ngồi và phần ghế/tựa xe che, nhưng vùng thân, đùi và ghế vẫn nằm trong ảnh. Tôi đặt chấm ước lượng theo thân và đùi, chọn Occluded vì khớp còn trong khung nhưng không nhìn thấy trực tiếp. Không chọn v=0 vì không có bằng chứng khớp đã ra ngoài mép ảnh.
