# Danh sách lớp v0 — Trần Anh Văn · G10

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (Driver Monitoring System — 7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_state` | open / closed / unknown | Tính tỷ số EAR và tỷ lệ PERCLOS để phát hiện tài xế nhắm mắt ngủ gật (micro-sleep) $\ge 1.5$ giây, kích hoạt chuông báo động | Có, trừ khi bị đốm lóa phản xạ LED trên kính hoặc tròng kính quá tối |
| 2 | `gaze_zone` | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung (distraction) khi mắt tài xế rời khỏi đường quá 2.0 giây (quy chuẩn EU ADDW), cảnh báo chuyển hướng chú ý | Có, xác định qua góc đồng tử và hướng mặt |
| 3 | `head_pose` | yaw / pitch / roll (góc quay đầu) | Hỗ trợ ước lượng hướng chú ý khi mắt bị che khuất; phát hiện tài xế gục đầu khi ngủ sâu hoặc quay đầu nói chuyện | Có, tính toán qua mô hình PnP từ các điểm mốc mặt (landmarks) |
| 4 | `hand_on_wheel` | yes / no / unknown | Giám sát tài xế có duy trì tay trên vô lăng không để đáp ứng tiêu chuẩn hỗ trợ lái rảnh tay (Euro NCAP Hands-off warning) | Có, qua vùng tiếp xúc giữa bàn tay và vành vô lăng |
| 5 | `phone_interaction` | held / mounted / lap | Phát hiện hành vi sử dụng điện thoại khi đang lái xe (phân biệt điện thoại trên giá đỡ để xem bản đồ vs cầm tay nhắn tin) | Có, qua hình khối chữ nhật và viền phản xạ của thân máy |
| 6 | `driver_seatbelt` | worn_correct / worn_incorrect / not_worn / unknown | Cảnh báo thắt dây an toàn và điều chỉnh thuật toán kích nổ túi khí trước khi xảy ra va chạm | Có, qua dải dây vắt chéo từ vai xuống hông đối diện |
| 7 | `mouth_state` | open_wide (ngáp) / normal | Bổ sung phát hiện cử chỉ ngáp sâu kéo dài báo hiệu giai đoạn chớm mệt mỏi, buồn ngủ (EU DDAW) | Có, đo khoảng cách giữa mí môi trên và môi dưới |

## OMS (Occupant Monitoring System — 7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `seat_occupancy` | person / empty / child_seat / infant_seat / object (theo từng ghế) | Đếm số lượng hành khách, lập bản đồ phân bố tải trọng khoang sau để nhắc dây an toàn từng ghế và tùy biến nổ túi khí rèm | Có, nhận diện qua hình dạng cơ thể và đồ vật |
| 2 | `infant_seat_facing` | rear / front | Tự động vô hiệu hóa túi khí ghế trước nếu có nôi em bé quay ngược lưng, tránh túi khí bung gây chấn thương sọ não trẻ | Có, nhận diện qua hướng đặt quai xách và phom nôi cong |
| 3 | `child_presence` | no / unknown (hỗ trợ sensor fusion yes) | Cảnh báo trẻ em bị bỏ quên trong xe đóng kín dưới trời nắng (Euro NCAP Child Presence Detection - CPD) sau khi tắt máy | Có, nếu trẻ không bị chăn hoặc áo khoác trùm kín |
| 4 | `rear_seatbelt` | worn_correct / worn_incorrect / not_worn / unknown | Nhắc nhở người ngồi hàng ghế sau thắt dây an toàn đúng cách theo tiêu chuẩn an toàn xe hơi | Có, nếu độ tương phản giữa dải dây và áo đủ rõ |
| 5 | `forgotten_object` | bag / box / cup / other | Cảnh báo hành lý, túi xách, máy tính xách tay để quên trên ghế khi chủ xe khóa cửa rời đi; chống mất trộm đồ | Có, qua hình khối ba lô, thùng hộp trên ghế |
| 6 | `passenger_out_of_position` | normal / leaning / feet_on_dash | Phát hiện tư thế ngồi sai nguy hiểm (nghiêng người sát cửa sổ, gác chân lên taplo) để giảm lực bung túi khí tránh gãy chân | Có, nhận diện qua tư thế khung xương thân người |
| 7 | `camera_occlusion` | yes / no | Phát hiện camera trần xe bị hành khách treo áo khoác, đồ đạc che khuất ống kính để báo lỗi hệ thống an toàn cabin | Có, toàn bộ khung hình bị tối đen hoặc mất nét hoàn toàn |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Trong trường hợp nôi em bé (`infant_seat`) hoặc ghế trẻ em bị phủ chăn mỏng kín người, camera quang học và hồng ngoại IR đều không thể nhìn xuyên qua vải để xác định có trẻ hay không. Khi đó trong Guideline quy định nhãn `occupied = unknown` có đủ để bàn giao cho mô hình OMS không, hay hệ thống bắt buộc phải tích hợp luồng tín hiệu từ cảm biến Radar sóng milimet 60 GHz (đo nhịp thở lồng ngực) vào chung nhãn ontology?
   * **Khung ví dụ:** `S06_ir.png` (nôi em bé đặt ở vị trí ghế sau).
   * **Bạn tạm gán thế nào và vì sao:** Tạm gán `infant_seat` kèm thuộc tính `facing = rear` và để các thuộc tính che khuất là `unknown`. Lý do: Tuân thủ quy tắc vàng 4.4-1 của Guideline: "Không thấy thì unknown", không võ đoán sự hiện diện bên dưới lớp vải khi dữ liệu chỉ có ảnh thị giác đơn thuần.

2. **Câu hỏi:** Trên ảnh hồng ngoại thật Drive&Act (DMS), khi tài xế đeo kính râm có lớp tráng phủ phản xạ NIR một phần, tạo ra đốm lóa sáng (glare) che khuất mắt trái nhưng mắt phải nhìn thấy rõ con ngươi đang mở. Khi tính chỉ số PERCLOS cho toàn bộ khuôn mặt, mô hình nên nội suy mắt trái từ mắt phải hay bắt buộc đánh dấu lỗi cảm biến cho khung hình đó?
   * **Khung ví dụ:** `D01.png` (đốm sáng lóa trên mắt kính tài xế).
   * **Bạn tạm gán thế nào và vì sao:** Tạm gán độc lập `eye_left = unknown` và `eye_right = unknown` (do mắt nghiêng khuất), kính gán `glasses = clear/sun`. Lý do: Guideline 4.5 quy định rõ `eye_left` và `eye_right` phải gán riêng từng mắt và không được suy từ mắt còn lại, đảm bảo dữ liệu trung thực cho bộ ước lượng độ tin cậy của mô hình.
