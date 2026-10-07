# Danh sách lỗi – SRS v5.8 (OMTS)

- **Tài liệu:** Report 3 – Software Requirement Specification v5.8 (07/10/2026)
- **Ngày rà soát:** 07/10/2026
- **Phạm vi rà soát:** toàn bộ phần chữ (mục I–V); không rà các sơ đồ (Context, BF, ERD, Use Case, State, Screen Flow).
- **Cách dùng:** đánh dấu `[x]` khi đã sửa. Mỗi mục ghi **Vị trí**, **Lỗi** và **Sửa** (đề xuất).

## Tổng quan

| Nhóm | Nội dung | Mục | Ưu tiên |
|---|---|---|---|
| A | Số liệu và tham chiếu sai | 1–8 | Trung bình |
| B | Quyết định mới chưa cập nhật hết | 9–13 | Cao |
| C | Mô hình dữ liệu không có chỗ chứa điều UC mô tả | 14–19 | **Cao nhất** |
| D | Phân quyền | 20–24 | **Cao nhất** |
| E | Vòng đời trạng thái | 25–30 | **Cao nhất** |
| F | Luồng UC mâu thuẫn | 31–38 | Cao |
| G | Thuật ngữ và biên tập | 39–47 | Thấp |

Đối chiếu tự động đã khớp (không cần sửa): 66 UC, 52 entity, 61 SCR, 45 trạng thái, 42 chuyển trạng thái; ma trận quyền khớp Primary Actors; mọi UC có FR; không có mã MSG nào được gọi mà chưa định nghĩa.

---

## A. Số liệu và tham chiếu sai

- [ ] **1. Mục I.3.3 – câu mở đầu**
  - Lỗi: ghi "17 quy tắc" nhưng bảng có 20 dòng (BR-01–04, 07, 09, 10, 18, 19, 21, 24–30, 32–34); ghi "toàn bộ 30 quy tắc ở V.1" nhưng V.1 có 34 (BR-01…BR-34).
  - Sửa: đổi thành 20 và 34.

- [ ] **2. Mục I.4.3 – đoạn mô tả sơ đồ Use Case**
  - Lỗi: ghi "UC08 chỉ chạy khi được UC01 include hoặc khi mở rộng UC03 («extend»)". Bảng include/extend ngay dưới, UC03 và ghi chú ma trận quyền lại ghi: UC03 «include» UC08; UC08 «extend» UC02 và UC05.
  - Sửa: "UC08 chỉ chạy khi được UC01, UC03 include hoặc khi mở rộng UC02, UC05 («extend»)".

- [ ] **3. Mục III.13 – cột "Nguồn" của JOB-01…07**
  - Lỗi: dùng cách đánh số nhánh cũ: "UC01 (luồng thay thế 2)", "UC15 (luồng thay thế 2)", "UC26 (luồng thay thế 4)", "UC32 (luồng thay thế 2)", "UC52 (luồng thay thế 5)", "UC70 (luồng thay thế 2)". UC01 hiện không có "luồng thay thế 2".
  - Sửa: đổi sang mã nhánh hiện hành (2a, 3a, 4a…).

- [ ] **4. Change Log – dòng 06/10/2026 (dòng đầu)**
  - Lỗi: "(V.3.1–V.3.6 thành V.3.1–V.3.6)" – trước và sau giống hệt nhau.
  - Sửa: ghi đúng số mục cũ → mới, hoặc bỏ cụm này.

- [ ] **5. Tên UC chưa cập nhật**
  - Lỗi:
    - FR-UC48, phác thảo SCR-32 ("[Đơn > Sửa và chốt]") và tên process UC48 vẫn là "Sửa và chốt giao dịch"; tên UC48 đã đổi thành "Chốt giao dịch bán" (03/10).
    - FR-UC32 ghi "Quản lý hồ sơ truy xuất và QR"; tên UC32 là "Rà soát và công bố hồ sơ truy xuất".
  - Sửa: dùng tên UC hiện hành.

- [ ] **6. Bảng V.1 Business Rules và V.2 System Messages lệch với UC**
  - Lỗi:
    - BR-32 được dùng ở UC02 nhưng cột Applies To không có UC02.
    - BR-33 liệt kê UC11, UC72, UC74 nhưng hàng "Business Rules / NFR" của ba UC này không ghi BR-33.
    - MSG62 và MSG67 ghi ngữ cảnh UC08 nhưng UC08 không dùng.
    - MSG02 được dùng ở UC43 (nhánh 1b) nhưng ngữ cảnh không ghi UC43.
  - Sửa: đồng bộ hai chiều.

- [ ] **7. E46 Notification và E48 AuditEvent**
  - Lỗi:
    - E46: Purpose và Used in thiếu nhắc hàng trả giữ tạm quá 3 ngày (JOB-07, MSG48, UC52).
    - E48, mục "Ghi": thiếu UC05, UC10, UC15, UC30, UC42, UC44, UC55, UC56, UC57, dù đặc tả các UC này đều ghi "ghi nhật ký kiểm toán".
  - Sửa: bổ sung các UC còn thiếu.

- [ ] **8. Phiếu Tạo bè và mã bè**
  - Lỗi:
    - E10, E49 và BR-27 ghi mỗi bè có "đúng một" phiếu Tạo bè; FR-UC76 ghi "tối đa một".
    - E10 Raft không khai mã bè là khóa duy nhất trong vùng, trong khi UC18 yêu cầu "mã duy nhất trong vùng".
  - Sửa: thống nhất "đúng một"; thêm khóa thay thế (zone_id, mã bè) cho E10.

---

## B. Quyết định mới chưa được cập nhật hết

- [ ] **9. Kênh SMS (QĐ-26) còn thiếu ở nhiều chỗ**
  - Lỗi:
    - BF-09 bước 1: "gửi chứng từ … qua email hoặc Zalo OA".
    - Bảng 3.4-2, chuyển Đang gửi → Đã gửi: "Phản hồi thành công của Zalo OA hoặc dịch vụ email".
    - API-01 (Caller và UC liên quan): thiếu UC02, UC05 (xác minh/đổi số điện thoại) và UC48.
    - IV.1 dòng 1 (Dịch vụ SMS): phần mô tả nhắc UC02, UC05, UC48 nhưng cột "UC liên quan" không có.
    - API-08: cột "Hệ thống ngoài" không có SMS, cột Caller lại có.
    - JOB-02 bước 2: chỉ gọi API-03/API-04.
    - UC32 (Dữ liệu nhập) và SCR-20: "Kênh gửi QR (Zalo OA / email)".
    - UC71: Secondary Actors thiếu Dịch vụ SMS.
    - UC73 và SCR-57: tab vẫn mang tên cũ "Xác minh điện thoại"; thiếu tab Google Maps, Dịch vụ lưu trữ đám mây, Dịch vụ OCR.
  - Sửa: thêm SMS vào tất cả các chỗ trên; đổi tên tab thành "Dịch vụ SMS".

- [ ] **10. UC05 trong bảng I.4.2**
  - Lỗi: Description ghi "…để hồ sơ luôn đúng mà không đổi định danh đã xác minh", trái UC05 hiện tại (được đổi email và số điện thoại sau khi xác minh).
  - Sửa: dùng Description như trong đặc tả UC05.

- [ ] **11. SCR-09, trường "Tên hiển thị, điện thoại, tên đăng nhập"**
  - Lỗi: ghi "điện thoại không cần xác minh OTP" – ý cũ của QĐ-16, đã bị QĐ-21 thay.
  - Sửa: "chủ tài khoản xác minh số bằng mã SMS ở lần đăng nhập đầu (UC02 nhánh 3a, BR-34)".

- [ ] **12. API-05 (III.14.5)**
  - Lỗi: "Dữ liệu chính … vị trí thiết bị khi chấm công" và "căn cứ chấm công" – QĐ-28 đã bỏ Google Maps khỏi UC57.
  - Sửa: xóa phần chấm công.

- [ ] **13. UC72 viết như thể nhiều HTX lần lượt đăng ký vào nền tảng**
  - Lỗi: OMTS chỉ phục vụ HTX Thủy sản Trung Nam, nhưng các chỗ sau vẫn viết theo kiểu nhiều HTX:
    - UC72 Trigger: "Một HTX đăng ký sử dụng OMTS và đã nộp giấy tờ xác minh".
    - BF-01, Điểm bắt đầu: "Quản trị hệ thống đã xác minh HTX đăng ký dùng OMTS".
    - UC72 bước 2: "kiểm trùng HTX".
    - Phác thảo UC72/SCR-56: "không chọn HTX có sẵn nếu đây là HTX đầu tiên".
    - FR-UC72: "Admin không phải chọn một HTX chưa được tạo".
  - Sửa: coi UC72 là khởi tạo một lần khi triển khai cho HTX Thủy sản Trung Nam (Trigger: "Triển khai OMTS cho HTX Thủy sản Trung Nam"); bỏ bước kiểm trùng HTX; nhánh 2a đổi thành "đã có Chủ HTX – thay Chủ HTX phải có biên bản".

---

## C. Mô hình dữ liệu không có chỗ chứa điều UC mô tả

- [ ] **14. Đồng bộ cổng truy xuất quốc gia**
  - Lỗi: E25 ghi "Đồng bộ cổng truy xuất quốc gia không thuộc phạm vi cam kết nên không có bảng theo dõi riêng". Nhưng:
    - UC41 bước 4 "lưu phản hồi, thời điểm, mã ngoài"; Postcondition "Trạng thái đồng bộ kiểm tra được".
    - SCR-25 là "Hàng đợi đồng bộ", có trạng thái gửi/nhận/lỗi và nút gửi lại.
    - JOB-04 "lấy hồ sơ từ hàng đợi"; API-10 "cập nhật kết quả đồng bộ".
  - Sửa: thêm lại entity theo dõi lần đồng bộ, hoặc ghi rõ dữ liệu này đặc tả ở SDD và sửa câu ở E25.

- [ ] **15. Lịch sử in nhãn QR**
  - Lỗi: UC32 bước 5, nhánh 5a, 5b và SCR-20 có "lưu lịch sử in", "hủy lần in lỗi", "ghi lần in lại" – entity TraceLabelIssue đã bỏ (Change Log 30/09), không entity nào chứa.
  - Sửa: thêm entity, hoặc ghi lịch sử in vào AuditEvent và nói rõ.

- [ ] **16. "Phiên bản" ở những chỗ không có entity phiên bản**
  - Lỗi:
    - UC30 nhánh 1a ("lưu kế hoạch mới") và SCR-19 ("Có thể lưu nhiều phiên bản kế hoạch"), process 2 "sửa phiên bản".
    - UC48 nhánh 1a: "lưu phiên bản điều khoản mới"; SCR-32 "[Lịch sử] Phiên bản điều khoản".
    - UC60 bước 5, nhánh 1a và Bảng 3.4-2 (Đã duyệt → Nháp): "phiên bản đã duyệt được giữ".
    - UC26 nhánh 1a: "lưu phiên bản" ngưỡng, có "ngày hiệu lực"; SCR-18 cũng có "ngày hiệu lực".
    - Trong khi đó: E48 ghi chỉ có ba entity có phiên bản (RaftLayoutVersion, PayRuleVersion, TracePublicationVersion); OrderRevision và WaterThresholdVersion đã bỏ (01/10); E07 chỉ có "ngưỡng hiện hành"; QĐ-20 ghi "không lưu phiên bản cũ, chỉ ghi nhật ký kiểm toán".
  - Sửa: đổi các chỗ trên thành "ghi nhật ký kiểm toán (trước – sau)", bỏ "ngày hiệu lực" của ngưỡng; hoặc thêm entity phiên bản tương ứng.

- [ ] **17. Đơn một hay nhiều sản phẩm**
  - Lỗi: E23 SalesOrder chỉ có một `product_id`, nhưng E21 ("Mỗi dòng đơn của thương lái…"), UC43 nhánh 2b ("không gửi được dòng đó"), process UC43 ("nhập dòng nhu cầu"), QĐ-25 ("mỗi dòng yêu cầu mua"), UC51 và SCR-35 ("biên nhận/dòng") đều nói đến "dòng đơn".
  - Sửa: chốt một sản phẩm cho mỗi đơn và bỏ chữ "dòng"; hoặc thêm entity dòng đơn.

- [ ] **18. E40 WorkAssignment không gắn người**
  - Lỗi: thuộc tính "người/tổ được giao" chỉ là chữ, không có `employee_id`/`worker_id`, nên UC62 không lọc được "việc được giao của tôi" và UC56 bước 3 không kiểm được "trùng người – ngày". "Tổ đội" (UC55 nhánh 1a, UC56) cũng không có entity.
  - Sửa: thêm `employee_id`, `worker_id` (tùy chọn) vào E40; quyết định có cần entity tổ đội hay không.

- [ ] **19. Thiếu thuộc tính so với UC**
  - Lỗi:
    - UC20/SCR-13: giống có mã, mô tả, hình; sản phẩm có mã, giống liên quan, mô tả → E13 chỉ có tên/loại, E21 không có mã và giống liên quan.
    - UC22/SCR-14: "giống cung ứng", "nhà cung cấp gợi ý theo giống" → E14 không có quan hệ với giống (UC23 bước 2 cũng dựa vào gợi ý này).
    - UC31/SCR-19: "chuyến tàu đưa lô về cảng", "trạng thái đến cảng" → không entity nào chứa.
    - UC24: "người phụ trách" → E16 không có.
    - UC25: "lượng giống theo đơn vị gốc", "lý do khác giống" (nhánh 3a) → E17 không có.
    - UC42/SCR-26: "địa chỉ giao", "đầu mối nhận" → E22 không có.
  - Sửa: bổ sung thuộc tính vào entity, hoặc bỏ khỏi UC/SCR.

---

## D. Phân quyền

- [ ] **20. Quyền "trong khu" không áp được với dữ liệu không thuộc khu**
  - Lỗi: ma trận quyền cho Quản lý khu Full* (* = trong khu) ở UC22, UC23, UC42, UC55, UC57 và Kế toán Full* ở UC49, UC50, UC53, UC54, UC58, UC59, UC61. Nhưng SeedSupplier, SeedReceiptLot, Customer, CustomerReceipt, Contractor, SeasonalWorker, AttendanceRecord, PayRuleVersion, LaborSettlement không có `zone_id`. Ví dụ AC-01 (một tài khoản là Kế toán chỉ ở Khu C) → không xác định được người này thấy phiếu thu, công nợ nào.
  - Sửa: định nghĩa phạm vi "dữ liệu chung HTX" (chỉ vai trò ở Toàn bộ khu mới thao tác), hoặc gắn khu cho các entity này.

- [ ] **21. UC48 bước 6 vượt quyền**
  - Lỗi: "người thao tác ghi tiền ở UC49" – người thao tác UC48 gồm Quản lý khu, nhưng ma trận quyền cho Quản lý khu là No ở UC49.
  - Sửa: ghi rõ "Chủ HTX hoặc Kế toán ghi tiền ở UC49", hoặc cấp quyền UC49 cho Quản lý khu.

- [ ] **22. Actor của UC52**
  - Lỗi: bảng I.4.2 và Description chỉ ghi Chủ HTX; Primary Actors và ma trận quyền có thêm Quản lý khu (ghi hàng trả thực nhận, QĐ-24).
  - Sửa: Description "Tôi với vai trò là Chủ HTX hoặc Quản lý khu phụ trách đơn…", nêu rõ Quản lý khu chỉ ghi hàng trả thực nhận.

- [ ] **23. Ai được đính chính hồ sơ truy xuất**
  - Lỗi: UC32 nhánh 3b1, BF-04 và JOB-03 ghi "chỉ Chủ HTX sửa hồ sơ"; UC39 Primary Actors có cả Quản lý khu phụ trách đơn; BF-08 ghi "Người phụ trách đơn đính chính".
  - Sửa: chốt một quy tắc (ví dụ: lô bàn giao ngoại tuyến rà không đạt thì chỉ Chủ HTX; còn lại theo UC39) và ghi thống nhất.

- [ ] **24. Ai được mở khóa tài khoản**
  - Lỗi: Bảng 3.4-2 cho Quản trị hệ thống (UC74) chuyển Đã khóa → Hoạt động với mọi tài khoản; nhưng UC74 nhánh 3b không cho xử lý tài khoản do Chủ HTX khóa. Trạng thái ACCOUNT không phân biệt ai đã khóa.
  - Sửa: thêm điều kiện ở Bảng 3.4-2 (Quản trị hệ thống chỉ mở tài khoản do chính mình khóa), và lưu người khóa trên tài khoản hoặc lấy từ AuditEvent.

---

## E. Vòng đời trạng thái

- [ ] **25. Đơn bị kẹt khi bỏ qua UC30**
  - Lỗi: UC30 nhánh 1b "Không lập kế hoạch chi tiết → ghi thu thực tế ở UC31", nhưng Bảng 3.4-2 không có Đã xác nhận → Đã thu; Đang thu hoạch chỉ đi ra từ UC30.
  - Sửa: thêm chuyển Đã xác nhận → Đang thu hoạch tại UC31 (lần thu đầu tiên), hoặc bỏ nhánh 1b.

- [ ] **26. Đơn không có đường kết thúc**
  - Lỗi:
    - Không có chuyển hủy từ Chờ xét hoặc Chờ khách đồng ý khi thương lái rút yêu cầu.
    - UC44 nhánh 5b chặn hủy từ Đang thu hoạch trở đi → thương lái bỏ đơn giữa chừng thì đơn treo mãi.
  - Sửa: thêm chuyển hủy cho các trạng thái trên (có lý do), quy định xử lý phần đã thu khi hủy.

- [ ] **27. TracePublicationVersion thiếu Đạt → Nháp**
  - Lỗi: UC32 nhánh 3a coi "dữ liệu đổi sau rà" là chưa đạt và bước 4 kiểm "dữ liệu chưa đổi sau rà", nhưng không có chuyển Đạt → Nháp.
  - Sửa: thêm chuyển Đạt → Nháp (Hệ thống, khi dữ liệu nguồn đổi sau rà).

- [ ] **28. Trạng thái không có trong mục I.3.4**
  - Lỗi:
    - UC24 nhánh 4a và MSG29: "bè đang bảo dưỡng" – bè chỉ có Đang dùng / Ngừng dùng.
    - UC72 nhánh 4a: "giữ tài khoản ở trạng thái cần xử lý".
    - UC74 và SCR-58: "Tạm dừng", "Khôi phục", "Khởi tạo phục hồi".
    - UC45 và SCR-29: chuỗi "Chờ cân → Đã xác nhận cân → Chờ rà → Chờ công bố QR → Sẵn sàng bàn giao → Đã bàn giao/chốt bán" và "Đã bàn giao – chờ đồng bộ → …", trái BR-29 (mọi trạng thái phải nằm trong danh mục Status).
  - Sửa: thay bằng trạng thái có trong 3.4 (ví dụ UC24 4a: "Bè Ngừng dùng hoặc còn chu kỳ chưa đóng"), hoặc ghi rõ đây là tiến trình hiển thị suy ra, không phải trạng thái lưu.

- [ ] **29. Bước chuyển trạng thái ghi sai hoặc thiếu trong Normal Flow**
  - Lỗi:
    - UC27 bước 3b4: "chuyển bè sang trạng thái có thể mở chu kỳ mới" – đúng ra là chu kỳ chuyển Đang mở → Đã đóng (bè không có trạng thái này).
    - Normal Flow không ghi bước chuyển trạng thái: UC09 (Sơ bộ → Đã hoàn thiện), UC30 (đơn Đã xác nhận → Đang thu hoạch), UC31 (lần thu Nháp → Đã xác nhận; đơn Đang thu hoạch → Đã thu – không có bước xác nhận cuối ngày), UC48 (Đã bàn giao → Đã chốt bán).
  - Sửa: thêm bước chuyển trạng thái vào Normal Flow và Postconditions.

- [ ] **30. Bước duyệt không có trạng thái chờ duyệt**
  - Lỗi: UC53 bước 3 và UC58 bước 4 có "Chủ HTX duyệt", nhưng SaleAdjustment và PayRuleVersion không có vòng đời → khi Kế toán nhập, bản ghi nằm ở đâu trước khi duyệt?
  - Sửa: thêm trạng thái (Nháp / Đã duyệt), hoặc quy định Kế toán chỉ nhập khi đã có duyệt ngoài hệ thống và bỏ bước duyệt.

---

## F. Luồng UC mâu thuẫn

- [ ] **31. Điều kiện ngừng dùng vùng nuôi**
  - Lỗi: E07 và mục 3.4.3 chặn khi "còn bè Đang dùng trong vùng"; UC15 nhánh 2b và ghi chú UC15 chặn khi "còn chu kỳ nuôi chưa đóng".
  - Sửa: chọn một điều kiện và ghi thống nhất.

- [ ] **32. Trả công trọn gói**
  - Lỗi: UC57 nhánh 3a "Việc được trả trọn gói theo UC56", nhưng V.3 "Ngoài phạm vi" có "trả công theo khoán việc".
  - Sửa: bỏ nhánh 3a, hoặc đưa khoán việc vào phạm vi (UC58 cần thêm cách tính).

- [ ] **33. UC23 nhánh 1a**
  - Lỗi: "Sửa lô giống đã được dùng ở UC25 → sửa qua UC39", nhưng UC39/E30 gắn `lot_id` của lô thu hoạch và yêu cầu "Quản lý khu được giao phụ trách đơn"; lô giống có thể chưa thuộc lô thu hoạch nào.
  - Sửa: mở rộng UC39/E30 cho bản ghi nguồn chưa gắn lô, hoặc quy định cách sửa lô giống riêng.

- [ ] **34. UC44 bước 4**
  - Lỗi: gửi thương lái "kg ước tính, giá tham khảo, nguồn giống, khu và bè" khi chưa có kế hoạch thu (UC30 chạy sau UC44), và tài liệu khẳng định không có bảng giá tham khảo (UC20, BR-12, V.3).
  - Sửa: chỉ gửi thông tin có ở thời điểm xét đơn (sản phẩm, lượng xác nhận, khu phụ trách, thời gian dự kiến), hoặc chuyển bước gửi sang sau UC30.

- [ ] **35. UC45 «include» UC32 và UC48 ghi "Bắt buộc: luôn gọi"**
  - Lỗi: nhánh 5a (cảng mất mạng) thì UC32 chạy sau khi đồng bộ; nhánh 1a (bán lại hàng trả) dùng QR cũ đã công bố.
  - Sửa: ghi điều kiện cho include, hoặc đổi UC32 thành «extend» với điều kiện "có mạng và lô chưa có bản công bố hiện hành".

- [ ] **36. Mật khẩu tạm và khóa tạm**
  - Lỗi:
    - Bảng 3.4-3 ghi mật khẩu tạm (UC11 nhánh 1d) buộc đổi ở lần đăng nhập đầu và hết hạn sau 24 giờ, nhưng UC02 và UC04 không có nhánh này.
    - MSG12 ("Thông tin đăng nhập không đúng") được dùng cho mật khẩu tạm hết hạn; MSG13 ("…liên hệ kênh hỗ trợ") được dùng cho khóa tạm 15 phút → thông báo sai ngữ nghĩa.
  - Sửa: thêm nhánh "đăng nhập bằng mật khẩu tạm → buộc đổi (UC04)" và "mật khẩu tạm quá hạn" vào UC02; thêm MSG riêng cho mật khẩu tạm hết hạn và khóa tạm 15 phút.

- [ ] **37. Quy tắc mật khẩu**
  - Lỗi:
    - UC01, SCR-01, SCR-02 ghi "tuân quy tắc mật khẩu cấu hình"; UC03, UC04, UC11 và QĐ-18 ghi "tối thiểu 8 ký tự, có chữ và số".
    - UC11 tạo tài khoản bằng mật khẩu Chủ HTX đặt mà không buộc đổi, trong khi nhánh đặt lại 1d dùng mật khẩu tạm buộc đổi.
  - Sửa: thống nhất "tối thiểu 8 ký tự, có chữ và số"; cân nhắc dùng mật khẩu tạm buộc đổi cả khi tạo tài khoản.

- [ ] **38. Tên trạng thái và đơn vị chấm công không khớp mô hình**
  - Lỗi:
    - UC70 bước 5 ("đã gửi, đang chờ, thất bại") và FR-UC71 ("chờ, đã nộp, đã giao hoặc lỗi") khác danh mục MESSAGE_DELIVERY (Đang gửi / Đã gửi / Thất bại).
    - UC57, FR-UC57, SCR-41 có "ngày/ca", "Giờ hoặc công thực tế", nhưng E41 chỉ có "cả ngày/nửa ngày" và tài liệu ghi không tính giờ làm thêm.
  - Sửa: dùng đúng tên trạng thái trong 3.4; bỏ "ca", "giờ".

---

## G. Thuật ngữ và biên tập

- [ ] **39. Tên actor không thống nhất**
  - Lỗi: "Owner" (119 lần), "Manager" (8 lần), "Admin" (12 lần) dùng lẫn với tên actor chính thức.
  - Sửa: thay bằng Chủ HTX / Quản lý khu / Quản trị hệ thống (trừ chỗ định nghĩa "Chủ HTX (Owner)").

- [ ] **40. Tên tài liệu thiết kế**
  - Lỗi: "SDS" (15 lần) và "SDD" (45 lần) dùng cho cùng một tài liệu.
  - Sửa: chọn một tên.

- [ ] **41. Bảng Definition and Acronyms còn thiếu**
  - Lỗi: thiếu HTX, BR, FR, NFR, MSG, SCR, BF, API, JOB, OTP, VietQR, SDD/SDS, QĐ, OPEN, CX, AC, MoSCoW, ERD, DFD; "chu kỳ nuôi" viết thường không thống nhất.
  - Sửa: bổ sung.

- [ ] **42. Dòng thừa, tên process ghép lỗi, dấu câu**
  - Lỗi:
    - Dòng thừa "3. Khách hàng, đơn hàng và bán hàng" cuối UC41 và "4. Thanh toán và xử lý sau bán" cuối UC48.
    - Tên process ghép lỗi: "Liên kết Quản lý hồ sơ khách hàng…" (UC42), "Gửi Tạo yêu cầu mua hàng…" (UC43), "Xác nhận Xét yêu cầu mua hàng…" (UC44), "Đối chiếu Xem biên nhận…" (UC47), "Phân bổ Ghi nhận tiền…" (UC49), "Kiểm tra Đối soát…" (UC50), "Nộp Gửi yêu cầu…" (UC51), "Xác nhận Áp dụng giảm giá…" và "xác định lượng giữ" (UC53), "Xác nhận Ghi nhận hoàn tiền…" (UC54), "UC30 Lập kế hoạch thu hoạch — Điều chỉnh…" (UC30), "UC37 Truy xuôi lô tới khách — Truy xuôi lô…" (UC37).
    - Dấu ".;" ở E23 ("theo phạm vi hiện hành.;") và E29 ("lịch sử trả hàng.;").
    - UC liên kết bị lặp: UC40 ("UC32" hai lần), UC63 ("UC45" hai lần), SCR-16, SCR-19, SCR-21.
  - Sửa: xóa dòng thừa, sửa tên process, bỏ dòng lặp.

- [ ] **43. Loại nhập sai ở mục III**
  - Lỗi:
    - SCR-07: "Email hoặc website – Chọn từ danh sách" (phải là văn bản).
    - SCR-13: "Giống hàu / Sản phẩm – Bắt buộc: Không" nhưng mô tả "mã và tên bắt buộc".
    - SCR-15: "Mã lô nhà cung cấp – Chọn từ danh sách".
    - SCR-16: "Chu kỳ – Ngày/giờ".
    - SCR-21: "Mã đơn/lô/QR hoặc mốc thời gian báo cáo – Ngày/giờ".
    - SCR-60: "Quy cách – Chọn từ danh sách" (UC76 cho nhập tự do).
    - SCR-19: câu ghi chú "Không nhập xác nhận kg của người mua trong UC31…" và "Chứng cứ/chuyến tàu…" bị biến thành trường kiểu "Số".
    - SCR-23: "Giá trị mới – Số" (giá trị sửa có thể là nguồn bè/lối, không chỉ số cân).
  - Sửa: rà lại cột "Loại nhập" của toàn bộ bảng trường.

- [ ] **44. Nội dung màn hình sai**
  - Lỗi: SCR-02 (Xác minh) chép lại toàn bộ form của SCR-01 (Đăng ký) và SCR-04 (Khôi phục); SCR-03 (Đăng nhập) ghi "Màn hình này cho phép người dùng đã đăng nhập…".
  - Sửa: SCR-02 chỉ giữ phần nhập mã; SCR-03 ghi "người dùng có tài khoản (chưa đăng nhập)".

- [ ] **45. Văn phong FR không đồng nhất**
  - Lỗi: FR-UC09, 10, 11, 12, 15, 20, 26, 32 viết theo kiểu user story "Tôi với vai trò…"; các FR còn lại viết theo kiểu hành vi hệ thống.
  - Sửa: viết lại các FR trên theo kiểu hành vi (điều kiện – hành động – kết quả).

- [ ] **46. Phân loại nhánh và Preconditions**
  - Lỗi:
    - Nằm trong Exception Flows nhưng kết thúc thành công hoặc tiếp tục luồng chính: UC01 4b, UC02 3d, UC05 3g, UC31 5a ("Use Case kết thúc thành công").
    - Preconditions mâu thuẫn với EF: UC02 ("Tài khoản … đang được phép truy cập" nhưng 2b xử lý tài khoản bị khóa); UC40 ("QR thuộc lô đã được công bố" nhưng 2a xử lý QR chưa công bố); UC72 ("đã được xác minh" nhưng 1a xử lý xác minh không đạt).
    - UC01: bước 4 ghép hồ sơ khách diễn ra trước bước 5 tạo tài khoản.
  - Sửa: chuyển các nhánh thành công sang Alternative Flows; nới Preconditions; đổi thứ tự bước 4 và 5 ở UC01.

- [ ] **47. Bố cục bảng**
  - Lỗi:
    - Ma trận quyền theo UC: UC76, UC77 đặt cuối bảng dưới tiêu đề "3. Vùng nuôi, bè và hồ sơ tuân thủ" lặp lại.
    - Mục 3.3: BR-25 có cột "Entity liên quan" là "—".
    - Bảng V.1: cột "Enforced By" chứa tên entity (và "UC18 (chặn…)") thay vì cơ chế thực thi.
    - Bảng "Giới hạn và quy tắc trường chờ xác nhận" (V.3) chỉ có CX-01, mà CX-01 đã chốt.
  - Sửa: chuyển UC76, UC77 vào nhóm 3; điền entity cho BR-25 (RaftLayoutVersion, Lane, CultivationCycle); đổi tên cột thành "Entity liên quan" hoặc ghi cơ chế thực thi; bỏ bảng CX nếu không còn mục mở.
