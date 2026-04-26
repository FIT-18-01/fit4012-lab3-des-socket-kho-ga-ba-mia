# Threat Model - Lab 3

## Thông tin nhóm
- Thành viên 1: Phùn Quang Huy - MSSV: 1871020311
- Thành viên 2: Nguyễn Minh Đức - MSSV: 1871020149

## Assets
- Bản tin gốc (plaintext) gửi giữa sender và receiver.
- DES key 8 byte và IV 8 byte được truyền qua mạng.
- Ciphertext và header độ dài.

## Attacker model
Kẻ tấn công có quyền lắng nghe luồng TCP nội bộ và có thể thay đổi gói tin trên đường truyền. Kẻ tấn công không kiểm soát hoàn toàn hai đầu sender/receiver nhưng có thể can thiệp vào mạng.

## Threats
- Kẻ tấn công nghe được key và IV plaintext khi chúng được truyền cùng packet.
- Kẻ tấn công sửa ciphertext (tamper) khiến giải mã sai hoặc lộ dữ liệu không chính xác.
- Kẻ tấn công thực hiện replay lại packet cũ.
- Kẻ tấn công có thể thay đổi header độ dài và làm hỏng quá trình đọc dữ liệu.

## Mitigations
- Không bao giờ truyền key và IV plaintext trong cùng luồng dữ liệu; cần dùng kênh an toàn hoặc cơ chế trao đổi key.
- Dùng MAC / HMAC để phát hiện thay đổi ciphertext và header.
- Dùng phiên bản thuật toán mạnh hơn như AES-GCM thay vì DES-CBC.
- Thực hiện kiểm tra tính toàn vẹn độ dài packet và reject packet không đúng định dạng.

## Residual risks
Hệ thống vẫn chịu rủi ro nếu kẻ tấn công nắm quyền truy cập mạng nội bộ, vì DES bản thân đã yếu và không bảo vệ chống replay nếu không có thông tin phiên.
