# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | 30 hard: người bị xe che hoặc cảnh ngược sáng. | Dễ bỏ sót người hoặc vẽ box vượt phần nhìn thấy. | Ảnh fisheye gốc; lưu camera_id, timestamp, độ phân giải và phiên bản calibration. | Chọn 20 normal và 30 hard từ nhiều cảnh/thời điểm. Đề xuất Nhi gán nhãn, Phúc soát độc lập, Tuấn phân xử bằng ảnh và rule. Kiểm thiếu/thừa, class và box; chỉ chốt gold sau khi sửa và kiểm lại. |
| rear | 30 hard: người sau xe đỗ hoặc vật bị cắt ở biên ảnh. | Dễ nhầm che khuất với cắt biên và bỏ sót phần vật còn thấy. | Ảnh fisheye gốc; giữ vòng kính, timestamp và calibration của camera sau. | Chọn 20 normal và 30 hard, tránh frame liên tiếp gần giống nhau. Review độc lập và phân xử như camera front; kiểm box, occluded và truncated riêng biệt. |
| left | 30 hard: vật méo ở rìa và tại seam trước-trái, sau-trái. | Box dễ lệch; cùng vật ở hai camera dễ bị xoá nhầm như nhãn trùng. | Ảnh gốc từng camera; lưu timestamp đồng bộ, thông số nội/ngoại tại và phiên bản calibration. | Chọn 20 normal nhiều lớp đối tượng và 30 hard phủ cả hai seam. Review độc lập và phân xử như camera front; kiểm hình học trên ảnh gốc. Ca chưa rõ giữ chờ, chưa đưa vào gold. |
| right | 30 hard: vật méo rìa hoặc bị che ở seam trước-phải, sau-phải. | Dễ bỏ sót vật hoặc ghép nhầm hai vật khi đối chiếu camera. | Ảnh gốc từng camera; giữ camera_id, timestamp và calibration như bên trái. | Chọn 20 normal và 30 hard phủ cả hai seam. Review độc lập và phân xử như camera front; kiểm phần nhìn thấy và class. Ghi quyết định, người soát, phiên bản rule; soát đủ tám nhóm với tổng 200 frame theo CSV. |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): Khi thay camera, đổi vị trí lắp, độ phân giải, calibration, phép biến đổi ảnh hoặc guideline; khi xuất hiện cảnh/lỗi mới chưa được phủ. Soát lại mẫu bị ảnh hưởng và lưu phiên bản mới. Sau P4 cập nhật giả định chọn mẫu theo lỗi đã thấy.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: Một người xuất hiện đồng thời ở camera front và left. Với nhãn trên ảnh từng camera, giữ box riêng ở cả hai ảnh. Muốn liên kết cùng đối tượng hoặc hợp nhất trên BEV cần timestamp đồng bộ, calibration, ảnh đối chiếu và policy về output/identity. Thiếu bằng chứng thì để chờ review, không tự ghép hay xoá box. Không dùng box trên BEV để thay trực tiếp box trên fisheye gốc.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: Hai người có thể cùng hiểu sai rule; báo cáo phụ thuộc chất lượng reference và phạm vi so sánh. ADASIND chỉ có một camera nên không kiểm chứng được độ phủ bốn hướng, calibration hay seam. Đây là kế hoạch giả lập chưa có 200 ảnh được kiểm chứng; tỷ lệ ưu tiên hard dùng tìm lỗi, không đại diện tần suất lỗi thực tế.
