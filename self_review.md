# Tự đánh giá — Trần Anh Văn · G10

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | child_seat (ghế trái ảnh) | `ok` | Gán chuẩn seat=rear_right theo xe, không bị lật theo góc nhìn màn hình | Rồi |
| S02_rgb.png | frame_meta | `guess` | Ban đầu để light=day theo cảm quan ảnh màu, bạn Hữu để unknown đúng chuẩn ảnh 3D SVIRO; đã đổi về unknown | Rồi (ở v2) |
| D01.png | face13 & seatbelt | `extra` / `guess` | Mặt quay đi bị che khuất hết điểm nhưng vẫn vẽ skeleton; tay đang kéo dây chưa cài đã gán worn_correct; bạn Hữu góp ý rất chuẩn; đã bỏ skeleton và đổi thành unknown | Rồi (ở v2) |
| D04.png | hand | `ok` | Cả hai tay buông rời vô lăng, gán đúng on_wheel=no theo đặc thù xe tự lái thử nghiệm | Rồi |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Gán thuộc tính `light = day` trên các ảnh RGB của bộ ảnh SVIRO (S02 đến S08).

Vì sao mình mắc: Theo thói quen quan sát thông thường, thấy ảnh màu ban ngày sáng rõ nên tiện tay chọn `day` mà quên mất quy tắc cốt lõi của bài: SVIRO là ảnh tổng hợp 3D mô phỏng, không có thời gian thực nên quy chuẩn bắt buộc là `unknown`. Bạn Hữu gán `unknown` chuẩn xác.

Lần sau tránh bằng cách: Đọc kỹ các ràng buộc đặc thù của từng dataset trong guideline trước khi bắt đầu; kiểm tra bằng script ngay từ Checkpoint A để bắt lỗi hệ thống và không lặp lại ở các ảnh sau.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: Ở khung hình `D01.png`, bạn Hữu không vẽ skeleton `face13` vì tài xế quay đầu che khuất toàn bộ mặt, đồng thời bạn Hữu chỉ ra rằng tài xế mới chỉ đang kéo dây cài chứ chưa cài khóa nên phải để `seatbelt = unknown`. Ban đầu mình vẫn vẽ skeleton và gán `worn_correct`. Đối chiếu Guideline §4.6 ("không thấy mặt thì không vẽ skeleton") và §4.7 ("không gán worn_correct chỉ vì thấy dải dây chéo"), bạn Hữu hoàn toàn đúng và mình đã tiếp thu sửa lại ở bản `export_final_v2.zip`.

Mình học được gì từ dòng đó: Khi gán nhãn cho xe tự hành, nguyên tắc an toàn hàng đầu là bám sát bằng chứng quan sát thực tế — không vẽ khung xương rỗng gây nhiễu mốc giải phẫu cho model và không suy đoán trạng thái an toàn (thắt dây) khi thao tác chưa hoàn tất.
