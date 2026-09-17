# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602254
- Ngày / CVAT local: 2026-09-17 / `http://localhost:8080`
- Công cụ đã dùng: CVAT local, Mask/Brush, gợi ý automatic annotation và script kiểm tra submission của repo

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

Kết quả tự kiểm ngày 2026-09-17: cả 9 ZIP đều `[OK]` về cấu trúc. Các export COCO dùng RLE; `medium_instance` có 70 annotations, `hard_panoptic` có 78, `cp1_holes` có 6, `cp2_slice` có 13 và `cp5_occlusion` có 35. Với ground truth được phát trong lớp, scorecard ba tier đạt **48.0 / 82**: Easy **16.4 / 20** (mIoU 0.769), Medium **14.6 / 32** (mean matched IoU × recall 0.606) và Hard **17.0 / 30** (PQ 0.455). Ground truth chỉ dùng cục bộ để tự kiểm, không đưa vào submission hay Git.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, người đi bộ mặc áo sáng ở gần giữa ảnh.
- Class và quy tắc tôi dùng để chọn biên: gán class `person`; tôi vẽ sát phần cơ thể nhìn thấy, dừng ở nơi người bị xe máy che và không gộp xe máy hoặc nền vào mask người.
- Nếu dùng gợi ý sau đó: tôi dùng automatic annotation cho các object còn lại, nhưng kiểm lại class, số object và biên; các person/vehicle nhỏ hoặc xa không được coi là nền chỉ vì mask gợi ý thiếu.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `medium_instance`, `000000458325.jpg`, các người và phương tiện nhỏ/xa dọc đường.
- Lỗi thuộc loại: thiếu-thừa vật.
- Bằng chứng tôi nhìn thấy: scorer hiện còn TP 54, FP 16 và FN 17; tổng export có 70 object so với 71 object ground truth. Ở ảnh `000000458325.jpg`, các object nhỏ/xa là vùng dễ bị bỏ sót hoặc nhận nhầm.
- Quy tắc và hành động sửa: tôi rà từng person/bicycle/car/motorcycle/bus/truck còn nhìn thấy, bổ sung mask riêng cho object thiếu và xóa/sửa mask tràn sang object hoặc nền.
- Sau sửa đã Save và export lại chưa? Có. Bản export cập nhật tăng Medium từ 49 lên 70 annotation; điểm Medium tăng từ 7.7 lên 14.6 / 32, dù vẫn cần tiếp tục rà các object nhỏ.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): `medium_instance` tăng từ 7.7 lên 14.6 / 32 sau export cập nhật; recall@0.5 hiện là 0.76. Scorecard ba tier hiện là **48.0 / 82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | `cp4_curb`, `7d83710e-4697c3b2.jpg`, mép bó vỉa và phần lát bên phải | road hay sidewalk | Mặt vỉa hè và mặt đường có màu gần nhau, nhưng bó vỉa và chức năng lối đi bộ là bằng chứng chính | Chọn `sidewalk` cho phần lát/nâng bên phải bó vỉa; phần xe chạy bên trái là `road`. |
| 2 | `cp2_slice`, `000000017627.jpg`, các xe đỗ sát nhau ở giữa ảnh | một mask xe hay nhiều instance xe | Hai xe cùng class sát nhau vẫn là hai object nếu thấy khe hoặc biên riêng | Tách từng xe thành mask riêng, không dùng một mask lớn phủ nhiều xe. |
| 3 | `cp5_occlusion`, `000000336232.jpg`, phương tiện bị xe buýt/taxi hoặc xe khác che | một instance bị che hay hai object | Chỉ vẽ phần nhìn thấy nhưng không đổi định danh object vì vùng bị che | Giữ một mask cho mỗi phương tiện nhận diện được; không vẽ xuyên qua vật che và không tách một xe thành hai object. |
