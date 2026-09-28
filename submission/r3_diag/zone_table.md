# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 10 | 4 | 2 | 2 | 3 | MISSING (2) |
| mid | 6 | 5 | 2 | 2 | 3 | MISSING (4) |
| edge | 2 | 1 | 1 | 2 | 3 | WRONG_CLASS (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: L thiếu nhiều nhất ở mid (5/6 reference; 2 box thừa), tập trung ở `adasind_167700.jpg`. Với M, edge có 2/2 reference bị thiếu và 3 box thừa; mid cũng có 2 thiếu và 3 thừa. Không suy tỷ lệ lỗi của toàn bộ dữ liệu từ 2 vật edge.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: Ảnh `167700` có người dắt xe, xe chồng nhau và box Bike quá rộng nên dễ nhầm class/hình học. Reference của chính ảnh này còn đặt `ego_body` lên người và xe ở mép phải, làm sai phạm vi so sánh; xem `screenshots/167700_ego_body_review.png` (đỏ = reference, xanh = bản của Nhi). IoU sweep cho L-mid matched giảm 2 → 1 khi ngưỡng tăng 0.30 → 0.50, gợi ý độ nhạy hình học. Ba frame của một camera không chứng minh nguyên nhân lỗi model hoặc chất lượng bốn camera SVM.
