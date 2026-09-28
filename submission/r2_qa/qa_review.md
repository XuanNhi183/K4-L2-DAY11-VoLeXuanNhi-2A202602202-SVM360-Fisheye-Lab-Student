# QA review · B1-mid

Mã khóa: 4B7F-EB27
Người soát (reviewer): Nhi
Người gán nhãn gốc (annotator): Phúc

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_014670.jpg | L2 | R04 | Cần xác minh class: xe vàng bị cắt ở mép trái đang là Truck. Phần thân có các ô/thanh ngang; ảnh này chưa đủ rõ để chốt xe tải hay xe chở khách. Nhờ Phúc/Coach soi ảnh gốc, không đổi class chỉ theo phỏng đoán. |
| adasind_014670.jpg | L4; L6 | R04; R05 | L4 là xe ba bánh mui vàng, nhãn ThreeWheeler phù hợp. L6 Car bị mép phải cắt và đã có truncated=true. Không đề nghị sửa hai điểm này. |
| adasind_032280.jpg | L4; L5; L8 | R03; R04; R05 | L5 bao người lái và xe máy chung một Bike. L4 là người đi bộ riêng; L8 là van chở người/cứu thương mang nhãn Car và occluded=true do người/xe phía trước che. Các lựa chọn này phù hợp phần ảnh nhìn thấy. |
| adasind_034080.jpg | L2; L6 | R03 | Nghi box Bike trùng: L2 (121,1010)-(188,1141) nằm trong L6 (108,993)-(278,1306), bao vùng người áo trắng trên cụm xe có người áo cam. Cần xác nhận có xe hai bánh thứ hai hay chỉ một xe chở hai người; nếu cùng xe thì giữ một Bike bao cả người và xe, bỏ L2. |
| adasind_034080.jpg | L9 | R02 | Box Car (466,1067)-(576,1152) trùm sang thân ThreeWheeler L10 đang che phía trước. Mép trái xe con nhìn thấy bắt đầu khoảng x=510; cần thu mép trái box theo phần xe con thực sự nhìn thấy, không suy phần khuất. Giữ occluded=true. |
| adasind_014670.jpg; adasind_032280.jpg; adasind_034080.jpg | ignore_region; metadata | R06; R07; R08 | Mỗi ảnh có hai lens_border và một ego_body với reason hợp lệ; đã đối chiếu đường bao với vùng viền kính và thân xe ở mép trái. Export dạng job không có tên task nên không kết luận task thiếu raw_fisheye. Review dùng ảnh gốc và XML khóa 4B7F-EB27, chưa mở reference/model. L là thứ tự box trong XML, không phải ID CVAT. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
