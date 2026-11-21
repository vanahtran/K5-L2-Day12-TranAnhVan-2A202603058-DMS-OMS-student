# TEAM — Ngày 12

Mã bộ ảnh: **G10** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Trần Anh Văn | 2A202603058 | có | Minh Hữu (ongbin123 - G10) | 55 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `D01.png` (khuôn mặt tài xế): Thảo luận về việc có nên vẽ khung xương `face13` khi tài xế cúi gục đầu khiến toàn bộ 13 điểm đều bị che khuất (outside=1) như bài của Văn, hay không vẽ skeleton như bài của Hữu (ongbin123). Sau khi đối chiếu Guideline §4.6 ("không thấy mặt thì không vẽ skeleton"), Văn đồng thuận theo Hữu lược bỏ skeleton face13 trên D01 và chỉ giữ lại bounding box `face`.
- `D05.png` (mắt trái tài xế): Hữu gán `eye_left = open`, Văn gán `eye_left = closed` do mắt tài xế hơi cụp khi nhìn xuống đùi. Thảo luận ca ranh giới mí mắt khép gần hết khi nhìn xuống đùi, thống nhất hỏi coach về ngưỡng phân biệt liếc đùi vs nhắm mắt.

## Cá nhân

### TranAnhVan-2A202603058
- Phần mình làm: Tự gán toàn bộ 22 ảnh cốt lõi (16 ảnh OMS S01–S08 RGB/IR và 6 ảnh DMS D01–D06), chạy script tự kiểm qua các mốc Checkpoint A/B/Final, nhận file export từ bạn Minh Hữu (`ongbin123`) chạy diff đối chiếu chéo (55 điểm khác biệt), phân tích nguyên nhân và sửa bản v2 đạt 0 lỗi 0 cảnh báo.
- Điều mình học được hôm nay: Hiểu rõ nguyên lý camera cận hồng ngoại NIR (940nm), cách tính chỉ số buồn ngủ EAR/PERCLOS, khắc phục triệt để lỗi quên đổi thuộc tính mặc định `seat=driver` trên SVIRO và lỗi cảm quan ánh sáng `light=day`.
