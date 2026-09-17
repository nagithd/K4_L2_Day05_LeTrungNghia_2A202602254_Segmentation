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

Kết quả tự kiểm ngày 2026-09-17: cả 9 ZIP đều `[OK]` về cấu trúc. Các export COCO dùng RLE; `medium_instance` có 49 annotations, `hard_panoptic` có 62, `cp1_holes` có 6, `cp2_slice` có 13 và `cp5_occlusion` có 35. Toàn bộ 24 unit tests của repo đã chạy thành công khi bật chế độ UTF-8.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: **[CẦN XÁC NHẬN: ghi tên ảnh, vị trí và object đầu tiên bạn tự vẽ]**
- Class và quy tắc tôi dùng để chọn biên: **[CẦN XÁC NHẬN: class và cách xử lý phần nhìn thấy/che khuất]**
- Nếu dùng gợi ý sau đó: có dùng automatic annotation; **[CẦN XÁC NHẬN: nêu một vùng đã sửa hoặc giữ và lý do]**
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: **[CẦN XÁC NHẬN: chọn một lỗi annotation bạn thực sự đã phát hiện]**
- Lỗi thuộc loại: **[CẦN XÁC NHẬN: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác]**
- Bằng chứng tôi nhìn thấy: **[CẦN XÁC NHẬN]**
- Quy tắc và hành động sửa: **[CẦN XÁC NHẬN]**
- Sau sửa đã Save và export lại chưa? **[CẦN XÁC NHẬN]**

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm — release chính thức `day5-reference-v1` chưa tồn tại và scorer báo `Protected reference missing` cho cả Easy, Medium và Hard. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | `cp4_curb` — **[CẦN XÁC NHẬN VỊ TRÍ]** | road hay sidewalk | Ranh theo chức năng và bó vỉa, không chỉ theo màu | **[CẦN XÁC NHẬN QUYẾT ĐỊNH]** |
| 2 | `cp2_slice` — **[CẦN XÁC NHẬN VỊ TRÍ]** | một mask hay hai instance xe | Hai vật cùng class sát nhau vẫn là hai instance | **[CẦN XÁC NHẬN QUYẾT ĐỊNH]** |
| 3 | `cp5_occlusion` — **[CẦN XÁC NHẬN VỊ TRÍ]** | một instance bị che hay hai object | Chỉ vẽ phần nhìn thấy nhưng giữ đúng định danh một vật | **[CẦN XÁC NHẬN QUYẾT ĐỊNH]** |
