# Báo cáo rà soát vòng 3 – SRS OMTS v5.8 (bản 07/10/2026)

- Cách làm: 2 reviewer độc lập (A: dữ liệu, trạng thái, phân quyền, BR/MSG/NFR; B: đặc tả UC, FR, màn hình, JOB/API) → kiểm tra chéo báo cáo của nhau → gộp → kiểm tra cuối trên văn bản gốc.
- Phạm vi: toàn bộ phần chữ; không rà sơ đồ, hình.
- Không lặp lại các lỗi đã báo ở vòng 2 (K19, K26, K30, K34, K39, K43, K46, N1–N13); phần cuối chỉ bổ sung vị trí còn sót cho các lỗi đó.
- Số N là số dòng trong bản trích văn bản của file .docx. Khi sửa trong Word, hãy tìm theo trích dẫn hoặc theo mã UC/SCR/E/BR.


**Tổng: 46 mục. Cao 1, Trung bình 11, Thấp 34.**
- Đầu vào 58 mục, không mục nào bị bác bỏ.
- 11 cặp trùng được gộp thành 11 mục: A-01+B-06, A-03+B-07, A-04+B-03, A-07+B-05, A-08+B-16, A-09+B-19, A-10+B-10, A-14+B-30, A-19+B-34, A-20+B-09, A-22+B-23.
- A-12 không tính là lỗi mới; đã chuyển xuống phần bổ sung cho N6.
- 9 mục xác nhận một phần đã viết lại theo phần được xác nhận: A-01, A-04, A-06, A-21, B-04, B-20, B-22, B-23, B-33.

## Xử lý các chỗ bất đồng
- **A-01/B-06, hệ quả.** Điều chỉnh tạo ở UC39 nhận trạng thái đầu Nháp (N=984). Chỉ UC53 chuyển được Nháp → Đã duyệt (N=1113), và E32 ghi "chỉ điều chỉnh Đã duyệt mới trừ công nợ" (N=703). Vì vậy hệ quả đúng là điều chỉnh mắc ở Nháp và không bao giờ tác động công nợ. Nhận định "Quản lý khu đổi công nợ mà không cần duyệt" của A bị bỏ.
- **A-01/B-06, mức độ: chốt Cao.** BR-23 là quy tắc đã chốt về tiền. Chiều tăng phải thu hoàn toàn không có đường. Chiều giảm chỉ có thể đi vòng qua UC53, và khi đó đơn bị coi là "đã được giảm giá" theo BR-15.
- **B-01: chốt Trung bình (B đặt Cao).** Chủ HTX có quyền Full ở mọi khu (N=1328) nên đơn vẫn xử lý được. Hậu quả chỉ là thiếu khu và Quản lý khu bị chặn.
- **A-09/B-19: chốt Thấp.** FR-UC49 (N=4362) và nhánh 2b đã cho ghi tiền ứng trước, nên lỗi là mâu thuẫn ở Preconditions cộng với thiếu truy vết, không phải chặn thật.
- **A-11: chốt Thấp.** Các phần quy phạm (UC70, ma trận, mục 4.1, BF-09) đã thống nhất; chỉ hai câu ghi chú lỗi thời.
- **A-06: chốt Thấp, viết lại.** UC31 không giới hạn khu (N=2298), dữ liệu nhập cho chọn vùng (N=2279, N=2309), và Chủ HTX vẫn làm được.
- **B-16 (gộp A-08): chốt Trung bình.** Lương tháng từng người không lưu được thì UC59 1a không tính được.
- **A-14 và B-30: gộp.** Cùng gốc ở các dòng chuyển sang Đã rút của Bảng 3.4-2 (N=1100–1103).

---

## Cao

### F-01. Phiếu điều chỉnh tiền khi sửa cân sau bán không đi tới được Đã duyệt
- Mức độ: Cao
- Nguồn: A-01 + B-06
- Vị trí: E32 (N=701, N=703, N=705); E26 (N=633); Bảng 3.4-2 (N=1113); BR-23 (N=5227); UC39 (N=2452, N=2458); FR-UC39 (N=4058); UC53 (N=2891, N=2893); SCR-23 (N=4168–4173); UC48 1g (N=2724); FR-UC48 (N=4219); MSG43 (N=5286); UC46 (N=2666)
- Trích dẫn: UC39 2a3 "Chênh lệch tiền ghi bằng phiếu điều chỉnh gắn giao dịch gốc; không ghi đè kg, QR hay công nợ" (N=2458); E32 "UC53 lưu điều chỉnh ở trạng thái Nháp; chỉ điều chỉnh Đã duyệt mới trừ công nợ" (N=703); "Nháp → Đã duyệt | UC53 | Chủ HTX | … Rà căn cứ và mức giảm" (N=1113); UC53 Preconditions "có thỏa thuận giảm giá" (N=2893); UC48 1g1 "điều chỉnh sau bán dùng UC51–UC54. (MSG43)" (N=2724)
- Lỗi:
  - Phiếu "tăng/giảm do sửa cân" (E32 N=701) được tạo ở UC39 nên mang trạng thái đầu Nháp, nhưng chỉ UC53 có chuyển sang Đã duyệt. UC53 chỉ lập điều chỉnh giảm giá mới, không có bước duyệt phiếu sẵn có. Vì vậy chênh lệch do sửa cân không bao giờ vào công nợ.
  - Chiều tăng phải thu không có đường nào. Chiều giảm nếu đi qua UC53 thì đơn bị coi là "đã được giảm giá" (BR-15).
  - SCR-23 không có trường phiếu cân mới hay điều chỉnh. "Used in" của E32 và E26 không có UC39.
  - Thương lái "xác nhận trong app" (FR-UC39, BR-23) nhưng không có UC hay màn hình nào cho việc này (UC46 chỉ xem).
  - UC48 1g, FR-UC48 và MSG43 hướng việc sửa cân hoặc nguồn sang UC51–UC54, trái với BR-23.
- Sửa: Cho UC39 2a3 tạo SaleAdjustment ở Nháp và để Chủ HTX duyệt. Thêm dòng UC39 vào Bảng 3.4-2 với điều kiện áp dụng cho cả loại tăng. Thêm UC39 và SCR-23 vào "Used in" của E32, E26, và thêm trường vào SCR-23. Thêm bước xác nhận cân mới cho thương lái (UC46 hoặc SCR-30), hoặc đưa Thương lái thành actor của UC39. Sửa UC48 1g, FR-UC48 và MSG43 thành "sửa cân hoặc nguồn qua UC39; giảm giá hoặc trả hàng qua UC51–UC54".

## Trung bình

### F-02. Điều kiện chặn Ngừng dùng của Khách hàng và Người nhận khoán không có trong UC42 và UC55
- Mức độ: Trung bình
- Nguồn: A-04 + B-03
- Vị trí: E22 (N=583); E38 (N=775); 3.4.3 (N=1127, N=1136, N=1137); UC42 (N=2541); UC55 (N=2958, N=2959); SCR-26 (N=4240); MSG11 (N=5254); MSG61 (N=5304)
- Trích dẫn: "Customer … Còn đơn chưa ở Đã chốt bán … hoặc đơn Đã chốt bán chưa quá 24 giờ" (N=1136); "Contractor … Còn quyết toán chưa Đã chi đủ" (N=1137); UC42 1b1 "đánh dấu ngừng… kết thúc thành công" (N=2541); UC55 "Exception Flows | Không có." (N=2959)
- Lỗi: UC42 không kiểm điều kiện chặn. UC55 1b (N=2958) cho đổi trạng thái mà không kiểm còn quyết toán chưa Đã chi đủ. MSG11 và MSG61 không có UC42, UC55 trong ngữ cảnh, và SCR-26, SCR-39 không có thông báo tương ứng.
- Sửa: Thêm EF chặn vào UC42 và UC55 (MSG11). Bổ sung MSG vào SCR-26, SCR-39 và vào ngữ cảnh của MSG11.

### F-03. Điều kiện "được giao phụ trách đơn" không có dữ liệu để kiểm
- Mức độ: Trung bình
- Nguồn: A-05
- Vị trí: E23 (N=593); mục 4.1 (N=1181); BF-04 (N=163); UC11 (N=1845, N=1848); UC44 (N=2598); Preconditions của UC32, UC39, UC45, UC48 (N=2333, N=2456, N=2626, N=2721); V.3.2 (N=5366)
- Trích dẫn: "zone_id (khu phụ trách đơn)" (N=593); "Chủ HTX chọn khu phụ trách đơn" (N=2598); "một khu có thể có nhiều tài khoản cùng vai trò, kể cả Quản lý khu" (N=1845); "Quản lý khu phải được giao phụ trách đơn" (N=2721)
- Lỗi: Không có bước giao người phụ trách và không có thuộc tính lưu người đó. Vì một khu có nhiều Quản lý khu, điều kiện này không phân biệt được ai.
- Sửa: Hoặc thêm người phụ trách (account) vào E23, UC44 và SCR-28. Hoặc định nghĩa "người phụ trách đơn = Chủ HTX hoặc mọi Quản lý khu có cặp khu – vai trò hiệu lực tại khu phụ trách", rồi sửa Preconditions các UC cho thống nhất.

### F-04. Quyết định "nhận trả toàn bộ đơn" cho yêu cầu chất lượng không có chuyển trạng thái đơn
- Mức độ: Trung bình
- Nguồn: A-02
- Vị trí: E31 (N=689); BF-05 (N=181, N=185); Bảng 3.4-2 (N=1089, N=1106); UC51 (N=2829); UC52 (N=2858, N=2860); SCR-36 (N=4432, N=4436); BR-15 (N=5219)
- Trích dẫn: "Chờ quyết định → Đang xử lý | … nhận trả toàn bộ đơn" (N=1106); chuyển duy nhất tới Đã chấp nhận trả là "Yêu cầu trả hàng → Đã chấp nhận trả" (N=1089); UC51 3b1 "vẫn gửi được yêu cầu chất lượng hoặc giảm giá" (N=2829)
- Lỗi: Với yêu cầu chất lượng, đơn đang ở Đã chốt bán (kể cả đã quá 24 giờ) nhưng UC52 vẫn cho chọn "nhận trả". Không có chuyển Đã chốt bán → Đã chấp nhận trả, nên chuyển này bị chặn (BR-30). Nếu cho chuyển thì lại vượt qua luật 24 giờ của BR-15.
- Sửa: Chỉ cho chọn "nhận trả toàn bộ đơn" khi đơn đang ở Yêu cầu trả hàng; ghi điều kiện này ở UC52, E31, SCR-36. Hoặc thêm chuyển có điều kiện và sửa BR-15.

### F-05. "Quá hạn giữ" chỉ tính khi hàng ở Đang giữ tạm, nên hàng đã đánh giá nhưng chưa bán không được nhắc
- Mức độ: Trung bình
- Nguồn: A-03 + B-07
- Vị trí: E33 (N=715); Bảng 3.4-1 (N=1035); Bảng 3.4-2 (N=1111); Bảng 3.4-3 (N=1160); BF-05 (N=193); UC52 (N=2858); JOB-07 (N=5014, N=5015, N=5021); BR-22 (N=5226)
- Trích dẫn: "“Quá hạn giữ” suy ra khi ở Đang giữ tạm quá 3 ngày chưa bán lại" (N=715); BR-22 "quá 3 ngày chưa bán lại thì cảnh báo Chủ HTX" (N=5226)
- Lỗi: Muốn bán lại phải qua Đã đánh giá (N=1111), nên hàng ở Đang giữ tạm không thể "đã bán lại". Điều kiện hiện tại loại đúng trường hợp BR-22 và JOB-07 muốn nhắc.
- Sửa: Định nghĩa lại: quá 3 ngày kể từ khi ghi hàng trả thực nhận mà chưa ở Đã xử lý xong. Sửa đồng bộ E33, Bảng 3.4-1, Bảng 3.4-3 và JOB-07.

### F-06. Danh sách thời vụ theo ngày và người nhận khoán của ngày không được UC nào lưu
- Mức độ: Trung bình
- Nguồn: A-07 + B-05
- Vị trí: E38 (N=773); E39 (N=785, N=788); E41 (N=809); UC55 (N=2957, N=2958, N=2965); FR-UC55 (N=4494); SCR-39 (N=4507, N=4517); UC57 (N=3015); SCR-41 (N=4553–4557)
- Trích dẫn: UC55 "chọn người nhận khoán và ngày làm… trùng người – ngày" (N=2957); FR-UC55 "danh sách lao động thời vụ theo ngày" (N=4494); E39 "người nhận khoán của từng ngày lưu trên AttendanceRecord" (N=788)
- Lỗi:
  - E38 và E39 không có ngày, công việc, mức tiền hay người đại diện kèm hiệu lực (UC55 1a), nên dữ liệu UC55 nhập không có chỗ lưu.
  - contractor_id của ngày nằm ở E41, nhưng UC57 và SCR-41 không có bước hay trường chọn người nhận khoán. Vì vậy UC59 không có căn cứ để tính tiền "qua người nhận khoán".
- Sửa: Viết lại UC55 thành quản lý danh mục, không theo ngày, và chuyển việc chọn người nhận khoán của ngày sang UC57 (hoặc UC56) cùng SCR-41. Mô hình hóa hoặc bỏ "người đại diện".

### F-07. Mức lương tháng không gắn được với từng nhân viên; SCR-42 thiếu thao tác duyệt
- Mức độ: Trung bình
- Nguồn: A-08 + B-16
- Vị trí: E42 (N=821, N=822); Bảng 3.4-2 (N=1116, N=1117); UC58 (N=3045, N=3046, N=3048, N=3057); UC59 1a1 (N=3078); FR-UC58 (N=4497); SCR-42 (N=4564, N=4573–4577)
- Trích dẫn: E42 "đối tượng, mức lương tháng… | Khóa ngoại: status_id" (N=821–822); "Đối tượng: nhân viên chính thức hoặc lao động thời vụ" (N=3057); FR-UC58 "lương tháng của từng nhân viên chính thức" (N=4497)
- Lỗi: "Đối tượng" chỉ là loại người, không có employee_id, nên lương tháng từng người không lưu được và UC59 1a không tính được. SCR-42 chỉ có [Lưu phiên bản], không có Duyệt, Từ chối hay lý do từ chối, dù Bảng 3.4-2 bắt buộc lý do khi từ chối (N=1117).
- Sửa: Thêm employee_id vào E42 (bắt buộc với lương tháng) và trường chọn nhân viên vào UC58, SCR-42. Thêm [Duyệt], [Từ chối] và "Lý do từ chối*" vào SCR-42.

### F-08. Tin báo cho thương lái ngoài UC70 không có bản ghi gửi và không có kênh dự phòng
- Mức độ: Trung bình
- Nguồn: A-10 + B-10
- Vị trí: E22 (N=581); E47 (N=884); BR-26 (N=963); Bảng 3.4-2 (N=1089); UC44 (N=2598, N=2599); UC45 bước 4 (N=2627); UC52 bước 2 (N=2858); API-08 (N=5126); MSG66 (N=5309)
- Trích dẫn: "có tài khoản thì qua email, email không gửi được thì qua SMS (MSG66)" (N=1089); E47 "đúng một chứng từ nguồn: SalesOrder (xác nhận đơn), SaleTransaction…" (N=884); "tài khoản Zalo (tùy chọn…)" (N=581)
- Lỗi:
  - Tin báo chấp nhận trả (MSG66), báo hủy đơn (UC44 5a3) và báo số cân, giá (UC45 bước 4) không thuộc 5 loại chứng từ và không đi qua UC70. Vì không có bản ghi gửi, hệ thống không biết "email không gửi được" để chuyển sang SMS, và không thể kiểm hay gửi lại ở UC71.
  - UC44 và UC45 chỉ gửi qua Zalo. Khách không có Zalo (và không có tài khoản, với UC52) thì không nhận được tin nào.
- Sửa: Thêm loại "thông báo đơn" vào BR-26 và E47, hoặc cho UC44, UC45, UC52 gửi qua UC70. Bổ sung kênh dự phòng SMS hoặc email ở UC44, UC45, UC52 và Bảng 3.4-2.

### F-09. UC42 thiếu bước Chủ HTX ghép tay hồ sơ khách mà năm nơi khác dẫn tới
- Mức độ: Trung bình
- Nguồn: B-04 (viết lại theo phần đã xác nhận)
- Vị trí: UC01 (N=1541); UC02 (N=1573); UC05 (N=1663); UC42 (N=2541, N=2548, N=2555, N=2563); SCR-26 (N=4238); SCR-30 (N=4308); BR-34 (N=5238); E22 (N=581)
- Trích dẫn: UC01 5a1 "tạo hồ sơ khách mới gắn tài khoản; Chủ HTX ghép với hồ sơ offline (nếu có) ở UC42" (N=1541); UC42 3a1 "ghép tài khoản vào hồ sơ khi khớp chắc chắn, không tạo hồ sơ thứ hai" (N=2541)
- Lỗi: UC42 có trường và process "liên kết tài khoản" (N=2548, N=2563, N=4238), nhưng luồng không có bước ghép tay. Câu 3a1 trái với UC01 5a1: khách đăng ký bằng email đã có hồ sơ mới, nên việc ghép thực chất là gộp hai Customer, và chưa có quy tắc chuyển đơn, công nợ (E22 cho quan hệ 1–1).
- Sửa: Thêm vào UC42 nhánh "Chủ HTX ghép tài khoản với hồ sơ offline": chọn, xác minh, gộp đơn và công nợ, ghi nhật ký kiểm toán, có MSG. Sửa 3a1 cho khớp UC01.

### F-10. UC44 nhánh 2a và 2b bỏ qua bước chọn khu phụ trách
- Mức độ: Trung bình
- Nguồn: B-01
- Vị trí: Bảng 3.4-2 (N=1074, N=1078); UC44 (N=2598, N=2599, N=2606, N=2609–2612); SCR-28 (N=4264)
- Trích dẫn: "2a2. Đơn không đi qua UC30, UC31. Use Case tiếp tục UC45." và "2b2. … chuyển đơn sang Đã xác nhận … Use Case dừng lại." (N=2599); "Chờ xét → Đã xác nhận | … Xác nhận sản phẩm, lượng và khu phụ trách" (N=1074)
- Lỗi: Đơn bán lại và đơn được xác nhận sau đề xuất sửa không qua bước 3 (chọn khu) và bước 4 (gửi thông tin đơn). Các đơn này không có khu phụ trách, nên Quản lý khu không đạt Preconditions của UC30, UC31, UC45.
- Sửa: Kết thúc 2b2 bằng "tiếp tục bước 3". Thêm bước chọn khu (hoặc khu mặc định) và gửi thông tin đơn vào 2a.

### F-11. UC48 có luồng sửa đơn "trước khi giao" dù chỉ chạy sau bàn giao
- Mức độ: Trung bình
- Nguồn: B-02
- Vị trí: E48 (N=896); UC44 (N=2616); UC48 (N=2719, N=2721, N=2723); FR-UC48 (N=4219); SCR-28 (N=4281)
- Trích dẫn: "Trigger | UC45 gọi sau khi hàng đã bàn giao." (N=2719); "1a. Cần sửa điều khoản đơn trước khi giao." (N=2723)
- Lỗi: Nhánh 1a không thể xảy ra, và không UC nào khác cho sửa đơn ở Đã xác nhận hoặc Đang thu hoạch (UC44 2b chỉ áp dụng ở Chờ xét). Cụm "đóng đơn" ở 1b không ứng với trạng thái nào.
- Sửa: Chuyển việc sửa điều khoản trước bàn giao sang UC44 (có nhật ký kiểm toán), bỏ 1a khỏi UC48, sửa FR-UC48 và "UC liên kết", thay "đóng đơn" bằng hành động có thật.

### F-12. SCR-26 thiếu ô tài khoản Zalo; SCR-27 và SCR-28 thiếu trường cho đơn bán lại
- Mức độ: Trung bình
- Nguồn: B-08
- Vị trí: E23 (N=593); UC42 (N=2540); UC43 2a1 (N=2572); SCR-26 (N=4237); SCR-27 (N=4254–4256); SCR-28 (N=4274–4278); BR-22 (N=5226)
- Trích dẫn: UC42 "nhập tên, số điện thoại, liên hệ và tài khoản Zalo" (N=2540); SCR-26 "Kênh app/điện thoại/Zalo | Chọn từ danh sách" (N=4237); UC43 "ghi tham chiếu hàng trả (UC52) và QR nguồn cũ" (N=2572)
- Lỗi: Không có dữ liệu Zalo để ghép tin nhắn đến (API-09). Đơn bán lại không lưu được source_return_id và lượng phân bổ, nên giới hạn phân bổ của BR-22 không kiểm được.
- Sửa: Thêm "Tài khoản Zalo" vào SCR-26. Thêm "lần trả nguồn, QR nguồn, lượng phân bổ" vào SCR-27 và SCR-28.

## Thấp

### F-13. Change log ghi "bỏ bảng CX" nhưng bảng vẫn còn
- Mức độ: Thấp
- Nguồn: A-15
- Vị trí: N=38, N=76, N=5332, N=5370–5386
- Trích dẫn: "ma trận quyền, BR-25, bỏ bảng CX" (N=38); bảng CX-UC-01…13 (N=5370–5386)
- Lỗi: Change log không khớp nội dung, vì Definitions (N=76) và V.3 (N=5332) vẫn dẫn tới bảng CX.
- Sửa: Xóa bảng và các tham chiếu, chuyển các mục còn mở sang V.3.2. Hoặc sửa change log.

### F-14. Định nghĩa "Lô nguồn" là "Lần thu hoạch"
- Mức độ: Thấp
- Nguồn: A-17
- Vị trí: N=49, N=603, N=620, N=1020, N=2298
- Trích dẫn: "Lô nguồn | Lần thu hoạch cho một đơn bán đầu" (N=49); "HarvestEvent (Lần thu hoạch)" (N=1020)
- Lỗi: Một lô gồm nhiều lần thu, và tên định nghĩa trùng tên tiếng Việt của E24.
- Sửa: Định nghĩa lại: "tập hàng thu cho một đơn bán đầu, gồm một hay nhiều lần thu; một QR chung".

### F-15. BF-06 thiếu bước duyệt mức lương; BF-04 thiếu làn Kế toán
- Mức độ: Thấp
- Nguồn: A-21 (viết lại theo phần đã xác nhận)
- Vị trí: BF-04 (N=163, N=169); BF-06 (N=201, N=211); Bảng 3.4-2 (N=1116–1117); UC49 (N=2755); UC58 (N=3046)
- Trích dẫn: "Kế toán đặt đơn giá công nhật và lương tháng có hiệu lực (UC58)" (N=201); làn BF-04 "Người phụ trách đơn…; Chủ HTX (đính chính hồ sơ); Hệ thống OMTS" (N=163)
- Lỗi: Ở BF-06, mức do Kế toán nhập phải được Chủ HTX duyệt mới dùng được, nhưng luồng không có bước này và không có trạng thái PAY_RULE. Ở BF-04, bước 5 có UC49 (Chủ HTX hoặc Kế toán) nhưng không có làn Kế toán, và làn Chủ HTX chỉ ghi "đính chính hồ sơ".
- Sửa: Thêm bước "Chủ HTX duyệt mức lương (UC58)" và trạng thái PAY_RULE vào BF-06. Thêm làn Kế toán vào BF-04 và ghi rõ người làm bước 5.

### F-16. Mục 3.1 nói "9 nhóm entity" nhưng trường "Nhóm" có 21 giá trị
- Mức độ: Thấp
- Nguồn: A-16
- Vị trí: N=260, N=262; trường "Nhóm" ở N=322–946
- Trích dẫn: "khung và màu thể hiện 9 nhóm entity của mục 3.2" (N=260)
- Lỗi: Mục 3.2 không định nghĩa 9 nhóm nào, nên không đối chiếu được màu trên ERD với entity.
- Sửa: Gộp trường "Nhóm" về đúng 9 nhóm, hoặc thêm bảng ánh xạ nhóm ERD ↔ entity.

### F-17. Dữ liệu UC nhập vào nhưng entity không có chỗ lưu (E16, E18, E19, E20, E24/E25)
- Mức độ: Thấp
- Nguồn: A-20 + B-09
- Vị trí: E16 (N=509); E18 (N=533); E19 (N=545–546); E20 (N=557, N=560); E24 (N=605); E25 (N=617); UC26 (N=2200); UC27 (N=2233, N=2235, N=2243); UC31 (N=2298, N=2299); SCR-16 (N=4003–4004)
- Trích dẫn: UC27 "ghi Hoàn tất giai đoạn thả kèm lý do… nhập ngày đóng, tóm tắt" (N=2235); UC31 "nhập kg ước tính và ảnh lô" (N=2298); UC26 "chọn vùng, bè hoặc chu kỳ" (N=2200)
- Lỗi:
  - E16 không có mốc hoàn tất thả, lý do và tóm tắt đóng chu kỳ.
  - Không entity nào có ảnh lô hay lý do thu khác kế hoạch.
  - E19 bắt buộc cycle_id và không có zone_id, nên nhật ký cấp vùng không lưu được.
  - E20 không có khóa trỏ về phép đo bị hiệu chỉnh ("phiên bản bản ghi" chỉ dùng cho kiểm xung đột, N=560).
  - Preconditions UC27 chỉ đòi "quyền xem" (N=2233) dù UC27 có thao tác đóng chu kỳ.
- Sửa: Bổ sung các thuộc tính trên. Cho cycle_id của E19 tùy chọn và thêm zone_id. Thêm corrected_from_measurement_id vào E20. Sửa Preconditions UC27 thành quyền Sửa.

### F-18. Tiền ứng trước: Preconditions UC49 trái nhánh 2b; tín dụng không truy được về phiếu thu
- Mức độ: Thấp
- Nguồn: A-09 + B-19
- Vị trí: E34 (N=723); E36 (N=747, N=749); BR-24 (N=961, N=5228); UC49 (N=2759, N=2761); UC54 (N=2921); FR-UC49 (N=4362)
- Trích dẫn: "Preconditions | • Giao dịch bán đã chốt ở UC48." (N=2759); "2b. … chưa gắn đơn… tiền ứng trước" (N=2761); E36 "tín dụng do… tiền đã thu chưa phân bổ" nhưng chỉ có "source_sale_id, source_adjustment_id" (N=747, N=749)
- Lỗi: Preconditions chặn khách trả trước khi có giao dịch nào, trái với 2b, FR-UC49 và BR-24. E36 không có khóa tới CustomerReceipt.
- Sửa: Đổi Preconditions thành "có hồ sơ khách (UC42)". Thêm source_receipt_id vào E36, hoặc ghi rõ số dư ứng trước được suy từ CustomerReceipt trừ ReceiptAllocation.

### F-19. PayLine không gắn với LaborSettlement
- Mức độ: Thấp
- Nguồn: A-13
- Vị trí: E43 (N=833–836); E44 (N=845–848); UC57 5a2 (N=3016); UC59 2b (N=3079); UC60 4b (N=3110)
- Trích dẫn: Khóa ngoại E43 "employee_id, worker_id, attendance_id, assignment_id, pay_rule_version_id" (N=834)
- Lỗi: Không biết dòng tiền nào đã nằm trong quyết toán Đã duyệt, nên không chặn được sửa (UC57 5a2) hay chốt trùng (UC60 4b).
- Sửa: Thêm settlement_id vào E43, hoặc ghi rõ quy tắc gom dòng theo người và kỳ ở E44.

### F-20. Các chuyển sang Đã rút: điều kiện chồng với Cần rà lại, và UC39 được ghi là UC thực hiện nhưng không có nhánh rút
- Mức độ: Thấp
- Nguồn: A-14 + B-30
- Vị trí: Bảng 3.4-2 (N=1100–1103); BF-08 (N=238, N=239, N=242); UC39 (N=2457–2460)
- Trích dẫn: "Đã công bố → Cần rà lại | … ảnh hưởng nội dung đã công bố" (N=1100); "Đã công bố → Đã rút | UC32, UC39 | … bị chứng minh sai" (N=1101); BF-08 "“Sai đã công khai?”: có thì rút công bố" (N=238)
- Lỗi: Hai chuyển có điều kiện chồng nhau mà không có tiêu chí chọn. Theo BF-08 thì luôn rút trước, nên chuyển sang Cần rà lại trong dòng Trạng thái của chính BF-08 (N=242) không xảy ra. UC39 được ghi là UC thực hiện chuyển sang Đã rút nhưng không có bước rút.
- Sửa: Nêu tiêu chí chọn giữa rút và đính chính, rồi sửa BF-08 bước 5. Bỏ UC39 khỏi hai dòng chuyển sang Đã rút, hoặc thêm nhánh rút (gọi UC32 1a).

### F-21. Ghi chú loại Quản lý khu khỏi UC70
- Mức độ: Thấp
- Nguồn: A-11
- Vị trí: N=1201, N=5377 (so với N=1187, N=1297, N=1411, N=248, N=3401)
- Trích dẫn: "gửi chứng từ (UC70) do Kế toán hoặc Chủ HTX thực hiện" (N=1201); "UC49 và UC70 do Kế toán" (N=5377)
- Lỗi: Hai câu ghi chú trái với UC70, ma trận quyền, mục 4.1, BF-09, và với việc UC48 (do Quản lý khu làm) luôn include UC70.
- Sửa: Sửa hai câu theo ma trận quyền.

### F-22. Kế toán "Xem mọi thông tin" trái ma trận; UC77 chỉ xem nhưng ghi Full
- Mức độ: Thấp
- Nguồn: A-18
- Vị trí: N=1206; ma trận N=1355–1358, N=1364–1367, N=1379, N=1405; UC77 N=2023
- Trích dẫn: "Kế toán | Toàn bộ khu | Xem mọi thông tin" (N=1206); "UC77 | … | Full | … | Full* | Full*" (N=1358)
- Lỗi: Ma trận ghi No cho Kế toán ở nhiều UC. UC77 chỉ đọc nhưng không ghi R như các UC xem khác.
- Sửa: Sửa N=1206 theo ma trận; đổi UC77 sang R hoặc R*.

### F-23. Còn câu ngụ ý người khác Chủ HTX được dùng UC09–UC11
- Mức độ: Thấp
- Nguồn: A-23 (B bổ sung N=1664)
- Vị trí: N=1337; BR-33 (N=969, N=5237); UC05 5a (N=1664); UC09 1a1 (N=1783); ma trận (N=1350–1352)
- Trích dẫn: "kể cả khi nhân viên có quyền Sửa trên chức năng tương ứng" (N=1337); "do người có quyền ở UC11 sửa" (N=969); "người có quyền ở UC11 vừa sửa" (N=1664); "chỉ cho xem nếu được cấp quyền" (N=1783)
- Lỗi: Ma trận ghi No cho mọi actor khác Chủ HTX ở UC09–UC11.
- Sửa: Viết lại các câu thành "chỉ Chủ HTX"; UC09 1a1 từ chối với MSG02.

### F-24. Danh mục API và giao tiếp ngoài thiếu UC đang dùng dịch vụ
- Mức độ: Thấp
- Nguồn: A-19 + B-34
- Vị trí: API-01 (N=1507, N=5032, N=5036); API-06 (N=1512, N=5097, N=5101); IV.1 (N=5173, N=5178); UC23 (N=2105, N=3969); UC51 (N=2822, N=4423); UC71 (N=3434); UC76 (N=1979, N=2004); JOB-02 (N=4946)
- Trích dẫn: UC76 "Secondary Actors | Dịch vụ lưu trữ đám mây" (N=1979); UC71 "Secondary Actors | … Dịch vụ SMS" (N=3434); SCR-35 "Bằng chứng | Tệp hoặc ảnh" (N=4423)
- Lỗi: API-06 và IV.1 thiếu UC76; API-01 và IV.1 thiếu UC71. UC23 và UC51 có tải tệp nhưng không khai báo Dịch vụ lưu trữ đám mây.
- Sửa: Bổ sung các UC này vào API-01, API-06, IV.1, III.14 và vào Secondary Actors của UC23, UC51.

### F-25. Lỗi gửi mã: UC08 chỉ MSG04, còn UC01, UC02 dùng MSG16
- Mức độ: Thấp
- Nguồn: B-11
- Vị trí: UC01 3a (N=1542); UC02 3c (N=1574); UC08 2a1 (N=1752); SCR-01 (N=3614); SCR-03 (N=3648); MSG04 (N=5247)
- Trích dẫn: "UC01, UC02, UC05 báo lỗi dịch vụ (MSG04)" (N=1752); UC02 "dịch vụ gửi mã lỗi … (MSG16)" (N=1574)
- Lỗi: Khi dịch vụ lỗi, người dùng nhận thông báo "mã không đúng" dù chưa có mã nào được gửi.
- Sửa: Tách nhánh dịch vụ lỗi ở UC01, UC02 sang MSG04. Thêm MSG04 vào SCR-01, SCR-03 và vào ngữ cảnh của MSG04.

### F-26. UC04: mã đổi mật khẩu qua email nằm ngoài chính sách mã và dùng sai MSG
- Mức độ: Thấp
- Nguồn: B-22 (viết lại theo phần đã xác nhận)
- Vị trí: UC04 (N=1636, N=1637); Bảng 3.4-3 (N=1157); MSG17 (N=5260)
- Trích dẫn: "2a2. Hệ thống gửi mã qua Dịch vụ email (BR-31)" (N=1636); "4a. Mật khẩu hiện tại hoặc mã sai… (MSG17)" (N=1637)
- Lỗi: Mã ở 2a2 không đi qua UC08 và không nằm trong dòng mã xác minh của Bảng 3.4-3 (thời hạn, số lần thử). Mã sai lại báo "Mật khẩu hiện tại không đúng". Gợi ý UC03 và UC11 ở 2b1 không áp dụng cho Quản trị hệ thống, dù actor này vẫn có đường qua UC05 rồi nhánh 2a.
- Sửa: Cho 2a gọi UC08, hoặc thêm UC04 vào Bảng 3.4-3 và JOB-01. Dùng MSG16 khi mã sai. Ghi rõ 2b1 áp dụng cho actor nào.

### F-27. Kết thúc nhánh sai loại hoặc trỏ bước làm mất hành vi
- Mức độ: Thấp
- Nguồn: B-35
- Vị trí: UC05 (N=1662, N=1663); UC46 (N=2668, N=2674); UC47 (N=2696, N=2702); UC48 4b (N=2724); UC54 1a (N=2923); Change log (N=38)
- Trích dẫn: UC05 3a2 "… Use Case tiếp tục bước 6." (N=1663); UC46 2a1 "không hiện chứng từ cũ… Use Case dừng lại" (N=2668)
- Lỗi:
  - Đổi email đi thẳng tới bước 6, bỏ qua bước 5 (ghi nhật ký kiểm toán).
  - UC46 và UC47 dừng hẳn, trong khi phác thảo vẫn hiện chứng từ mới.
  - UC54 1a là AF nhưng kết thúc "dừng lại"; UC48 4b là nhánh thành công nhưng nằm trong EF, trái change log N=38.
- Sửa: Cho 3a2 về bước 5. Chuyển UC46 2a và UC47 2b thành AF tiếp tục bước 3. Sửa cách kết thúc của UC54 1a, chuyển UC48 4b sang AF.

### F-28. UC09: phác thảo và dữ liệu nhập thiếu tài khoản ngân hàng bắt buộc
- Mức độ: Thấp
- Nguồn: B-14
- Vị trí: E01 (N=329); UC09 (N=1789, N=1792–1797, N=1806); FR-UC09 (N=3720); SCR-07 (N=3729, N=3744)
- Trích dẫn: "bắt buộc thêm tài khoản ngân hàng nhận chuyển khoản" (N=1806); SCR-07 "(7) Tài khoản nhận chuyển khoản*" (N=3729)
- Lỗi: Phác thảo và dữ liệu nhập của UC09 không có trường này, khác SCR-07, FR-UC09 và E01.
- Sửa: Thêm trường vào phác thảo và dữ liệu nhập của UC09.

### F-29. UC10 và V.3.2: mục mở đã chốt, nhãn trạng thái lệch danh mục
- Mức độ: Thấp
- Nguồn: A-22 + B-23 (bỏ ý "thiếu luồng Đã nghỉ → Đang làm", vì trường Tình trạng trong form sửa hồ sơ đã cho chọn, N=1822)
- Vị trí: Bảng 3.4-1 (N=995–996); UC10 (N=1822, N=1825, N=1837); FR-UC10 (N=3721); SCR-08 (N=3752); V.3.2 (N=5362)
- Trích dẫn: "Còn cần xác nhận: số điện thoại có bắt buộc với mọi nhân viên" (N=1837); V.3.2 "UC10 | Nhóm/Chủ HTX: danh mục tình trạng làm việc" (N=5362); "Tình trạng* [đang làm việc / ngừng làm việc]" (N=1822)
- Lỗi: Ghi chú UC10 còn hỏi việc đã chốt (V.3.2, N=1825). V.3.2 vẫn để mở danh mục tình trạng dù Bảng 3.4-1 đã chốt. Nhãn trạng thái không theo "Đang làm / Đã nghỉ".
- Sửa: Bỏ câu hỏi lỗi thời ở UC10 và mục mở ở V.3.2; dùng nhãn theo danh mục ở UC10 và SCR-08.

### F-30. MSG gọi sai ngữ nghĩa
- Mức độ: Thấp
- Nguồn: B-24
- Vị trí: UC20 2c (N=2053); UC22 2b (N=2083); UC26 1a2 và 6a (N=2201); UC32 4b (N=2336); UC43 1b (N=2573); 3.4.3 (N=1133–1135); MSG11 (N=5254); MSG27 (N=5270)
- Trích dẫn: UC20 2c1 "đổi sang Ngừng dùng thay vì xóa… (MSG11)" (N=2053); UC26 1a2 "lưu ngưỡng mới… (MSG27, MSG28)" (N=2201)
- Lỗi:
  - MSG11 ("không thể thực hiện") dùng cho thao tác đã thành công.
  - MSG27 ("vượt ngưỡng") dùng khi chỉ đổi ngưỡng, còn nhánh 6a (vượt ngưỡng thật) lại không có MSG.
  - MSG02 ("không có quyền") dùng cho lỗi lệch nội dung hai ngôn ngữ ở UC32 4b. Riêng UC43 1b dùng MSG02 thì có thể chấp nhận.
- Sửa: Dùng MSG phù hợp cho từng nhánh. Chuyển MSG27 sang 6a và tách nhánh lỗi riêng cho MSG28. Tách UC32 4b thành hai nhánh.

### F-31. "Giống liên quan", "Lưu nháp" phiếu thu và lựa chọn thanh toán không có chỗ lưu
- Mức độ: Thấp
- Nguồn: B-13
- Vị trí: E21 (N=569); E34 (N=727); ghi chú Bảng 3.4-2 (N=1093); UC20 và SCR-13 (N=2059, N=3920); UC49 và SCR-33 (N=2768); UC45 và SCR-29 (N=2645, N=4300)
- Trích dẫn: "[Sản phẩm] Mã* Tên* Giống liên quan" (N=2059); "Lưu nháp | Xác nhận tiền đã nhận" (N=2768); "Lựa chọn thanh toán ngay hoặc ghi công nợ — bắt buộc ghi nhận" (N=2645)
- Lỗi: E21 không liên kết giống. E34 không có trạng thái Nháp. Lựa chọn thanh toán không có thuộc tính, trái với ghi chú "tình trạng thanh toán suy ra từ công nợ" (N=1093).
- Sửa: Bỏ ba trường hoặc thao tác này, hoặc bổ sung thuộc tính tương ứng.

### F-32. UC22 và SCR-14: số điện thoại bắt buộc bị mất; còn sót trường đã bỏ
- Mức độ: Thấp
- Nguồn: B-12
- Vị trí: E14 (N=485); UC22 (N=2081, N=2089, N=2092–2094, N=2101, N=2102); FR-UC22 (N=3913); SCR-14 (N=3939, N=3943, N=3948–3950)
- Trích dẫn: "Đã chốt: bắt buộc tên và số điện thoại" (N=2102); SCR-14 "Thông tin liên hệ | … Theo thực tế" (N=3949); "giống có thể cung ứng" (N=3943); "Quan hệ nhà cung cấp ưu tiên" (N=3950)
- Lỗi: Phác thảo, dữ liệu nhập và SCR-14 không đánh dấu số điện thoại bắt buộc. "Mã" nhà cung cấp, "giống cung ứng" và "nhà cung cấp ưu tiên / nguồn gợi ý" không có trong E14.
- Sửa: Đánh dấu số điện thoại là bắt buộc; bỏ các trường thừa hoặc bổ sung chúng vào E14.

### F-33. Giống dự kiến: bắt buộc ở UC24 nhưng tùy chọn ở E16
- Mức độ: Thấp
- Nguồn: B-15
- Vị trí: E16 (N=509); UC24 (N=2149, N=2153); FR-UC24 (N=3976); SCR-16 (N=4000)
- Trích dẫn: "Giống dự kiến và ngày bắt đầu: bắt buộc." (N=2153); "planned_seed_type_id (giống dự kiến, tùy chọn)" (N=509); FR-UC24 "vùng nuôi lịch sử" (N=3976)
- Lỗi: Cùng một trường có hai mức bắt buộc khác nhau. Cụm "vùng nuôi lịch sử" ở FR-UC24 không rõ nghĩa và không có trong UC24.
- Sửa: Thống nhất một mức bắt buộc; bỏ cụm "vùng nuôi lịch sử".

### F-34. Điểm mở rộng không khớp quan hệ «extend»; UC32 nhánh 5b không có đường vào
- Mức độ: Thấp
- Nguồn: B-29
- Vị trí: Bảng include/extend (N=1286–1302); UC27 (N=2238); UC32 (N=2331, N=2335, N=2338); BF-02 (N=94, N=137); BF-08 (N=100, N=238)
- Trích dẫn: "Extension points: Đóng chu kỳ." (N=2238); "Extension points: Rút công bố; Phát hành nhãn QR; Gửi QR cho thương lái." (N=2338)
- Lỗi: Các điểm mở rộng này không có UC nào mở rộng. Ngược lại, quan hệ extend có thật (UC39 tại UC32 3a) và nhánh 4a lại không gắn nhãn điểm mở rộng. Nhánh 5b không được gọi từ UC45 (N=1295), cũng không có trong Trigger.
- Sửa: Bỏ các điểm mở rộng không dùng, và sửa theo ở BF-02, BF-08. Gắn nhãn cho 3a, 4a. Thêm Trigger cho 5b hoặc chuyển 5b sang UC45 1a.

### F-35. UC30 bước 2 và SCR-19 chỉ hiện bè của khu phụ trách dù nguồn có thể ở khu khác
- Mức độ: Thấp
- Nguồn: A-06 (viết lại theo phần đã xác nhận)
- Vị trí: E23 (N=596); BR-09 (N=956); UC30 (N=2266, N=2267, N=2279); UC31 (N=2297, N=2298, N=2309); SCR-19 (N=4066)
- Trích dẫn: "nguồn thu hoạch vẫn có thể từ khu khác" (N=596); "các bè thuộc khu" (N=2267)
- Lỗi: Câu chữ ở UC30 bước 2 và SCR-19 trái với E23 và BR-09, dù UC31 và các trường chọn vùng cho phép lấy nguồn ở khu khác. Quyền của Quản lý khu với bè ở khu khác chưa được nêu.
- Sửa: Sửa UC30 bước 2 và SCR-19 cho chọn bè ở khu khác, và nêu điều kiện quyền.

### F-36. UC41: Preconditions loại bản Đã rút nhưng nhánh 1a lại xử lý bản đã rút
- Mức độ: Thấp
- Nguồn: B-18
- Vị trí: UC41 (N=2511, N=2513); JOB-04 (N=4982)
- Trích dẫn: "Lô có bản công bố ở Đã công bố (không ở Cần rà lại hay Đã rút)" (N=2511); "1a. Bản công bố đã bị rút…" (N=2513)
- Lỗi: Thông báo hủy lên cổng quốc gia không bao giờ chạy được.
- Sửa: Mở Preconditions cho trường hợp bản đã đồng bộ trước đó vừa bị rút.

### F-37. UC45: thứ tự chốt giá và rà, công bố khác nhau giữa các phần
- Mức độ: Thấp
- Nguồn: B-28
- Vị trí: BF-04 (N=165–167); UC45 (N=2627, N=2638, N=2656); FR-UC45 (N=4216)
- Trích dẫn: luồng chính chốt giá ở bước 3, rà ở bước 5 (N=2627); process 2 "chờ rà/công bố rồi thống nhất giá" (N=2656)
- Lỗi: Process, tiến trình ở phác thảo và FR-UC45 ngược thứ tự với luồng chính và BF-04.
- Sửa: Thống nhất theo luồng chính và BF-04.

### F-38. UC52 5b2 giao việc ghi tín dụng cho UC50, trong khi UC50 chỉ đối soát
- Mức độ: Thấp
- Nguồn: B-31
- Vị trí: E36 (N=747); UC50 (N=2793); UC52 (N=2859); FR-UC50 (N=4363)
- Trích dẫn: "5b2. UC50 ghi tín dụng, UC54 ghi tiền thực hoàn." (N=2859)
- Lỗi: Không UC nào tạo bản ghi CustomerCredit.
- Sửa: Cho hệ thống tạo CustomerCredit khi Chủ HTX lưu quyết định ở UC52.

### F-39. UC56 và UC57 không chặn nhân viên Đã nghỉ
- Mức độ: Thấp
- Nguồn: B-33 (chỉ giữ phần nhân viên; người nhận khoán và thời vụ Ngừng dùng đã bị ẩn theo quy định chung ở N=979)
- Vị trí: Bảng 3.4-1 (N=996); BF-06 (N=211); UC56 (N=2989); UC57 (N=3017)
- Trích dẫn: "LEFT | Đã nghỉ | Không giao việc, chấm công mới" (N=996); UC57 "Exception Flows | Không có." (N=3017)
- Lỗi: Quy tắc của trạng thái Đã nghỉ không được thể hiện trong UC và không có MSG.
- Sửa: Thêm EF chặn nhân viên Đã nghỉ vào UC56, UC57 (MSG61).

### F-40. Công thức giá hiệu lực của UC66 chưa định nghĩa mức tính
- Mức độ: Thấp
- Nguồn: B-20 (viết lại theo phần đã xác nhận)
- Vị trí: UC66 (N=3287, N=3309); FR-UC66 (N=4663)
- Trích dẫn: "Giá hiệu lực = (giá trị bán gốc − giảm giá − tín dụng hàng trả) / (kg cân chốt − kg hàng trả)" (N=3309)
- Lỗi: Không rõ công thức tính theo đơn hay gộp theo kỳ. Nếu tính theo đơn thì với đơn trả toàn bộ, mẫu số bằng 0.
- Sửa: Ghi rõ mức tính (gộp theo kỳ và sản phẩm) và cách xử lý khi mẫu số bằng 0.

### F-41. UC71 thử lại có thể gửi "bản mới", trái FR-UC71 và BR-26
- Mức độ: Thấp
- Nguồn: B-32
- Vị trí: E47 (N=881, N=884); UC71 (N=3439); FR-UC71 (N=4779); SCR-55 (N=4827)
- Trích dẫn: "hệ thống cho biết sẽ gửi lại phiên bản cũ hay bản mới" (N=3439); FR-UC71 "không tự thay bằng bản mới" (N=4779)
- Lỗi: Với QR truy xuất, bản mới là một publication_id khác, nên lần thử lại sẽ đổi chứng từ nguồn.
- Sửa: Thử lại luôn gửi đúng phiên bản gốc; muốn gửi bản mới thì tạo lần gửi mới ở UC70.

### F-42. "Thông báo liên quan" của SCR lệch với UC; 5 SCR không có dòng này
- Mức độ: Thấp
- Nguồn: B-25 (bỏ con số "37" chưa tái lập được)
- Vị trí: SCR-05 (N=3698); SCR-07 (N=3746); SCR-08 (N=3767); SCR-09 (N=3789); SCR-13 (N=3933); SCR-14 (N=3952); SCR-18 (N=4047); SCR-27 (N=4258); SCR-40 (N=4538); SCR-34, 39, 41, 42, 51
- Trích dẫn: SCR-18 "MSG07 …; MSG26 …; MSG27 …; MSG28" (N=4047), trong khi UC26 dùng MSG06, MSG58, MSG11
- Lỗi:
  - Thiếu MSG mà UC dùng: SCR-05 thiếu MSG10, MSG18; SCR-07, 08, 13, 14 thiếu MSG10; SCR-27 thiếu MSG02; SCR-40 thiếu MSG41.
  - SCR-09 có MSG11 dù UC11 không dùng.
  - SCR-34, 39, 41, 42, 51 không có dòng "Thông báo liên quan".
  - Nhiều SCR có MSG01 trong bảng trường nhưng không có trong dòng này.
- Sửa: Đồng bộ dòng "Thông báo liên quan" với MSG trong UC.

### F-43. Bảng trường SCR: loại nhập sai và số mục lệch phác thảo
- Mức độ: Thấp
- Nguồn: B-26
- Vị trí: N=3765, N=3832–3833, N=3856, N=3929–3930, N=3968, N=4003–4004, N=4043–4044, N=4317, N=4334, N=4383, N=4443, N=4464, N=4466, N=4484, N=4653, N=4716–4717, N=4752, N=4795
- Trích dẫn: SCR-37 "Giao dịch gốc và lý do chất lượng | Loại nhập: Số" (N=4464); SCR-51 "Kỳ — bắt buộc… Bắt buộc: Không" (N=4752)
- Lỗi: Loại nhập không đúng kiểu dữ liệu. Số mục trỏ sai trên phác thảo. Một số câu ghi chú bị đưa thành trường (N=4653, N=4795).
- Sửa: Sửa loại nhập và số mục; đưa các câu ghi chú ra khỏi bảng trường.

### F-44. Bảng FR: đặt sai nhóm, sai dạng, lệch UC
- Mức độ: Thấp
- Nguồn: B-27
- Vị trí: FR-UC18 (N=3816); FR-UC27 (N=3979); FR-UC30 (N=4052); FR-UC70 (N=4778); FR-UC76, FR-UC77 (N=4844–4845)
- Trích dẫn: FR-UC18 "Tôi với vai trò là Chủ HTX hoặc Quản lý khu, tôi muốn…" (N=3816)
- Lỗi:
  - FR-UC76 và FR-UC77 nằm trong bảng III.12 thay vì III.3.
  - FR-UC18 viết dạng user story và thiếu UC76, chặn Ngừng dùng, BR-25.
  - FR-UC27 dùng tên cũ.
  - FR-UC30 lệch chủ thể so với Trigger UC30.
  - FR-UC70 thiếu QR thanh toán và phiếu thu.
- Sửa: Chuyển FR-UC76, FR-UC77 sang III.3 và viết lại các FR trên theo UC.

### F-45. SCR-43 thiếu phần lương tháng và dòng khoán việc
- Mức độ: Thấp
- Nguồn: B-17
- Vị trí: E43 (N=833); UC59 (N=3078); SCR-43 (N=4584, N=4592–4595)
- Trích dẫn: UC59 "1a1. Người thao tác chọn tháng… 1a2. … khoản cộng/trừ kèm lý do" (N=3078)
- Lỗi: Màn hình không nhập được tháng, nhân viên, khoản cộng/trừ và lý do, cũng không có vùng cho dòng khoán việc ở 1b.
- Sửa: Thêm tab "Lương tháng" và vùng "Dòng khoán việc đã nghiệm thu".

### F-46. SCR-52 ghi mở từ SCR-47, nhưng UC68 không mở rộng UC63
- Mức độ: Thấp
- Nguồn: B-21
- Vị trí: N=1298–1301, N=3346, N=4671, N=4757
- Trích dẫn: "Mở từ các màn hình báo cáo SCR-47 đến SCR-51." (N=4757)
- Lỗi: UC68 chỉ mở rộng UC64–UC67, và SCR-47 không có nút Xuất.
- Sửa: Sửa thành "SCR-48 đến SCR-51".

---

## Bổ sung cho danh sách đã biết
- **K19:** Còn ở chính UC24: phác thảo "Người phụ trách/bối cảnh làm việc" (N=2149) và dữ liệu nhập "Người phụ trách/lô giống dự kiến" (N=2154).
- **K34:** Còn ở hàng BF-03 của bảng tổng hợp BF (N=95), mô tả SCR-28 trong danh sách màn hình (N=1470) và Purpose của API-04 (N=5070).
- **N1:** Cùng lỗi "liên hệ Chủ HTX… (UC11)" còn ở phác thảo UC03 (N=1613), SCR-04 mục (7) (N=3654), UC04 2b1 (N=1636) và FR-UC03 (N=3591). Với tài khoản Chủ HTX, đường đúng là UC74.
- **N5:** Phác thảo UC44 (N=2606) và dữ liệu nhập (N=2609–2612) cũng không có khu phụ trách. Lỗi luồng liên quan xem F-10.
- **N6 (phạm vi rộng hơn mô tả, từ A-12):** Quy định "dữ liệu chung HTX chỉ vai trò gán ở Toàn bộ khu" (N=1337; các entity ở N=488, N=500, N=584, N=776, N=788, N=812) còn mâu thuẫn với:
  - mô tả Quản lý khu ở mục 4.1 (N=1187) và bảng vai trò (N=1205);
  - BF-02 bước 2 (N=130), BF-06 bước 2 và 4 (N=202, N=204);
  - Preconditions UC22 (N=2080), UC23 (N=2109), UC42 (N=2539), UC55 (N=2956), vốn không đòi Toàn bộ khu.
  Hệ quả: Quản lý khu gán ở một khu không làm được UC22, UC23, UC42, UC55, UC57.
- **N10:** "Farming zone" còn ở dữ liệu nhập UC30 (N=2279); "cả chuyến" còn ở dữ liệu nhập UC31 (N=2312).
- **K39:** Đúng. "Chủ HTX (Owner)" ở N=1185 và N=1328 chỉ là chú thích, chấp nhận được.
- **Mục "Đã kiểm và khớp":**
  - "MSG ngữ cảnh khớp UC" có ngoại lệ: UC08 2a1 (N=1752) chỉ định MSG04 cho UC01, UC02 nhưng ngữ cảnh MSG04 (N=5247) không có hai UC này (xem F-25).
  - "Mọi UC có FR" đúng, nhưng FR-UC76, FR-UC77 đặt sai nhóm (xem F-44).
