# Guideline patch

- **Rule mới đề xuất:** Bổ sung hướng dẫn cho R01: ở ca sát ngưỡng H=40 px, đo chiều cao của box ôm sát **phần vật thật sự nhìn thấy trên ảnh gốc**. Không nới box để đạt H. Nếu box của người gán nhãn và reference nằm hai phía của ngưỡng, ghi cả hai tọa độ, ảnh crop và quyết định của người soát trước khi tính đó là lỗi thiếu.
- **Áp dụng cho:** Mọi class động ở ca sát ngưỡng R01/R02; ví dụ `adasind_152940.jpg` R6 `ThreeWheeler`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R01 nêu ngưỡng 40 px và R02 yêu cầu box bám vật, nhưng chưa chỉ cách phân xử khi phần xe nhìn thấy được vẽ chặt cao 35,8 px còn teaching reference cao 43 px. `delta.md` vì thế báo R6 "chưa sửa" dù việc nới box có thể thêm nền.
- **`rules_version` mới:** Đề xuất `v1.1.0` từ `v1.0.0`; chỉ áp dụng sau khi Lab Coach duyệt.
- **Hiệu lực từ:** Các vòng gán nhãn và review sau khi duyệt patch; không áp dụng ngược để sửa bản `r1_craft` đã khóa.
