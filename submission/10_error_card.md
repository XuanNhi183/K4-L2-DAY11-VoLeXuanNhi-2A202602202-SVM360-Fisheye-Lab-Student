# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B1 | BOX_GEOMETRY | 1 |
| center | B3 | ATTRIBUTE | 1 |
| center | B3 | BOX_GEOMETRY | 1 |
| center | B3 | MISSING | 8 |
| center | B3 | SPURIOUS | 5 |
| center | B3 | WRONG_CLASS | 2 |
| center | C0 | SPURIOUS | 1 |
| center | C0 | WRONG_CLASS | 2 |
| edge | B3 | MISSING | 2 |
| edge | B3 | SPURIOUS | 3 |
| edge | B3 | WRONG_CLASS | 2 |
| edge | C0 | SPURIOUS | 1 |
| mid | B1 | DUPLICATE | 1 |
| mid | B1 | WRONG_CLASS | 1 |
| mid | B3 | BOX_GEOMETRY | 1 |
| mid | B3 | IGNORE_SCOPE | 1 |
| mid | B3 | MISSING | 9 |
| mid | B3 | SPURIOUS | 6 |
| mid | B3 | WRONG_CLASS | 1 |
| mid | C0 | WRONG_CLASS | 2 |
| unknown | B3 | STRUCTURE | 1 |

## Top defects
- MISSING: 19 (ví dụ frame adasind_152940.jpg)
- SPURIOUS: 16 (ví dụ frame adasind_019560.jpg)
- WRONG_CLASS: 10 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: `MISSING` nổi bật ở `adasind_167700.jpg`, nơi nhiều người và xe chồng lên nhau; L3 bao cả người dắt xe lẫn xe, còn L5 nhầm người dắt xe thành `Bike` (R03). Riêng `adasind_152940.jpg` R6, box ôm sát trong bản rework cao 35,8 px nhưng reference cao 43 px, nên công cụ vẫn báo thiếu dù hai bên cùng chỉ vào chiếc xe màu hồng. Số đếm của thẻ gồm nhiều dòng nói về cùng một vật, không phải số vật sai độc lập.
- Cách sửa và ai nhận việc (`owner`): `annotator` đã tách người dắt xe khỏi `Bike`, chỉnh box và bổ sung các vật đủ ngưỡng ở vòng rework; `delta.md` ghi matched ở center 6→9, mid 1→4, edge 1→2. Giữ box đối chiếu R6 ôm sát phần xe nhìn thấy, không nới để vượt 40 px. `qa` kiểm tra reference R6 và polygon `ego_body` sai ở mép phải ảnh `167700` trước khi kết luận các ca còn lệch.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `screenshots/167700_ego_body_review.png` cho thấy reference khoanh nhầm người/xe thành `ego_body`; `screenshots/212280_bus_class_review.png` minh họa ca L2 `Car` so với R3 `Bus`. Đối chiếu các dòng `B3-center` trong `findings.csv`, `rework/delta.md` và R01, R03, R04, R07 trong `docs/02-rules-vi.md`.
