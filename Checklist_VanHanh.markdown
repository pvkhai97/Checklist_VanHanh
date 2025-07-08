# Checklist Vận Hành Hệ Thống

Dưới đây là checklist vận hành hệ thống được trình bày theo các giai đoạn trong ngày, được tổ chức rõ ràng và dễ theo dõi.

## 1. Đầu Ngày

| STT | Công việc | Máy | Các bước thực hiện | Kết quả mong muốn | Kết quả vận hành | Ghi chú |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Kiểm tra gw_files Horizon | 10.21.189.39 | Kiểm tra tomcat đã được restart từ ngày trước chưa? | Còn gw_files với ngày cuối giờ ngày làm việc trước. Nếu chưa, bật trước 7h50. | 0 | Nếu chưa bật, bật lại Tomcat trước 8h. |
| 2 | Kiểm tra backup thư mục Log GW_FILE (HSX) | 172.21.2.10 (HSXGateway) | Kiểm tra ổ C:\\FSS\\exchangeKrx còn thư mục gw_file không? | Không còn thư mục gw_file, đã backup vào BACKUP với tên gw_file_yyyy_MM_dd. | 1 |  |
| 3 | Start HSX GW | 172.21.2.10 (HSXGateway) | Chạy file Start_ORS trên desktop. | Start bình thường, không có log Exception. | 1 |  |
| 4 | Kiểm tra log I- kết nối HSX GW | 172.21.2.10 (HSXGateway) | Kiểm tra log bắt tay trên baratail, đoạn connect I success (I_OMS1, I_OMS2). | Cả 2 I_OMS1 và I_OMS2 kết nối thành công. | 1 |  |
| 5 | Kết nối đến Gateway HSX | 172.21.2.10 (HSXGateway) | Mở Firefox, đăng nhập HSX GW status, để Mode "Startup", nhấn Start. | Trạng thái kết nối: CONNECTION_ESTABLISHED. | 1 |  |
| 6 | Kiểm tra backup thư mục Log GW_FILE (HNX) | 172.21.2.11 (HNX Gateway) | Kiểm tra ổ C:\\FSS\\exchangeKrx còn thư mục gw_file không? | Không còn thư mục gw_file, đã backup vào BACKUP với tên gw_file_yyyy_MM_dd. | 1 |  |
| 7 | Start HNX GW | 172.21.2.11 (HNX Gateway) | Chạy file StartORS.bat trên desktop. | Start bình thường, không có log Exception. | 1 |  |
| 8 | Kiểm tra log I- kết nối HNX GW | 172.21.2.11 (HNX Gateway) | Kiểm tra log bắt tay trên baratail, đoạn connect I success (I_OMS1, I_OMS2). | Cả 2 I_OMS1 và I_OMS2 kết nối thành công. | 1 |  |
| 9 | Kết nối đến Gateway HNX | 172.21.2.11 (HNX Gateway) | Mở Firefox, đăng nhập HNX GW status, để Mode "Startup", nhấn Start. | Trạng thái kết nối: CONNECTION_ESTABLISHED. | 1 |  |
| 10 | Bật GW_Monitor.exe | 10.21.189.25 | Chạy GW_Monitor.exe, đăng nhập với tài khoản ithn/bsc@123a. | Đăng nhập thành công. | 1 |  |
| 11 | Start GW_Monitor.exe | 10.21.189.25 | Chạy GW_Monitor.exe, nhấn Start trên tab HOSE và HNX, nhập user (ithn/bsc@123a). | Xử lý hết message, số lượng message xử lý bằng số nhận về. Process HOSE = Y. | 1 | Nếu job đã ENABLE, stop và start lại. Kiểm tra thời gian start job trong tab Logs. |
| 12 | Restart Engine | 10.21.189.60 | Vào Task Manager, restart KARAF. | Restart thành công. | 1 |  |
| 13 | Kiểm tra baratail | 10.21.189.60 | Kiểm tra log baratail, dòng Refresh Application. | Kiểm tra hoàn tất. | 1 |  |
| 14 | Start FDS Monitor | 10.21.189.53 | Bật Monitor (ithn/bsc@123a). | Đăng nhập thành công. | 1 |  |
| 15 | Start Auto Trading Engine | 10.21.189.53 | Trong tab Auto Trading Engine, nhấn Start. | JOB status thành ENABLE. | 1 | Nếu job đã ENABLE, stop và start lại. |
| 16 | Start HNX đẩy lệnh | 10.21.189.53 | Kiểm tra Service Status trong tab General, nhấn Start trong mục HNX. | All Service Status: CONN, HNX CONN: CONNECTION_ESTABLISHED, chỉ số INDEX, BOND, BONDL = 13 hoặc 15. | 1 |  |

## 2. Bước Sau 3 Giờ

| Máy | Công việc | Các bước thực hiện | Thời gian | Ghi chú |
| --- | --- | --- | --- | --- |
| 10.21.191.38 | Bật infofile CS để lấy Databond | Bật infofile CS, sau 4h10 click runSynceDatabon trên desktop. | 3h10 |  |
| 10.21.189.24 | Thay đổi tham số Hold/Unhold | Vào màn hình Hold/Unhold, set tần suất từ 10 thành 1000. | Sau bước trên |  |

## 3. Cân Lệnh

| STT | Công việc | Máy | Các bước thực hiện | Kết quả mong muốn | Hệ thống | Ghi chú |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Reset Info file cơ sở | 10.21.191.38 | Reset Infofile (tắt rồi bật lại). | Kết nối reset thành công. | FDS | Khoảng 15h10. |
| 2 | Thay đổi tham số Phong tỏa giải tỏa | 10.21.189.24 | Vào Flex-HN: 111609, sửa tần suất từ 10 -&gt; 1000. | Sửa thành công. |  |  |
| 3 | Chấm lệch tiền + chứng + orders trên OMS | DB FLEX | Vào C:\\Scripts_SQL, chạy script chấm. | Không có dữ liệu lệch. |  |  |
| 4 | Báo cho nghiệp vụ | PC | Vào Skype, thông báo trong room Hỗ trợ nghiệp vụ và vận hành Core. | Báo thành công. |  |  |

## 4. Tắt Phần Mềm

| STT | Công việc | Máy | Các bước thực hiện | Kết quả mong muốn | Ghi chú |
| --- | --- | --- | --- | --- | --- |
| 3 | Đồng bộ dữ liệu FLEX sang FDS, chạy đồng bộ trái phiếu | 10.21.189.53 | Chạy FDS: 330201, đồng bộ thông tin chứng khoán, khách hàng, chuyển tiền. | Đồng bộ thành công. |  |
| 5 | Tắt HOSE GW | 172.21.2.10 | Tắt StartGWHOSE.bat trên desktop. | Tắt thành công. |  |
| 6 | Backup thư mục log gw_file (HOSE) | 172.21.2.10 | Backup thư mục gw_file vào BACKUPLOG với tên gw_file_yyyy_MM_dd. | Backup thành công. |  |
| 7 | Backup thư mục log gw_file (HNX) | 172.21.2.11 | Backup thư mục gw_file vào BACKUPLOG với tên gw_file_yyyy_MM_dd. | Backup thành công. |  |
| 8 | Tắt FiX (OMS) HNX | 172.21.2.11 | Tắt màn hình command StartFiX đang chạy. | Tắt thành công. |  |
| 9 | Backup thư mục log gw_file của HNX FIX | 172.21.2.11 | Backup thư mục gw_file vào BACKUPLOG với tên gw_file_yyyy_MM_dd. | Backup thành công. |  |
| 10 | Stop tiến trình HOSE-Monitor | 10.21.189.25 | Trong GW_Monitor.exe, nhấn STOP trên tab HOSE, nhập user/pass. | Stop thành công. |  |
| 11 | Stop tiến trình HNX-Monitor | 10.21.189.25 | Trong GW_Monitor.exe, nhấn STOP trên tab HNX, nhập user/pass. | Stop thành công. |  |
| 12 | Stop FDS Monitor | 10.21.189.53 | Kiểm tra trạng thái HNX CONN, INDEX, BOND, BONDL; nhấn STOP trong tab General. | Stop thành công. |  |
| 13 | Tắt hệ thống Horizon | 10.21.189.41 | Chạy lệnh: `su horizon`, `cd /home/horizon/HorizonSoftware`, `./hori.sh`, chọn 1, STOP, chọn y. | Tắt thành công, xuất hiện dòng Kill. |  |
| 15 | Stop tomcat | 10.21.189.39 | Nháy chuột phải biểu tượng Apache Tomcat trên taskbar, chọn Stop service. | Stop thành công. |  |
| 16 | Tắt Fix Market Data | 10.21.189.39 | Tắt ứng dụng, backup folder gateway vào thư mục backup. | Tắt bình thường, log được backup. |  |
| 17 | Tắt Fix Order | 10.21.189.40 | Tắt ứng dụng, backup folder gateway vào thư mục backup. | Tắt bình thường, log được backup. |  |
| 18 | Bật lại Tomcat | 10.21.189.39 | Nháy chuột phải biểu tượng Apache Tomcat, chọn Start service. | Start thành công. |  |
| 20 | Chạy ghi giá TP HNX | 10.21.189.53 | Chạy ghi dữ liệu giá TP HNX trên desktop. | Chạy thành công. |  |

## 5. Flex Batch

### Chạy Batch Giữa Ngày

| STT | Công việc | Máy | Các bước thực hiện | Kết quả mong muốn | Ghi chú |
| --- | --- | --- | --- | --- | --- |
| 1 | Cập nhật giá đóng cửa tự tính | Jump | Chạy script trong C:\\Script_SQL: 1. Chuan bi Update_price_tu_tinh.sql, 2. Update_price_tu_tinh.sql, 3. Check_lai_gia_update.sql. | Chạy thành công. |  |
| 2 | Kiểm tra không còn GD với ngân hàng | PC | Flex-HN: 111614, kiểm tra giao dịch. | Không còn giao dịch. |  |
| 3 | Tắt bảng vận hành thu hộ, chi hộ | 10.21.189.24 | Tắt chương trình. | Tắt bình thường, không lỗi. |  |
| 4 | Kiểm tra GW Monitor đã tắt Job | 10.21.189.25 | Kiểm tra Process MSG HOSE và HNX thành N. | Job tắt thành công. |  |
| 5 | Đóng cửa Chi nhánh Hội sở | 10.21.189.25 | Chạy Flex-HN: 011004. | Thông báo đóng cửa thành công. |  |
| 6 | Đóng cửa Chi nhánh HCM | 10.21.189.25 | Chạy Flex-HCM: 011004. | Thông báo đóng cửa thành công. | Lưu ý: Đóng/khởi tạo chi nhánh nào thì vào Flex đó. |
| 7 | Đóng cửa Hội sở tổng | 10.21.189.25 | Chạy Flex-HN: GD 011002. | Thông báo đóng cửa thành công. |  |
| 8 | Chạy batch giữa ngày | 10.21.189.25 | Chạy Flex-HN: GD 011009. | Batch giữa ngày thành công. | Lưu ý: Không nhầm với batch cuối ngày. |

### Vận Hành Đầu Ngày Sau Batch

| STT | Công việc | Máy | Các bước thực hiện | Kết quả mong muốn | Ghi chú |
| --- | --- | --- | --- | --- | --- |
| 1 | Chạy vận hành đầu ngày OMS | 10.21.189.82 | Chạy `./start_beginofday.sh`, pass: bsc.123, reset I-OMS: karaf. | Vận hành bình thường, không lỗi. | Báo FSS nếu có lỗi. |
| 2 | Vào trang quản trị OMS | PC | Truy cập 10.21.189.104:13111 (admin/admin), set trạng thái HOSE, HNX, UPCOM sang NEW. | Set trạng thái thành công. |  |
| 3 | Khởi tạo Hội sở tổng | 10.21.189.25 | Chạy Flex-HN: GD 011001. | Thông báo khởi tạo thành công. |  |
| 4 | Khởi tạo Chi nhánh Hội sở | 10.21.189.25 | Chạy Flex-HN: GD 011003. | Thông báo khởi tạo thành công. |  |
| 5 | Khởi tạo Chi nhánh HCM | 10.21.189.25 | Chạy Flex-HCM: GD 011003. | Thông báo khởi tạo thành công. |  |
| 6 | Đồng bộ dữ liệu Chi nhánh Hội sở | 10.21.189.25 | Chạy FlexCustodianHN: GD 010001, mục 9 -&gt; 12, nhấn đồng bộ. | Hoạt động bình thường, không lỗi. |  |
| 7 | Đồng bộ dữ liệu Chi nhánh HCM | 10.21.189.25 | Chạy FlexCustodianHCM: GD 010001, mục 9 -&gt; 12, nhấn đồng bộ. | Hoạt động bình thường, không lỗi. |  |
