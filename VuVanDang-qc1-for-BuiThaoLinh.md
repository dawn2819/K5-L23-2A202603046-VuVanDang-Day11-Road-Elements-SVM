# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Bùi Thảo Linh       Người kiểm (học viên): Vũ Văn Đăng  
Ngày: 2026-11-21                         Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): BuiThaoLinh-front.zip, BuiThaoLinh-fisheye.zip (`revision`: 1)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 58  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 8 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 12 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 14 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 6 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 8 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 6 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 10 | 0 | chính |
| QC1-12 file | lỗi file | 58 | 1 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A01 | lane#2 | chính | Điểm cuối vạch L1 kéo quá xa chân trời (> 5 px so với điểm kết thúc thực tế) |
| 2 | QC1-07 | A03 | drivable#1 | chính | Polygon drivable tràn nhẹ lên gờ vỉa hè phía bên phải |
| 3 | QC1-12 | A04 | road_curb#1 | nhẹ | Có 1 điểm click đúp lặp liền nhau |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A02 | Vạch sơn phân làn bên phải bị bóng râm cây che khuất một đoạn 3m, có cần bật cờ occluded không? | Đã bật occluded theo quy tắc nối qua vật cản / bóng che ngắn. |

## Quyết định
Lỗi nặng: 0   Lỗi chính: 2 / 58 nhãn = 3.45 %   Lỗi nhẹ: 1   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): Release  
Lý do (theo luật của phiếu): Lô kiểm không có lỗi nặng; tỉ lệ lỗi chính là 3.45% (< 5% ngưỡng cho phép); không còn ca mơ hồ chờ lead giải quyết.  

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
