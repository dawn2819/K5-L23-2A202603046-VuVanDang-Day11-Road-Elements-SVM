# Báo cáo cá nhân — Ngày 11
Họ tên: Vũ Văn Đăng               Mã học viên: 2A202603046  
Phiên bản CVAT (Help → About): CVAT 2.15.0 (hoặc bản web lớp)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 08:45 UTC+7    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | `lane` (polyline), `road_curb` (polyline), `crosswalk` (polygon), `drivable` (polygon), `traffic_light` (rectangle), `traffic_sign` (rectangle) |
| Thuộc tính và giá trị | Đúng | Đủ các thuộc tính: position (L1/R1/L2/R2/other), style, color, kind, area_type, edge_zone,... |
| 4 tag ảnh | Đúng | `camera`, `timeofday`, `weather`, `source` đều có thuộc tính select `value` |
Cách kết thúc polyline trên bản CVAT này: Nhấp đúp chuột trái vào điểm cuối (hoặc phím tắt `N` để kết thúc vẽ).  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ Tag (hoặc chọn label kiểu Tag ở panel phải), chọn giá trị tương ứng trong menu select `value`.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 24 | 9 | 9 | 30 | 27 | 13 |
| front-extra (đã làm 4 / 4) | 4 | 9 | 2 | 8 | 9 | 9 | 11 |
| fisheye | 8 | 6 | 8 | 8 | 10 | 4 | 9 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 0 | 5 | 8 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05, A06, A07, A08, A09, A10, A14 | lane | Vẽ bịa thêm vạch L1/R1 hay để trống / gán road_curb | Không vẽ vạch lane ở phía mép đường không có sơn, chỉ gán road_curb | Ảnh thực tế không có vạch sơn kẻ đường (mép đường là vỉa hè hoặc không kẻ vạch). Tuân thủ guideline Road v1.0 không vẽ bịa vạch, áp dụng quy tắc miễn trừ coach waiver |
| A04, A09, A11, A14 | lane | Vẽ 2 polyline riêng cho 2 dải vạch hay 1 polyline trung tâm | 1 polyline ở tâm vạch với thuộc tính `kind = double` | Theo taxonomy Road v1.0, vạch đôi là 1 polyline mang thuộc tính `kind=double`, tránh làm mô hình hiểu nhầm thành 2 làn xe riêng biệt |
| B05, B06, B07, B08 | lane | position = L1/R1 hay other | `position = other` | Theo quy tắc camera góc hông (fisheye_left / fisheye_right), mọi vạch làn bắt buộc gán `position = other` |
| B02, B03, B04, B05 | traffic_light / traffic_sign | Bật hay tắt cờ `edge_zone` | Bật `edge_zone = true` khi tâm box nằm ngoài 80% bán kính | Tuân thủ quy tắc ảnh fisheye: các đối tượng nằm ngoài 80% bán kính vòng ảnh bị méo quang học mạnh |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Bùi Thảo Linh  Quyết định nhận được: Release (sau khi khắc phục các góp ý)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-01 tag camera | 3 | Đồng ý | Đã sửa: bổ sung 4 tag ở B04; đổi camera B06, B10 thành fisheye_left |
| QC1-04 tâm vạch, chiều | 1 | Đồng ý | Đã sửa: đảo chiều polyline A16 vẽ từ gần xe ra xa |
| QC1-05 vạch đứt, che | 4 | Đồng ý | Đã sửa: gộp các cặp polyline vạch đôi ở A04, A09, A11, A14 thành 1 polyline kind=double |
| QC1-11 fisheye | 1 | Đồng ý | Đã sửa: thêm điểm theo cung cho lane ở B05 (đủ >= 4 điểm) và cập nhật edge_zone |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| VuVanDang-front.zip | Có (pass `road_check lint`) | 11 / 11 | 8 / 8 | Có (`camera = front`) |
| VuVanDang-fisheye.zip | Có (pass `road_check lint`) | 4 / 4 | 4 / 4 | Có (`camera = fisheye_front`) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `docs/images/screenshots/01_project_labels.png` (minh chứng 6 labels và 4 tags).
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): `docs/images/screenshots/02_front_annotated_A01.png` (ảnh A01 đủ lane, drivable, road_curb, traffic_sign).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: `docs/images/screenshots/03_fisheye_curve_B01.png` (ảnh B01 phóng to cung cong fisheye).
4. Một đoạn XML có `<polyline label="lane">`: `docs/images/screenshots/04_xml_lane_snippet.png` (trích xuất thẻ polyline lane trong annotations.xml).

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
- Lỗi mắc nhiều nhất là QC1-05 (vẽ tách 2 polyline riêng cho vạch đôi thay vì 1 polyline mang `kind=double`) và QC1-01 (nhầm tag camera fisheye_right thay vì fisheye_left).
- Cách tránh ở Ngày 20: Tự chạy script `road_check lint` liên tục sau mỗi task để phát hiện sớm các cảnh báo taxonomy và tag, kiểm tra kỹ quy tắc gán nhãn trước khi export.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
- Nhãn `lane` đi vào module phát hiện vạch làn (Lane Detection) và giữ làn tự động (Lane Keeping Assist - LKA).
- Chọn lỗi QC1-04 (vẽ ngược chiều từ xa về gần ở A16): Mô hình học chuỗi điểm theo hướng di chuyển của xe (từ gần ra xa để nội suy góc lái). Nếu vẽ ngược chiều, vector hướng của làn bị đảo ngược 180 độ, khiến thuật toán điều khiển của xe hiểu sai hướng chuyển động của làn đường, có thể dẫn đến đánh lái sai hướng hoặc phanh gấp.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | không có làn | không có làn | 602.6 | 542.7 | 484.5 |
| x của bạn kia | không có làn | không có làn | 604.1 | 543.8 | 485.2 |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?  
   - Hàng y = 640 sẽ đổi thành "không có làn" (vì điểm cuối không chạm tới hàng y đó).
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?  
   - Ở hàng 720: Cả hai đều không có vạch (lệch 0 px). Ở hàng 560: Lệch nhau khoảng 0.7 px (|484.5 - 485.2|).  
   - Lệch ở các hàng gần xe hơn (gần đáy ảnh, như y = 680 hay 640) ảnh hưởng đến LKA nhiều hơn, vì đây là vị trí sát thân xe nhất, quyết định góc lái trực tiếp tức thời để giữ xe nằm giữa làn.
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?  
   - Phép nội suy tìm tọa độ giao cắt x tại từng hàng y không đổi kết quả hình học; tuy nhiên các script xử lý chuỗi dựa vào điểm đầu tiên gần xe nhất (như kiểm tra độ dốc, hướng vector xe chạy, hoặc model hồi quy dự đoán điểm kế tiếp) sẽ gặp khó khăn và xử lý sai hướng.
