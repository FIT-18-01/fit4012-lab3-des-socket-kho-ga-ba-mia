# Report 1 page - Lab 3

## Thông tin nhóm
- Thành viên 1: Sinh viên 1 - MSSV: 00000000
- Thành viên 2: Sinh viên 2 - MSSV: 00000001

## Mục tiêu
Thiết kế hệ thống gửi/nhận dữ liệu mã hoá DES qua TCP socket, học cách sử dụng DES-CBC với padding PKCS#7, và xây dựng cơ chế header độ dài để định vị ciphertext.

## Phân công thực hiện
Sinh viên 1 chịu trách nhiệm chính cho `sender.py`, tạo key/IV, mã hoá dữ liệu và gửi gói tin. Sinh viên 2 chịu trách nhiệm chính cho `receiver.py`, đọc header, nhận ciphertext và giải mã. Cả hai phối hợp viết `des_socket_utils.py`, kiểm thử tự động và hoàn thiện tài liệu.

## Cách làm
`sender.py` tạo key và IV 8 byte ngẫu nhiên, mã hoá plaintext bằng DES-CBC với padding PKCS#7, rồi gửi tuần tự key + IV + length header + ciphertext qua socket. `receiver.py` lắng nghe kết nối TCP, đọc chính xác 20 byte header, phân tích key, IV và độ dài ciphertext, sau đó đọc ciphertext và giải mã.

## Kết quả
Hệ thống đã chạy thành công với phép kiểm thử cục bộ: Sender gửi bản tin, receiver nhận và giải mã về bản rõ đúng. Bộ test tự động bao gồm kiểm tra padding/header, hợp lệ giao thức, tích hợp sender/receiver local, và hai tình huống negative với dữ liệu bị sửa và sai key.

## Kết luận
Kỹ thuật:
- DES-CBC yêu cầu padding để ciphertext có độ dài bội của 8 byte.
- Header độ dài giúp receiver biết cần đọc bao nhiêu ciphertext.
Bảo mật:
- Gửi key và IV plaintext trên cùng luồng TCP là điểm yếu nghiêm trọng.
- DES và DES-CBC đều không phù hợp cho hệ thống thực tế; cần dùng AES-GCM và trao đổi key an toàn.
