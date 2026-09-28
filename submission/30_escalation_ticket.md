# Escalation ticket

## Ticket 1

- **Frame:** `adasind_167700.jpg` (`B3-center`)
- **Ảnh chụp:** `submission/screenshots/167700_ego_body_review.png` (đường đỏ = reference; xanh = export của Nhi)
- **Expected impact:** Reference đánh dấu `ego_body` phía phải lên người và xe đạp; box L6 bị báo `IGNORE_SCOPE`, còn phép so sánh có thể bỏ qua vật hợp lệ và làm sai số missing/spurious ở ảnh này. Kết quả quality/zone của slice cần đọc với giới hạn đó.
- **Owner:** `qa`
- **Recommendation:** Lab Coach kiểm lại ảnh gốc và polygon `ego_body` của reference; nếu xác nhận sai, chuyển vùng ignore sang thân xe ở mép trái, giữ người và xe bên phải trong vùng hợp lệ, rồi chạy lại compare/local-quality. Giữ reference hiện tại làm bằng chứng cho đến khi có bản sửa có phiên bản.
