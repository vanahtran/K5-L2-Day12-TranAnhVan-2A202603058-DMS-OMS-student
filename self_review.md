# Tự đánh giá — Trần Anh Văn · G10

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | child_seat (ghế trái ảnh) | `ok` | Gán chuẩn seat=rear_right theo xe, không bị lật theo góc nhìn màn hình | Rồi |
| S02_rgb.png | frame_meta | `guess` | Ban đầu để light=day theo cảm quan ảnh màu, đã đổi về unknown theo chuẩn ảnh 3D SVIRO | Rồi (ở v2) |
| D01.png | face13 | `extra` | Mặt quay đi bị che khuất hết điểm, vẽ skeleton có toàn bộ điểm outside=1; đã bỏ skeleton chỉ giữ box face | Rồi (ở v2) |
| D04.png | hand | `ok` | Cả hai tay buông rời vô lăng, gán đúng on_wheel=no theo đặc thù xe tự lái thử nghiệm | Rồi |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Gán thuộc tính `light = day` trên các ảnh RGB của bộ ảnh SVIRO (S02 đến S08).

Vì sao mình mắc: Theo thói quen quan sát thông thường, thấy ảnh màu ban ngày sáng rõ nên tiện tay chọn `day` mà quên mất quy tắc cốt lõi của bài: SVIRO là ảnh tổng hợp 3D mô phỏng, không có thời gian thực nên quy chuẩn bắt buộc là `unknown`.

Lần sau tránh bằng cách: Đọc kỹ các ràng buộc đặc thù của từng dataset trong guideline trước khi bắt đầu; kiểm tra bằng script ngay từ Checkpoint A để bắt lỗi hệ thống và không lặp lại ở các ảnh sau.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: Ở khung hình `D06.png`, thuộc tính `gaze_zone` của tài xế. Mình gán `road` do thấy hướng người quay về phía trước, nhưng bạn chỉ ra rằng góc đầu và mí mắt đang cụp xuống vùng đùi (`gaze_zone = lap`). Sau khi phóng to quan sát trục mắt, mình đã đồng thuận theo bạn sửa thành `lap`.

Mình học được gì từ dòng đó: Khi gán hướng nhìn (gaze zone), không được chỉ nhìn tư thế thân người mà phải kết hợp góc nghiêng của đầu (head pose) và khe mắt để xác định vùng chú ý thật sự của tài xế.
