# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? Cần quy tắc riêng: trên ảnh gốc của hai camera, một vật ở seam có thể có hai box hợp lệ. Chỉ gọi là `DUPLICATE` khi policy đầu ra yêu cầu một đối tượng duy nhất và đã có timestamp đồng bộ, calibration, ảnh đối chiếu để xác nhận hai box cùng vật. Chưa đủ bằng chứng thì giữ cả hai và chuyển người soát quyết định, không xóa theo cảm giác.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. Giữ cùng track ID khi còn nhận ra cùng vật qua các frame liên tiếp. Thêm keyframe khi hình học thay đổi đáng kể; đặt Outside khi vật rời trường nhìn. Muốn nối track giữa hai camera cần timestamp đồng bộ, calibration, vùng nhìn chồng, chuỗi ảnh thể hiện đường đi và policy định danh; một cặp box giống nhau chưa đủ chứng minh cùng track.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? Ở `adasind_167700.jpg`, L6 `Bike` bị báo `IGNORE_SCOPE`, nhưng ảnh gốc cho thấy reference khoanh `ego_body` lên người và xe phía phải; thân xe gắn camera lại ở mép trái. Tôi giữ bản khóa, lưu `screenshots/167700_ego_body_review.png`, ghi ticket để Coach phân xử thay vì xóa box cho khớp reference. Nếu làm lại, tôi sẽ kiểm từng polygon ignore cùng ảnh gốc và kiểm riêng người đang dắt xe theo R03 trước khi khóa.
