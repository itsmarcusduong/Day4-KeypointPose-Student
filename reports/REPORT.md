# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: **Chưa cung cấp** | Nhóm: **Chưa cung cấp** | Ngày thực hành: **Chưa cung cấp**

> Điền từ dữ liệu dự án, terminal đính kèm và output notebook đã lưu. Chưa có bằng chứng về lần chấm sau rework hoặc kiểm chéo. Các mục chưa có dữ liệu được ghi rõ, không tính là đã hoàn thành.

## 1. Nhãn của tôi

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 317 / 144 / 32 |
| Trung bình số khớp có v > 0 mỗi người | 15,9 |
| Thời gian trung bình mỗi ảnh | Chưa có tổng thời gian gán; tính bằng tổng số phút / 20 |

Nguồn: [visibility report](visibility_report.md), [JSON visibility](../outputs/visibility_report.json).

Ba khớp có `%v=1` cao nhất:

1. `left_ear`: **66%** (19/29).
2. `right_ear`: **52%** (15/29).
3. `left_wrist`: **38%** (11/29); `right_wrist` đồng hạng **38%**.

Đây là các vị trí cần chú ý vì thường bị che, nhưng tỉ lệ bị che không tự chứng minh chúng khó nhất. Trong `train_06`, mũ bảo hiểm che tai; trong `train_15`, cổ tay người ngồi trên xe khó tách khỏi áo và tay lái. Tai khó chọn cờ khi chỉ thấy một phần, còn cổ tay khó xác định vị trí khi bàn tay và cẳng tay không nhìn rõ. Nhận xét dựa trên ảnh; mức độ khó theo trải nghiệm cá nhân cần người gán xác nhận.

## 2. Chấm với gold

Chỉ có một lần đánh giá được cung cấp. Ghi lần này vào cột trước rework; chưa có kết quả lần hai.

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.9035 | Chưa có dữ liệu |
| OKS@0.50 | 0.9655 | Chưa có dữ liệu |
| OKS@0.75 | 0.9310 | Chưa có dữ liệu |
| Lỗi `dao_trai_phai` | 1 | Chưa có dữ liệu |
| Lỗi `nham_nguoi` | 0 | Chưa có dữ liệu |
| Lỗi `xoa_khop_bi_che` | 1 | Chưa có dữ liệu |

Nguồn: [eval_vs_gold.json](../outputs/eval_vs_gold.json). Dùng số JSON vì lưu nhiều chữ số hơn terminal. Có 29 người gold, ghép được 29, thiếu 0 và thừa 0. Có thêm 17 phát hiện lệch nhẹ, 72 cờ khác gold và 70 khớp gold không gán nhãn. Hai nhóm sau là thông tin chẩn đoán, không trừ OKS theo hướng dẫn bài.

Terminal in **Xuất sắc** theo điểm số, nhưng theo [RUBRIC.md](../RUBRIC.md), bài vẫn **cần rework** do còn một lỗi đảo trái/phải, chưa đạt đầy đủ cổng bắt buộc.

**Tôi đã sửa gì giữa hai lần chạy:** Chưa có bằng chứng đã sửa và chạy lại. Ba việc cần thực hiện, chưa được tính là đã sửa:

- `train_02.jpg`, người #1: gold phát hiện đảo trái/phải, OKS **0.4864**. Kiểm toàn bộ cặp trái/phải theo cơ thể người đi xe đạp rồi đổi lại các cặp bị đảo.
- `train_04.jpg`, người #1, `left_wrist`: hiện `(0, 0, v=0)` trong khi gold có v=1. Xác định cổ tay bị che còn trong ảnh, đặt lại chấm ước lượng và chọn Occluded. Skeleton này có OKS **0.8030**.
- `train_15.jpg`, người #1, `left_wrist` và `right_wrist`: gold báo lệch nhẹ **47 px** và **31 px**. Kiểm vị trí theo cẳng tay/tay lái, điều chỉnh trong CVAT, export lại và đánh giá. OKS skeleton **0.7426**.

**Lỗi đảo trái/phải xảy ra ở đâu?** Ở `train_02.jpg`, người #1. Ảnh chỉ có một người nên dễ phân biệt danh tính, nhưng tư thế đứng nghiêng bên xe đạp và quay đầu làm trái/phải dễ nhầm. Nguyên nhân có thể là đặt tên theo khung ảnh thay vì cơ thể; đây là giả thuyết từ ảnh và chẩn đoán gold, chưa phải xác nhận của người gán. Cần kiểm cả vai, hông và các chi.

## 3. Kiểm chéo

Bạn cùng nhóm: **Chưa cung cấp**. Chưa có nhãn của bạn cùng nhóm hoặc `visibility_compare.md`, nên chưa tính được hai khớp lệch nhiều nhất.

| Khớp | Bạn | Họ | Lệch | Nguyên nhân |
| --- | ---: | ---: | ---: | --- |
| Chưa xác định - hàng 1 | Chưa có dữ liệu | Chưa có dữ liệu | Chưa tính | Chưa đối chiếu |
| Chưa xác định - hàng 2 | Chưa có dữ liệu | Chưa có dữ liệu | Chưa tính | Chưa đối chiếu |

[GUIDELINE_MINI.md](../GUIDELINE_MINI.md) đã bổ sung dự thảo luật và ba ca có dẫn chứng từ nhãn hiện tại. Chưa có bằng chứng nhóm đã thống nhất luật mới sau kiểm chéo. [review_partner.md](review_partner.md) và [reviewer checklist](REVIEWER_CHECKLIST.md) ghi rõ phạm vi tự kiểm và các mục chưa có dữ liệu kiểm chéo.

## 4. Model

Nguồn: output baseline và cell so sánh trong [notebook](../notebooks/day4_pose_finetune_yolo26.ipynb). [eval_model.json](../outputs/eval_model.json) được khôi phục từ bảng đã in, không phải kết quả chạy model mới.

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 | 0.8450 | +0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6908 | +0.0055 |
| pose_precision | 0.9734 | 0.9792 | +0.0058 |
| pose_recall | 0.8462 | 0.8462 | +0.0000 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

Notebook dùng GPU Tesla T4, 20 ảnh train/29 skeleton và 10 ảnh test/13 skeleton. Cấu hình tối đa 80 epoch, batch 8, kích thước 640, patience 30; thực tế dừng sớm sau **39 epoch**, checkpoint tốt nhất ở **epoch 9**. Bảng dùng lần đánh giá riêng của `best.pt` trong cell so sánh; số in cuối vòng train thuộc lần đánh giá khác.

### Trả lời năm câu hỏi cuối notebook

1. **`pose_mAP50-95` thay đổi bao nhiêu?** Tăng **0.0055**, từ **0.6853** lên **0.6908**, tương đương 0,55 điểm phần trăm. mAP50 và recall giữ nguyên, precision tăng 0.0058. Checkpoint được chọn cải thiện nhẹ trên 10 ảnh test; tập nhỏ chưa đủ kết luận tốt hơn ở mọi tình huống. Chỉ số pose này không giảm nên chưa có căn cứ nói fine-tune làm hỏng khả năng dự đoán pose; box mAP50-95 giảm 0.0078.

2. **Box và pose chênh bao nhiêu?** Sau fine-tune: box_mAP50-95 **0.8041**, pose_mAP50-95 **0.6908**, chênh **0.1133**. Theo hai chỉ số, model tìm người tốt hơn định vị bộ khớp trên tập test. Ô bao chỉ xác định vùng cơ thể; pose cần định vị nhiều khớp và phân biệt trái/phải, kể cả vị trí bị che. Đây là quan sát trên tập test của bài.

3. **Một ảnh test dự đoán sai:** Trong `test_07`, người ngồi sau bàn, hông không nhìn thấy trực tiếp. Các chấm hông và đường nối thân trên ảnh dự đoán rơi xuống vùng bàn phía trước thay vì vùng cơ thể hợp lý. Gọi lỗi **trượt hẳn**: điểm rơi vào vật che phía trước, không chỉ lệch vài pixel khỏi khớp rõ ràng. Nhận xét dựa trên [lưới dự đoán](../outputs/report_evidence/model_test_grid.png), chưa phải phép đo sai số từng khớp với nhãn test.

4. **OKS model-vs-nhãn thấp nhất:** `train_02`, **0.347**. Gold cũng phát hiện nhãn của tôi đảo trái/phải và cho OKS **0.4864**, nên có căn cứ xác định nhãn của tôi cần sửa. Tuy nhiên chưa có ảnh dự đoán train hoặc tọa độ model được lưu để xác nhận model đúng ở từng khớp. Cần đối chiếu dự đoán với ảnh gốc và gold; OKS bất đồng không đủ xác nhận model đúng hoàn toàn.

5. **Ảnh gán tệ nhất có là ảnh model tệ nhất?** Nếu xét bất đồng model-vs-nhãn thì **có**, đều `train_02`: nhãn-vs-gold thấp nhất **0.4864**, model-vs-nhãn thấp nhất **0.347**. Sự trùng nhau phù hợp với lỗi trái/phải trong nhãn, chưa chứng minh model kém nhất ở ảnh này khi so với gold. Hai phép so dùng hai mốc khác nhau; nhãn sai có thể khiến model đúng vẫn có OKS thấp khi so với nhãn đó.

## 5. Một rule evidence đã dùng

Trong `train_06.jpg`, người #1 đi xe máy, `right_hip` được gán **v=1**, khoảng **(0.649, 0.572)** theo tọa độ chuẩn hóa. Phía hông này bị tư thế ngồi và phần ghế/tựa xe che, nhưng vùng thân, đùi và ghế vẫn nằm trong ảnh. Vì vậy đặt chấm ước lượng theo thân và đùi, dùng Occluded để biểu thị khớp trong khung nhưng không thấy trực tiếp. Không chọn Outside vì không có bằng chứng khớp ra ngoài ảnh. Nhãn hiện tại và [ảnh skeleton](../outputs/vis_train/train_06.jpg) thể hiện quyết định này.

## Các mục cần bổ sung trước khi nộp đầy đủ

- Họ tên, nhóm, ngày thực hành và tổng thời gian gán.
- Sửa lỗi trong CVAT, export lại, kiểm định dạng và chấm lần hai; lưu cả kết quả trước/sau.
- Tên/nhãn bạn cùng nhóm, visibility compare, kết quả kiểm chéo và luật đã thống nhất.
- Screenshot CVAT cho các luật nhóm; ảnh hiện tại được vẽ từ nhãn YOLO.
- Dự đoán train để kết luận ai đúng trong ca bất đồng `train_02`.
