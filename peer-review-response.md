# Peer Review Response

## Thông tin nhóm
- Thành viên 1: Phùn Quang Huy - MSSV: 1871020311
- Thành viên 2: Nguyễn Minh Đức - MSSV: 1871020149

## Thành viên 1 góp ý cho thành viên 2
Mã rõ ràng, nhưng cần thêm kiểm tra lỗi khi `recv_exact` không nhận đủ byte. Đề nghị viết thêm comment cho `des_socket_utils.py` để giải thích header và padding.

## Thành viên 2 góp ý cho thành viên 1
Sender hoạt động tốt, nhưng đầu ra cần ghi log rõ ràng và hỗ trợ biến môi trường để chạy local. Nên điều chỉnh để in ra UTF-8 trên Windows.

## Nhóm đã sửa gì sau góp ý
Chúng tôi đã bổ sung `sys.stdout.reconfigure(encoding='utf-8')` trong cả sender và receiver để tránh lỗi Unicode trên Windows. Chúng tôi cũng thêm `requirements.txt`, hoàn chỉnh tài liệu nhóm và mô tả threat model, và xác nhận bộ test tự động chạy thành công.
