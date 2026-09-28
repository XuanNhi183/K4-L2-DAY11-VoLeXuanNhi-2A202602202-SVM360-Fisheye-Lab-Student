# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `B3-center` / `adasind_167700.jpg` | `compare.md` nêu 9 khác biệt: 4 `MISSING`, 2 `WRONG_CLASS`, 1 `BOX_GEOMETRY`, 1 `SPURIOUS`, 1 `IGNORE_SCOPE`. | Người dắt xe, các phương tiện chồng nhau và reference đặt `ego_body` lên người/xe ở mép phải; sai phạm vi làm kết quả so sánh thiếu tin cậy. | Ảnh gốc, XML hai phía, `r1_craft/compare.html`, `screenshots/167700_ego_body_review.png` và dòng L6/R2 trong `findings.csv`. |
| `B3-center` / `adasind_152940.jpg` | 2 `MISSING` trong `compare.md` (R5 và R6); sau rework R5 đã sửa, R6 còn báo chưa sửa. | Xe hồng R6 nằm sát ngưỡng H=40: box ôm sát 35,8 px, reference 43 px. Cần phân xử hình học trước khi gọi là lỗi bỏ sót. | Ảnh gốc, box R6 trong XML reference, box rework, `rework/delta.md`, dòng R6 trong `findings.csv` và R01/R02. |

Giới hạn của kết luận từ ba frame ADASIND: Đây là ba ảnh của một camera fisheye, không đại diện đủ cảnh, thời điểm, class hay bốn camera SVM. Một khác biệt có thể bắt nguồn từ nhãn người học, teaching reference, ngưỡng ghép hoặc vùng ignore. Các dòng `findings.csv` còn có thể lặp cùng một vật qua nhiều báo cáo nên không dùng số dòng làm tỷ lệ lỗi.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: Kiểm đủ 8 ô `front/rear/left/right × normal/hard` trong `45_sampling_plan.csv`, mỗi camera 20 normal + 30 hard, tổng 200. Lấy mẫu từ nhiều cảnh và thời điểm, giới hạn frame liền nhau cùng một chuỗi, kiểm độ phủ class, che khuất, méo rìa và vùng seam từng camera. Tỷ lệ hard được chủ ý tăng để tìm lỗi; chưa có 50.000 frame thật, xác suất chọn mẫu hay nhãn gold đã duyệt nên không thể suy ra tỷ lệ lỗi của hệ thống.
