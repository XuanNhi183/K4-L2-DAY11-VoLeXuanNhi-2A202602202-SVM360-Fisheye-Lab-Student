# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `673a707266427b29a18d7bf8c6d535b0c7fbf076ca22c73b8286c0e2ca23d696`; slice `B3-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_152940.jpg, adasind_167700.jpg, adasind_212280.jpg. Frame thiếu trong export: không.
TP=8; FP=5; FN=10; số lần đối chiếu=20; mean IoU của TP=0.876.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.400 | 0.875 | 0.750 |
| precision | 0.615 | 0.313 | 0.000 |
| recall | 0.444 | 0.271 | 0.000 |
| jaccard | 0.348 | 0.206 | 0.000 |
| dice | 0.516 | 0.290 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 5 | 2 | 3 | 0.750 | 0.714 | 0.625 | 0.500 | 0.667 |
| Bus | 0 | 0 | 1 | 0.950 | 0.000 | 0.000 | 0.000 | 0.000 |
| Car | 0 | 1 | 1 | 0.900 | 0.000 | 0.000 | 0.000 | 0.000 |
| Pedestrian | 0 | 0 | 2 | 0.900 | 0.000 | 0.000 | 0.000 | 0.000 |
| ThreeWheeler | 1 | 1 | 1 | 0.900 | 0.500 | 0.500 | 0.333 | 0.500 |
| Truck | 2 | 1 | 2 | 0.850 | 0.667 | 0.500 | 0.400 | 0.571 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_152940.jpg | 4 | 0 | 2 | 0.667 | 1.000 | 0.667 |
| adasind_167700.jpg | 2 | 4 | 7 | 0.182 | 0.333 | 0.222 |
| adasind_212280.jpg | 2 | 1 | 1 | 0.667 | 0.667 | 0.667 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Bus | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|---:|
| Bike | 5 | 0 | 0 | 0 | 0 | 0 | 3 |
| Bus | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| Car | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| Pedestrian | 1 | 0 | 0 | 0 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 0 | 0 | 1 | 0 | 1 |
| Truck | 0 | 0 | 0 | 0 | 0 | 2 | 2 |
| <extra> | 1 | 0 | 0 | 0 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
