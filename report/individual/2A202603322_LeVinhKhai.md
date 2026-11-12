# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603322 
- Ngày / CVAT local: 11/11/2026
- Công cụ đã dùng: CVAT local, Segment Anything (SAM ViT-H), Git/GitHub

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | chưa có | … / 1 | 3 |
| cp2_slice | chưa có | … / 1 | 3 |
| cp5_occlusion | chưa có | … / 1 | 3 |
| cp3_thin | chưa có | … / 1 | 3 |
| cp4_curb | chưa có | … / 1 | 3 |
| cp6_coverage | chưa có | … / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: 000000181542.jpg, người phụ nữ đứng ở chính giữa ảnh, object PERSON 14 (MANUAL), class person.
- Class và quy tắc tôi dùng để chọn biên: tôi chọn class person vì đây là một người riêng biệt. Tôi tự vẽ mask theo đúng phần cơ thể nhìn thấy, bám sát biên đầu, tóc, thân, tay và chân; không lấy nền, xe máy hoặc các vật thể xung quanh vào mask. Với phần bị che khuất, tôi không tự suy đoán biên ẩn phía sau vật khác.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do:  Sau object đầu tiên, tôi dùng gợi ý tự động từ Segment Anything (SAM ViT-H) cho một số object tiếp theo. Tôi không giữ nguyên kết quả máy một cách tự động mà kiểm tra lại class, số lượng instance và đường biên của từng mask. Khi SAM ăn sang nền, lấy nhầm phần của object bên cạnh hoặc bỏ sót một phần nhìn thấy, tôi chỉnh lại bằng công cụ mask/eraser trong CVAT trước khi Save.
Quyết định giữ/sửa gợi ý: Tôi chỉ giữ gợi ý khi mask bám đúng vật thể và không làm gộp hai instance. Nếu biên chưa đúng hoặc ăn sang nền, tôi sửa lại thủ công trước khi lưu.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: hard_panoptic, ảnh 000000350023.jpg, khu vực xa ở giữa ảnh có các cột/cụm đèn giao thông nhỏ.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: thiếu vật / thiếu vùng
- Bằng chứng tôi nhìn thấy:  Khi xem toàn ảnh ở mức zoom bình thường, một số cột và cụm đèn ở xa rất nhỏ nên tôi đã bỏ sót. Sau khi phóng to, tôi vẫn nhận ra được hình dạng và vị trí của các object này.
- Quy tắc và hành động sửa: Quy tắc và hành động sửa: Tôi zoom vào khu vực xa, kiểm tra lại class của task Hard và bổ sung mask cho các object còn nhìn thấy đủ rõ; không tự gán nhãn cho những vùng quá mờ hoặc không chắc chắn.
- Sau sửa đã Save và export lại chưa? Có, tôi đã Save lại annotation và export lại hard_panoptic.zip.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| hard_panoptic, ảnh 000000350023.jpg, người rất nhỏ và mờ ở khu vực gần đèn giao thông trong ảnh | Có thể là một person đang đi bộ; hoặc người đó đang ngồi/đi trên một phương tiện nên không thể xác định chính xác object cần gán | Kích thước object quá nhỏ và hình ảnh bị mờ, không đủ chi tiết để xác định chắc chắn tư thế hoặc việc người đó có đang gắn với một phương tiện hay không. Guideline yêu cầu không tự suy đoán khi không đủ bằng chứng quan sát | Tôi quyết định không gán nhãn cho trường hợp này để tránh đoán sai class hoặc tạo annotation không chắc chắn | 
| hard_panoptic, ảnh 000000460147.jpg, các phương tiện rất xa ở cuối đường | Có thể tiếp tục gán các object này vào car, truck hoặc class phương tiện phù hợp; hoặc bỏ qua vì ảnh quá nhỏ và mờ nên không đủ căn cứ phân biệt class | Ở khoảng cách xa, một số phương tiện chỉ còn vài cụm pixel, hình dáng thân xe và các đặc điểm phân biệt giữa car, truck hoặc class khác không còn rõ. Guideline yêu cầu không bịa class khi pixel không đủ để quyết định | Tôi chỉ gán nhãn cho những phương tiện còn đủ rõ để xác định class; các phương tiện quá nhỏ hoặc quá mờ thì không gán để tránh suy đoán sai |
| medium_instance, ảnh 000000458325.jpg, xe đẩy ở khu vực giữa ảnh | Có thể có một em bé/người ngồi trong xe đẩy và cần gán thêm person; hoặc xe đẩy che khuất phần bên trong nên không thể xác định có em bé hay không | Phần bên trong xe đẩy bị mờ và che khuất, không nhìn thấy đủ đặc điểm cơ thể để xác nhận một person. Guideline yêu cầu chỉ gán theo phần nhìn thấy và không tự suy đoán object bị che | Tôi quyết định không tạo thêm instance person cho phần bên trong xe đẩy vì không có đủ bằng chứng quan sát để xác nhận có em bé/người ở đó |
