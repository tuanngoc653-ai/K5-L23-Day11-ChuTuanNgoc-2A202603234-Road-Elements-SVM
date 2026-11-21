# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): dohoanganh        Người kiểm (học viên): chutuanngoc
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): `dohoanganh-front.zip`, `dohoanganh-fisheye.zip` (không nhận được manifest đi kèm, nên không có `revision`)
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 83

Mẫu kiểm: A01, A04, A08, A11 (front) · B02 (fisheye_front), B08 (fisheye_right). Mỗi ảnh được mở với nhãn vẽ chồng lên ảnh gốc và phóng to ở chỗ nghi ngờ; cả hai file cũng được chạy `road_check lint`.

| Ảnh | Shape | Tag | Tổng |
| --- | ---: | ---: | ---: |
| A01 | 10 | 4 | 14 |
| A04 | 12 | 4 | 16 |
| A08 | 19 | 4 | 23 |
| A11 | 8 | 4 | 12 |
| B02 | 5 | 4 | 9 |
| B08 | 5 | 4 | 9 |
| **Tổng** | **59** | **24** | **83** |

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 8 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 | 2 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 22 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 14 | 2 | nặng |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 23 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 9 | 1 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 10 | 3 | chính |
| QC1-12 file | lỗi file | 2 | 7 | nhẹ |

Ngoài bảng: 1 lỗi nhẹ về tag `weather` (A04), xem lỗi số 12.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-08 | A08 | traffic_light #3 | nặng | Đèn hướng về xe (facing front) đang sáng **xanh** nhưng gán `color = yellow` (vỏ đèn màu vàng, đèn sáng là xanh). |
| 2 | QC1-08 | B02 | traffic_light #3 | nặng | Đèn bên phải, facing front, phóng to thấy đèn xanh đang sáng nhưng gán `unknown` (xem ca mơ hồ). |
| 3 | QC1-05 | A04 | lane #9, #10 | chính | Vạch vàng đôi tim đường vẽ thành 2 polyline cùng L1; phải là 1 polyline ở giữa hai vệt sơn, `kind = double`. |
| 4 | QC1-05 | A11 | lane #1, #7 | chính | Vạch đôi bên trái vẽ thành 2 polyline cùng L1; phải là 1 polyline. |
| 5 | QC1-06 | A11 | lane #1, #7 | chính | Vạch đôi tim đường là màu vàng (pixel sơn R≈G>B, khác mặt đường ám xanh lúc chạng vạng) nhưng gán `color = white`. |
| 6 | QC1-07 | A04 | drivable #0 | chính | Làn đang đi (giữa vạch vàng L1 và R1) gán `area_type = alternative`; ảnh không có vùng `direct` nào. |
| 7 | QC1-07 | B02 | road_curb (thiếu) | chính | Mép vỉa hè bên phải (phía người đi bộ) nhìn rõ, không sơn, nhưng chưa gán `road_curb`; chỉ có curb bên trái (#4). |
| 8 | QC1-10 | A01 | traffic_sign (thiếu) | chính | Thiếu biển xanh nhỏ ở xa, khoảng (432,463)–(449,489), cao 26 px (≥ 8 px nên bắt buộc gán). |
| 9 | QC1-11 | B02 | traffic_light #2 | chính | Tâm box ngoài 80 % bán kính vòng ảnh nhưng `edge_zone = false`; phải bật. |
| 10 | QC1-11 | B02 | traffic_light #3 | chính | Như lỗi 9: `edge_zone` phải bật. |
| 11 | QC1-11 | B08 | lane #4 | chính | Polyline fisheye chỉ có 3 điểm; cần đặt điểm dày theo cung. |
| 12 | QC1-01 (tag khác) | A04 | tag weather | nhẹ | Trời nhiều mây xám, đường khô: nên là `overcast`, đang gán `clear` (guideline mục 3, tag weather). |
| 13 | QC1-12 | A04 | drivable #0, road_curb #1, drivable #11 | nhẹ | Điểm lặp liền nhau (click hai lần), 3 shape. |
| 14 | QC1-12 | A08 | lane #17 | nhẹ | 3 điểm lặp liền nhau. |
| 15 | QC1-12 | A11 | crosswalk #2 | nhẹ | 1 điểm lặp. |
| 16 | QC1-12 | B02 | crosswalk #0, drivable #1 | nhẹ | Điểm lặp, 2 shape. |

(Mục 13–16 là 7 shape có điểm lặp, đếm là 7 lỗi nhẹ QC1-12.)

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| B02 | Đèn #3 (phải, facing front): đèn xanh sáng mờ dưới nắng. Gán `unknown` có được chấp nhận không, hay bắt buộc `green`? Người kiểm đã chọn mức cao hơn (nặng). | (chờ) |
| A11 | Vạch đôi trái lúc chạng vạng: người kiểm đo màu sơn thấy ngả vàng nên coi là `yellow`. Nếu lead coi là trắng thì bỏ lỗi số 5. | (chờ) |
| A04 | Tag weather `clear` hay `overcast`: trời phủ mây xám, không thấy nắng. Lỗi chỉ ở mức nhẹ, không đổi kết luận. | (chờ) |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 9 / 83 nhãn = 10,8 %   Lỗi nhẹ: 8   Ca chờ lead: 3
Quyết định (Release / Hold / Rework): **Rework**
Lý do (theo luật của phiếu): có lỗi nặng (lỗi số 1: sai màu đèn hướng về xe ở A08). Kể cả khi lead xử ca mơ hồ theo hướng có lợi cho người làm (bỏ lỗi số 2 và 5), vẫn còn 1 lỗi nặng, và tỉ lệ lỗi chính 8 / 83 = 9,6 % vẫn trên 5 %. Ca mơ hồ không đổi kết luận nên không Hold.

### Ghi chú ngoài mẫu (từ `road_check lint`, chưa kiểm bằng mắt, không tính vào tỉ lệ)
- A14 (ảnh thêm) chưa có nhãn nào; nếu không làm thì nên bỏ khỏi file thay vì để trống.
- QC1-02: A05 thiếu L1, R1; A06 thiếu R1; A09 thiếu R1. Bạn tự kiểm xem có thật không thấy vạch không; nếu không thấy thì xin coach xác nhận.
- QC1-05: A09 có 2 polyline cùng L2 (nhiều khả năng cũng là vạch đôi bị tách như A04, A11).
- QC1-12: tổng cộng 25 shape có điểm lặp trên toàn lô.
- Box nhỏ hơn 8 px (không bắt buộc): A03 traffic_light #1, A10 traffic_sign #11.

Gợi ý sửa nhanh: mở Details của từng polyline vạch đôi, xoá một polyline, kéo polyline còn lại vào giữa hai vệt sơn và đặt `kind = double`; kiểm lại màu của mọi đèn facing front bằng cách phóng to; bật `edge_zone` cho đèn và biển gần viền vòng ảnh fisheye; chạy lại `road_check lint` trước khi export.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
