# TEAM — Ngày 12

Mã bộ ảnh: **G10** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Trần Anh Văn | 2A202603058 | có | Đinh Hữu Minh (ongbin123 - G10) | 55 |

Các ca thảo luận đối chiếu chéo chuyên sâu giữa hai bạn (ghi tên ảnh + đối tượng):

1. **`D01.png` (Dây an toàn & Khung xương mặt tài xế)**:
   - *Dây an toàn (`seatbelt`)*: Văn ban đầu gán `worn_correct` do thấy dải dây chéo vắt qua người; Minh Hữu đề xuất giữ `unknown` vì tài xế đang dùng hai tay kéo dây cài vào khóa, chưa xác định dây đã cài ổn định. Theo Guideline §4.4-1 và §4.7 không được gán `worn_correct` chỉ vì thấy dải dây chéo. Văn hoàn toàn đồng thuận theo Minh Hữu đổi về `unknown`.
   - *Khung xương (`face13`)*: Văn vẽ skeleton có 13 điểm `outside=1` do đầu tài xế ngoảnh xa camera; Minh Hữu đề xuất không vẽ. Theo Guideline §4.6 ("không thấy mặt rõ thì không vẽ skeleton"), Văn đồng thuận lược bỏ skeleton trên D01 ở bản `export_final_v2.zip` giúp kiểm tra đạt 0 lỗi 0 cảnh báo.

2. **`D05.png` (Trạng thái mắt trái & Vùng nhìn `gaze_zone`)**:
   - *Mắt trái (`eye_left`)*: Minh Hữu gán `open`, Văn gán `closed` do mí mắt tài xế sụp sâu khi nhìn xuống. Hai bạn xác định đây là ca ranh giới rất khó giữa liếc mắt xuống lòng đùi và nhắm mắt thực sự trên ảnh NIR góc nghiêng.
   - *Vùng nhìn (`gaze_zone`)*: Minh Hữu gán `lap` (lòng đùi), Văn ban đầu gán `center`. Văn đồng thuận theo Minh Hữu gán `lap` vì trục mắt chúc thẳng xuống đùi/vô lăng. Riêng ca mắt mở/nhắm được giữ lại trong log để xin ý kiến coach phân xử ngưỡng PERCLOS.

3. **`S01_ir.png` / `S01_rgb.png` (Biên hộp đối tượng cốc nước `object`)**:
   - Hai bạn cùng phát hiện cốc nước nhưng IoU < 0.5 do box của Văn bị kéo rộng sang phần khóa dây an toàn bên cạnh. Minh Hữu phân tích và đề xuất giữ box sát thân cốc. Văn đồng thuận theo Minh Hữu căn chỉnh lại mép hộp bám sát biên thực tế đối tượng theo Guideline §4.4-5 và §4.8.

4. **`S03, S05, S07, S08` (Hướng quay nôi em bé `infant_seat facing` & Ghế trẻ em `child_seat occupied`)**:
   - *Hướng nôi (`facing`)*: Minh Hữu chỉ rõ nguyên tắc xác định hướng quay của nôi em bé phải dựa trên cấu trúc đầu và chân của trẻ so với hướng xe chạy (đầu áp lưng ghế sau, chân hướng mũi xe $\rightarrow$ `front`) theo Guideline §4.1 và §4.4-3, không được nhìn theo quai xách.
   - *Ghế trẻ em (`occupied`)*: Đối với ghế trống quan sát rõ lòng ghế không có vật che, hai bạn thống nhất gán `occupied = no` thay vì phân vân `unknown`.

## Cá nhân

### TranAnhVan-2A202603058
- **Phần mình làm**: Tự gán toàn bộ 22 ảnh cốt lõi (16 ảnh OMS S01–S08 RGB/IR và 6 ảnh DMS D01–D06), chạy script tự kiểm qua các mốc Checkpoint A/B/Final, nhận file export và file review từ bạn Đinh Hữu Minh (`ongbin123`), đối chiếu 55 điểm khác biệt, phân tích nguyên nhân và tiếp thu các phản biện chuẩn xác để hoàn thiện bản `export_final_v2.zip` đạt 0 lỗi 0 cảnh báo.
- **Điều mình học được hôm nay**: Nắm vững kỹ thuật đối chiếu chéo (peer diff) trong dự án dữ liệu xe tự hành thực tế; hiểu sâu nguyên lý "không thấy thì unknown" (không suy đoán trạng thái dây an toàn hay hướng nôi khi chưa đủ bằng chứng); phân biệt bản chất vật lý giữa ảnh NIR thực (Drive&Act 940nm) và ảnh mô phỏng 3D (SVIRO `light=unknown`).
