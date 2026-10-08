# SRS v5.8 (bản đã sửa 08/10/2026): danh sách cần sửa tiếp

## Nguồn và phạm vi
- Tổng hợp từ lần so sánh với V4_1 và các mục còn tồn của vòng 2–3. Mọi mục đã được đối chiếu lại với văn bản.
- File áp dụng: `Report_3_SRS_v5.8_da_sua_Clean.docx`, hoặc bản TrackChanges sau khi chấp nhận hết.
- Không xét sơ đồ, trừ mục D.
- **Lưu ý:** lần so sánh chỉ chấm mẫu 11/66 UC và gặp khoảng 2 lỗi nhỏ mỗi UC. Các UC chưa chấm có thể còn lỗi cùng kiểu: nhánh "tiếp tục" sau khi bị chặn, Postcondition thiếu kết quả của nhánh, MSG xác nhận gắn sai bước. Nên rà thêm một lượt theo checklist ở mục F.

Mức độ: 🔴 Cao (sai nghiệp vụ hoặc không kiểm thử được) · 🟠 Trung bình · 🟡 Thấp.

---

## A. Lỗi luồng nghiệp vụ (nên sửa trước)

| # | Mức | Vị trí | Hiện trạng | Cách sửa |
|---|---|---|---|---|
| A1 | 🔴 | UC45, Normal Flow bước 4 | "Hệ thống gửi số cân, giá và **số tiền** cho thương lái qua Zalo OA…" (BR-26), nhưng số tiền cuối chỉ có sau UC48 bước 2–3 (làm tròn lên nghìn đồng, người thao tác xác nhận). BF-04 cũng ghi gửi số tiền sau UC48. | Bước 4 UC45 chỉ gửi **số cân và giá đã thống nhất**. Số tiền cuối gửi ở UC48 bước 5 (đã có). Sửa SCR-29 và FR-UC45 nếu có nhắc "số tiền". |
| A2 | 🔴 | UC48, nhánh 4a "Cảng mất mạng" | 4a2 xong thì "Use Case tiếp tục bước 5". Nhưng bước 5 tạo VietQR rồi gửi qua UC70, việc này cần mạng. UC45 5a3 lại ghi gửi QR khi có mạng. | 4a3: "Khi có mạng trở lại, hệ thống thực hiện bước 5 (tạo VietQR, gửi qua UC70)." Đổi điểm quay về thành "Use Case kết thúc thành công; bước 5 chạy sau đồng bộ". |
| A3 | 🔴 | UC18 Quản lý bè | Normal Flow chỉ là **Thêm bè**. AF có Xem (1a), Bè chưa có chu kỳ (1b), Ngừng dùng (1c), nhưng **không có nhánh sửa bè**. EF 2a "Đổi mốc hoặc thứ tự lối khi bè còn chu kỳ chưa đóng" rẽ từ bước 2 của luồng thêm bè. Bè mới thì chưa có chu kỳ, nên nhánh này không bao giờ xảy ra. | Thêm AF **1d. Sửa bè**: 1d1 chọn bè, sửa vị trí, kích thước, ghi chú, ảnh, sơ đồ lối; 1d2 kiểm như bước 3; 1d3 lưu và ghi audit; "tiếp tục bước 5". Chuyển EF 2a thành **1d-a** (rẽ từ 1d1). Thêm nút Sửa ở SCR-12 nếu chưa có. |
| A4 | 🔴 | UC31, bước 6 "Thu xong" | "Hệ thống kiểm mọi lần thu của đơn đã xác nhận và chuyển đơn Đang thu hoạch → Đã thu", nhưng EF chỉ có 2b. Không có nhánh khi kiểm **không đạt** (còn lần thu Nháp). | Thêm EF **6a. Còn lần thu Nháp khi chọn Thu xong** → 6a1. Hệ thống chặn, liệt kê các lần thu Nháp (MSG mới hoặc MSG61) → "Use Case tiếp tục bước 6". |
| A5 | 🔴 | UC61, bước 4 | "Hệ thống kiểm tra tiền chi không vượt số còn lại", nhưng EF chỉ có 4a (trùng). Không có nhánh chi vượt, dù MSG45 "{field_name} vượt quá mức cho phép" đã có sẵn. | Thêm EF **4b. Số tiền vượt số còn phải trả** → 4b1. Hệ thống chặn, hiện số còn lại (MSG45) → "Use Case tiếp tục bước 3". Thêm UC61 vào cột Ngữ cảnh của MSG45. |
| A6 | 🟠 | UC45, Preconditions | Chỉ đòi "Đơn đã xác nhận ở UC44 và có lô nguồn thực thu ở UC31". Bảng 3.4-2 chỉ cho chuyển **Đã thu → Đã bàn giao**. | Sửa thành "Đơn ở trạng thái **Đã thu** (UC31 đã chọn Thu xong), hoặc phần hàng trả được phép bán lại ở UC52". |
| A7 | 🟠 | UC45, Postconditions | Không nêu trạng thái đơn sau bàn giao. | Thêm "• Đơn chuyển Đã thu → Đã bàn giao (bàn giao ngoại tuyến: chuyển trên thiết bị, chờ đồng bộ)". |
| A8 | 🟠 | UC45, nhánh 5a "Cảng mất mạng" | Nhánh đặt ở bước 5, nhưng bước 4 (gửi qua Zalo OA/SMS) đã cần mạng. | Sau khi sửa A1: chuyển điểm rẽ lên **4a**, hoặc ghi rõ trong 5a1 "tin ở bước 4 được gửi khi có mạng". |
| A9 | 🟠 | UC32, nhánh 4b "Không đủ quyền công bố" | "4b1. Hệ thống chặn công bố. (MSG02) ⏎ Use Case **tiếp tục bước 2**." Đã bị chặn quyền mà vẫn tiếp tục luồng. | Đổi thành "Use Case dừng lại". |
| A10 | 🟠 | UC49 Ghi nhận thanh toán | Description và Postconditions nói "phân bổ vào giao dịch", nhưng Normal Flow (bước 1–4) không có bước phân bổ. | Thêm bước: "Người thao tác phân bổ số tiền vào một hoặc nhiều giao dịch còn nợ (mặc định cũ nhất trước); hệ thống kiểm tổng phân bổ ≤ số tiền thu." Thêm EF khi phân bổ vượt (MSG45). |
| A11 | 🟠 | UC49, Secondary Actors | Có "Zalo OA" nhưng không bước nào dùng. Biên nhận gửi qua UC70 (ở UC48). | Bỏ Zalo OA khỏi Secondary Actors, hoặc thêm bước "gửi biên nhận qua UC70". |
| A12 | 🟠 | E34 CustomerReceipt | Thuộc tính: "receipt_id, customer_id, số tiền, ngày, phương thức, chứng cứ". Thiếu **mã tham chiếu** (UC49 bước 2 nhập; 3a kiểm trùng trên trường này) và thiếu phần **phân bổ**. | Thêm `reference_no` (duy nhất theo phương thức). Thêm entity hoặc thuộc tính phân bổ (receipt_id, sale_id, số tiền phân bổ), hoặc ghi rõ phân bổ lưu ở đâu. |
| A13 | 🟠 | E02 Account | UC02 2c/2d và Bảng 3.4-3 đếm "after(24 giờ)" từ lúc cấp mật khẩu tạm. E02 không có thuộc tính này. | Thêm `temp_password_issued_at`, `must_change_password` (UC11 1d, UC72, UC74). |
| A14 | 🟡 | UC24, Preconditions | "Bè (UC18) và **giống (UC20) đã có**", nhưng dữ liệu nhập ghi "giống dự kiến: tùy chọn" (F-33). | Sửa thành "• Bè (UC18) đã có." Bỏ "giống (UC20)" hoặc ghi "(nếu chọn giống dự kiến)". |

## B. Lỗi nhỏ trong UC (từ mẫu chấm)

| # | Mức | Vị trí | Hiện trạng | Cách sửa |
|---|---|---|---|---|
| B1 | 🟡 | UC01, EF 3a | "3a1. … cho thử lại trong giới hạn. (MSG16) ⏎ Use Case dừng lại." Vừa cho thử lại vừa dừng. | Tách: còn lượt thì "Use Case tiếp tục bước 3"; hết lượt thì "dừng lại". |
| B2 | 🟡 | UC01, Postconditions | AF 5a1 tạo hồ sơ khách gắn tài khoản, nhưng Postconditions không nêu. | Thêm "• Có hồ sơ khách gắn tài khoản (hoặc chờ Chủ HTX ghép ở UC42)". |
| B3 | 🟡 | UC02, EF 3b, 3c, 3e | Thuộc phần mở rộng 3a (bước 3a2–3a3) nhưng đánh số như nhánh của bước 3, và quay về "bước 3". | Đổi thành 3a2a, 3a2b…, quay về "bước 3a2". Hoặc ghi rõ "rẽ từ bước 3a2". |
| B4 | 🟡 | UC11, Postconditions | Chỉ nêu tài khoản và cặp khu – vai trò. Bỏ sót kết quả của 1b (khóa), 1c (mở khóa), 1d (mật khẩu tạm 24 giờ), dù cả ba nhánh đều "kết thúc thành công". | Thêm 3 gạch đầu dòng tương ứng. |
| B5 | 🟡 | UC11 1b2, UC32 1a2 | MSG09 là hộp xác nhận ("Bạn có chắc chắn muốn {action}?") nhưng gắn ở bước kết quả. | Chuyển (MSG09) về bước xác nhận: UC11 **1b1**, UC32 **1a1**. |
| B6 | 🟡 | UC11, ô "Điểm cần xác nhận / lưu ý" | Ghi chú lịch sử tự mâu thuẫn: "06/10: … không bắt buộc xác minh số … 07/10 (thay ý … nêu trên)". | Chỉ giữ quy định hiện hành. Lịch sử đưa về Change Log hoặc V.3.2. |
| B7 | 🟡 | UC31, AF 5a | "Chưa có cân tại cảng khi người dùng muốn bàn giao". Bàn giao thuộc UC45, nằm ngoài phạm vi UC31. | Bỏ nhánh 5a khỏi UC31 (UC45 đã chặn bàn giao khi chưa cân). |
| B8 | 🟡 | UC48, AF 1a | "Use Case tiếp tục bước 1": quay về đúng bước vừa rẽ. | Đổi thành "tiếp tục bước 2". |
| B9 | 🟡 | Hàng "Business Rules" của UC | BR được dẫn trong thân UC nhưng không có ở hàng BR và cột Applies To: BR-09 ở UC30 bước 2; BR-19 ở UC45 Preconditions; BR-31 ở UC11 (dữ liệu nhập) và UC70 (ghi chú). | Thêm vào hàng Business Rules của UC30, UC45, UC11, UC70. Cập nhật Applies To của BR-09 (thêm UC30), BR-19 (UC45), BR-31 (UC11, UC70). |

## C. NFR: làm cho đo được (học từ V4_1)

NFR hiện có 13 mục, không có cột nghiệm thu. NFR-11 "còn mở", NFR-12 "RTO chốt ở SDS", một số số đo ghi "mục tiêu sơ bộ".

**Đề xuất:** thêm cột **"Tiêu chí nghiệm thu"** vào bảng NFR. Bổ sung hoặc sửa các mục sau (số liệu là đề xuất, nhóm chốt):

| Nhóm | Yêu cầu đề xuất | Cách nghiệm thu |
|---|---|---|
| Hiệu năng | p95 đọc danh sách/chi tiết ≤ 2 s; ghi biểu mẫu ≤ 3 s; trang QR công khai ≤ 3 s (không tính upload ảnh, dịch vụ ngoài). | ≥ 1.000 yêu cầu sau warm-up, 50 người dùng đồng thời; báo cáo p95 và tỷ lệ lỗi. |
| Phiên | Hết phiên sau 30 phút không thao tác, tối đa 12 giờ. Đăng xuất thu hồi phiên hiện tại; đổi hoặc đặt lại mật khẩu thu hồi mọi phiên. **Riêng thiết bị đang có bản nháp offline:** cho mở khóa cục bộ để nhập tiếp, đăng nhập lại khi đồng bộ (tránh mâu thuẫn như V4_1). | Thử nhiều thiết bị; dùng lại phiên đã thu hồi; mô phỏng hết phiên khi offline. |
| Chống đoán | Đã có 5 lần sai → tạm khóa 15 phút (UC02 2e). Thêm: tối đa 3 lần gửi mã/15 phút theo đích và mục đích; 5 lần nhập mã sai/mã. | Kịch bản thử sai liên tiếp. |
| Bảo mật | Mật khẩu băm một chiều có salt; mã OTP và mật khẩu tạm không vào log, audit hay QR; HTTPS; không đặt credential trong URL. | Kiểm API, log, audit, export. |
| Sao lưu | RPO ≤ 24 giờ, **RTO ≤ 8 giờ** (chốt luôn, không để SDS). Backup hằng ngày; diễn tập phục hồi mỗi quý. | Phục hồi vào môi trường cô lập, đo thời gian, đối chiếu bản ghi và tệp. |
| Ảnh | JPEG/PNG ≤ 10 MiB/tệp; tối đa 10 ảnh/lần ghi; kiểm MIME thật; lỗi tệp không làm mất bản nháp. | Thử tệp hợp lệ, giả đuôi, quá dung lượng. |
| Offline | Giữ ít nhất 100 bản chờ, mỗi bản 5 ảnh, qua đóng/mở ứng dụng; gửi lại cùng ID không tạo bản ghi lặp. | Tắt mạng, nhập, tắt ứng dụng, bật lại, đồng bộ. |
| Log | Log vận hành ≥ 90 ngày; nhật ký kiểm toán nghiệp vụ không bị xóa theo vòng log. | Kiểm cấu hình lưu trữ. |
| Nền tảng | Nêu rõ: web responsive, màn hình từ 360 px; Chrome/Edge/Safari, 2 phiên bản gần nhất. | Ma trận trình duyệt khi nghiệm thu. |

## D. Mục còn tồn từ vòng 2–3

| # | Mức | Mục | Việc cần làm |
|---|---|---|---|
| D1 | 🟡 | N13 | Sắp lại thứ tự các dòng bảng V.3.2. |
| D2 | 🟡 | F-16 | Mục ERD ghi "9 nhóm": đối chiếu tên nhóm trong sơ đồ, sửa số hoặc liệt kê tên nhóm. |
| D3 | 🟠 | Sơ đồ | Cập nhật theo nội dung đã sửa: STD-ORDER (thêm Đã thu → Đã hủy, Đã xác nhận → Đã thu); STD của SaleAdjustment (Nháp → Chờ duyệt → Đã duyệt/Từ chối); UCD có UC44 5c, UC42 3c; BF-03 và BF-04 nếu có nhánh mới. |
| D4 | 🟡 | MSG01 | Thêm MSG01 vào dòng "Thông báo liên quan" của các SCR có trường bắt buộc mà chưa liệt kê. |
| D5 | 🟡 | Include có điều kiện | Ghi chú UML cho các quan hệ include chỉ chạy khi thỏa điều kiện (ví dụ UC45 → UC32 "nếu lô chưa có bản công bố hiện hành"). |

## E. Trình bày

| # | Mức | Vị trí | Việc cần làm |
|---|---|---|---|
| E1 | 🟡 | Priority của cả 66 UC | Bỏ chữ "(đề xuất)" sau khi nhóm chốt độ ưu tiên. |
| E2 | 🟡 | Khoảng 15 ô ghi chú trong thân UC | Có ngày quyết định ("Đã chốt 06/10/2026: …", "07/10/2026: …"). Chỉ giữ nội dung hiện hành; lịch sử đưa về Change Log hoặc V.3.2. |
| E3 | 🟡 | Bảng trường SCR | 4 tên trường bị cắt "…": "(7) Danh sách bè và lối, mốc bắt đầu/kết thúc phần chiều dài đã…", "Chênh lệch tạm thời giữa mục tiêu và kg ước tính, ghi rõ…", "(4) Phiếu cân và kg thực được thương lái xác nhận trực tiếp tại…", "(1) Điều khoản sửa trước khi thực hiện, hoặc thỏa thuận xử lý…". Ngoài ra 1 câu bị đặt vào cột tên trường: "Không nhập giao dịch hay thay đổi KPI trực tiếp trên màn hình." Đặt tên trường ngắn gọn; chuyển câu dài sang cột mô tả. |
| E4 | 🟡 | UC01 | Tên "Đăng ký tài khoản **khách hàng**" nhưng actor là Thương lái. Thống nhất một thuật ngữ, ví dụ "Đăng ký tài khoản thương lái", hoặc định nghĩa rõ "khách hàng = thương lái" ở Definitions. |
| E5 | 🟡 | Dải mã UC (ví dụ "UC31–41") | Dải trùm cả mã đã bỏ (UC33–35). Liệt kê mã cụ thể, hoặc thêm ghi chú "mã bỏ trống không dùng". |
| E6 | 🟡 | "Nhóm quyết / chốt ở SDS" (27 lần) | Rà từng chỗ. Yêu cầu nghiệp vụ hoặc NFR thì chốt trong SRS. Chỉ để SDS những chi tiết kỹ thuật thật sự (cấu trúc bảng, API endpoint). |

## F. Đề xuất bổ sung (tùy nhóm quyết; V4_1 có, v5.8 chưa có)

1. **Sự cố bè và sửa bè:** ghi sự cố (bão, đứt dây, chìm phao) và việc lắp/sửa. Có thể gộp vào UC76/UC77 (vật tư bè) hoặc thêm UC mới.
2. **Đính chính tiền bằng bút toán đảo:** khoản thu (UC49) hoặc hoàn tiền ghi sai thì tạo bút toán đảo + bút toán đúng, không sửa đè. Hiện tại BR "giá trị bán gốc không đổi" đã có, nhưng chưa có luồng đảo khoản thu.
3. **Chốt kỳ đối soát công nợ có snapshot:** khóa số dư theo kỳ, mọi điều chỉnh sau đó ghi vào kỳ đang mở.
4. **Định nghĩa chỉ tiêu báo cáo:** công thức, nguồn dữ liệu, mốc ngày cho từng chỉ tiêu ở UC63–UC68, đặt ở III (như III.12.2 của V4_1).
5. **Một đơn giao nhiều đợt:** nếu thực tế HTX có giao làm nhiều chuyến cho một đơn.

### Checklist rà các UC còn lại (dùng cho lượt rà tiếp)
- [ ] Nhánh bị chặn (quyền, dữ liệu sai, trùng) kết thúc bằng "dừng lại" hoặc quay về đúng bước nhập. Không được "tiếp tục" bước sau.
- [ ] Mỗi bước "Hệ thống kiểm …" có ít nhất một EF khi kiểm không đạt, kèm MSG.
- [ ] Postconditions nêu kết quả của mọi nhánh "kết thúc thành công", kể cả chuyển trạng thái.
- [ ] MSG loại "Xác nhận" gắn ở bước người dùng xác nhận, không gắn ở bước kết quả.
- [ ] Preconditions nêu đúng trạng thái theo Bảng 3.4-2.
- [ ] Bước gọi dịch vụ ngoài (Zalo/SMS/email/VietQR/cổng) không nằm trên đường offline.
- [ ] BR, MSG, entity nhắc trong thân UC có trong hàng Business Rules và cột Applies To/Ngữ cảnh. Thuộc tính dùng trong UC có trong entity.
