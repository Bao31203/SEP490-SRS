# So sánh SRS V4_1 và SRS v5.8 (đã sửa 08/10/2026)

Không chấm sơ đồ. OMTS chỉ phục vụ HTX Thủy sản Trung Nam.

## 1. Kết luận

**v5.8 (đã sửa) tốt hơn và ít lỗi hơn rõ rệt.** V4_1 có điểm mạnh riêng: NFR đo được, xử lý offline và chứng từ đảo. Nhưng tài liệu còn dở dang:
- mục III gần như trống;
- nhiều nghiệp vụ còn TBD;
- số liệu tự mâu thuẫn;
- còn dấu vết nhiều HTX;
- 2/5 comment của giảng viên chưa xử lý.

| Tiêu chí | V4_1 | v5.8 đã sửa | Bản hơn |
|---|---|---|---|
| Lỗi tìm được khi rà toàn bộ | ~70 lỗi riêng biệt (≈15 Cao) | Đã qua 3 vòng rà; còn ~6 lỗi luồng nhỏ + các mục đã biết (N13, F-16, sơ đồ) | v5.8 |
| Mục III (màn hình) | 75 SCR: 42 SCR ghi "chưa được đặc tả", 33 SCR chỉ có 1 dòng mô tả; không SCR nào có bảng trường | 61 SCR đều có bảng trường, loại nhập, thông báo liên quan | v5.8 |
| Ghi chú nháp | TBD 61, "chưa đặc tả" 81, mã PA 74–97 | TBD 0, "chưa đặc tả" 0, PA 0 | v5.8 |
| Số liệu tổng | Ghi lúc 35, lúc 48, lúc 69 UC; ghi "tám package" trong khi có 12 | Khớp (66 UC, 52 entity, 61 SCR, 54 chuyển trạng thái) | v5.8 |
| Phạm vi một HTX | Còn "nhiều tenant", "thương lái–nhiều HTX", "trong mỗi HTX"; không có tên Trung Nam | Đúng một HTX | v5.8 |
| Thuật ngữ | Owner 274 lần, Chủ HTX 141 lần (comment C2 chưa sửa) | Owner 4 lần | v5.8 |
| Vòng đời trạng thái | Có ngõ cụt: hủy đơn, mất trắng chu kỳ, trả hàng, lô không bàn giao | Có danh mục trạng thái và bảng chuyển trạng thái có điều kiện | v5.8 |
| Nghiệp vụ còn TBD | LABOR-5, LABOR-6 TBD; LABOR-8 không có nguồn dữ liệu; payOS chỉ khai tên | Đủ: lương, khoán, trả hàng/bán lại, VietQR, Zalo/SMS | v5.8 |
| NFR | 19 NFR, đều có tiêu chí nghiệm thu đo được (p95, RPO/RTO, phiên, ảnh) | 13 NFR, nhiều chỗ chưa có số đo | **V4_1** |
| Luồng UC từng ca | Chặt, có offline/xung đột, chống trùng | Chặt, còn vài lỗi nhỏ | Ngang nhau |
| Vị trí theo template | FR nằm ở V.3; JOB/API chen giữa các package mục III | Đúng template | v5.8 |

**Chấm mẫu công bằng** (người chấm không biết file nào là bản nào; 10 chức năng có ở cả hai bản; cùng một checklist):
- V4_1: 21 lỗi, trong đó 6 nặng.
- v5.8: 22 lỗi, trong đó 4 nặng.

Hai bản ngang nhau ở mức từng UC. Khoảng cách nằm ở cấp toàn tài liệu: độ phủ, tính nhất quán, mục III, ghi chú nháp.

## 2. Lỗi nặng nhất của V4_1

1. **Mục III trống.** Không SCR nào có trường, nút hay quy tắc hiển thị.
2. **Không có UC hủy hoặc sửa đơn**, dù Order có trạng thái Cancelled (dòng 360, 733).
3. **Ngõ cụt vòng đời:**
   - Chu kỳ nuôi mất trắng không đóng được; "cơ chế mở lại chưa được xác định" (dòng 705).
   - Lô đã thu mà khách không nhận thì không có lối ra.
   - Trả hàng được chấp thuận thì treo ở Pending mãi.
4. **Không sửa được giao dịch bán đã chốt sai.** Chỉ đảo được Payment, Adjustment và Refund.
5. **Owner đầu tiên không có mật khẩu ban đầu**, và kênh khôi phục chưa xác minh: "còn phải chọn theo cách triển khai" (dòng 1951).
6. **LABOR-5, LABOR-6 là TBD; LABOR-8 không có nguồn dữ liệu**, nhưng vẫn được tính vào 69 UC.
7. **Không có danh mục Permission**, nên các ô "Restricted" của ma trận quyền không kiểm thử được.
8. **Hạn phiên 30 phút** mâu thuẫn với nhập liệu offline ngoài biển (dòng 682, NFR-15).
9. **payOS (comment C1) chỉ khai tên actor/API**, không có UC, dữ liệu hay luồng.
10. **Package SALE (12 UC) không dùng mã MSG nào.** 49 MSG khác có Context mẫu "Kết quả thao tác … trong nhóm X".

Tình trạng comment của giảng viên:
- C4: đã xử lý.
- C0, C3: xử lý một phần.
- C1, C2: chưa xử lý.

## 3. v5.8 còn cần sửa (phát hiện thêm khi so sánh)

- **UC45 bước 4:** gửi "số tiền" cho thương lái trước khi UC48 chốt giá trị cuối. Nên ghi là gửi số cân và giá tạm, số tiền gửi sau khi chốt.
- **UC48 nhánh 4a** (cảng mất mạng): sau khi đồng bộ, câu "kết quả rà UC32" cần nói rõ thứ tự với bước cần mạng.
- **UC18:** chưa có luồng sửa thông tin bè.
- **UC31:** chưa có nhánh lỗi khi chọn "Thu xong" mà còn lần thu Nháp.
- **UC61:** chưa có nhánh lỗi khi chi vượt số còn lại.
- **UC32 4b1:** bị chặn quyền mà vẫn "tiếp tục bước 2".
- **NFR:** nên học V4_1, thêm số đo và cột tiêu chí nghiệm thu (p95, RPO/RTO, timeout phiên, dung lượng ảnh).
- **Các mục đã biết:** N13 (thứ tự V.3.2), F-16 (ERD "9 nhóm"), cập nhật sơ đồ STD-ORDER và UCD.

## 4. Nên lấy gì từ V4_1 sang v5.8

- NFR có số đo và cách nghiệm thu: NFR-10 p95; NFR-11 phiên; NFR-12 giới hạn đăng nhập sai; NFR-18 RPO ≤ 24 giờ, RTO ≤ 8 giờ; NFR-19 ảnh.
- Định nghĩa chỉ tiêu báo cáo (III.12.2).
- Chốt kỳ đối soát công nợ kèm snapshot; sửa tiền bằng bút toán đảo.
- Nghiệp vụ sự cố và sửa bè (FARM-3, FARM-4); một đơn giao nhiều đợt.
