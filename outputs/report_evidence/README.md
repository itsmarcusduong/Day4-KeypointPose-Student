# Nguồn bằng chứng lập báo cáo

- `model_test_grid.png`: giải mã nguyên ảnh PNG nhúng trong output cell 13 của `notebooks/day4_pose_finetune_yolo26.ipynb`, không sửa ảnh.
- `model_comparison_notebook.txt`: nguyên văn output dạng text của cell 11, có bảng baseline/sau fine-tune/chênh.
- `model_vs_train_labels_notebook.txt`: nguyên văn output dạng text của cell 15, có bảng OKS model so với nhãn train.
- `../eval_model.json`: khôi phục 6 hàng số trong bảng cell 11, giữ cấu trúc `baseline_yolo26n-pose`, `finetuned`, `delta` như code notebook. Độ chính xác 4 chữ số thập phân theo bảng đã in; không chạy lại model.
- `../vis_train/*.jpg`: vẽ bằng `tools/visualize_pose.py` trên 20 ảnh và nhãn train hiện tại, 29 skeleton. Đây không phải screenshot CVAT hoặc dự đoán model.

Cell tính từ 0 theo mảng `cells` trong JSON notebook. Kết quả gold lấy từ `../eval_vs_gold.json` và terminal người dùng cung cấp; không chạy lại vì chưa có file gold trong workspace. Chưa có kết quả sau rework hoặc dữ liệu kiểm chéo.
