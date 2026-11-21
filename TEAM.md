# TEAM — Ngày 12

Mã bộ ảnh: **G10** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Trần Anh Văn | 2A202603058 | có | Nguyễn Văn Nam (G10) | 6 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `D01.png` (khuôn mặt tài xế): Thảo luận về việc có nên giữ khung xương `face13` khi tài xế cúi gục đầu khiến toàn bộ 13 điểm đều bị che khuất (outside=1). Sau khi tham vấn Guideline §4.6, thống nhất lược bỏ skeleton face13 trên D01 và chỉ giữ lại bounding box `face`.

## Cá nhân

### TranAnhVan-2A202603058
- Phần mình làm: Tự gán toàn bộ 22 ảnh cốt lõi (16 ảnh OMS S01–S08 RGB/IR và 6 ảnh DMS D01–D06), chạy script tự kiểm qua các mốc Checkpoint A/B/Final, thực hiện diff đối chiếu chéo và sửa bản v2 đạt 0 lỗi 0 cảnh báo.
- Điều mình học được hôm nay: Hiểu rõ nguyên lý vật lý của camera cận hồng ngoại NIR (940nm), cách tính chỉ số buồn ngủ EAR/PERCLOS, và nắm chắc quy tắc tọa độ ghế theo xe (trái ảnh là rear_right) trong khoang lái ô tô.
