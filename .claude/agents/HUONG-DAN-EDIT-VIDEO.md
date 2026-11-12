# Hướng dẫn edit video với skill `edit-video-talking-head`

Skill này thay 6 skill cũ (Dạng 1–4, Cấp độ 1–2). JC chỉ cần nhớ **1 câu lệnh + chọn đúng kiểu**.

## Bước 0 — Chuẩn bị (làm 1 lần)
- Chạy trên **Claude Code ở máy của JC** (cần cài được ffmpeg, Python, Node). Chat Claude thường không dựng được file MP4.
- Lần đầu Cole tự kiểm tra và cài ffmpeg, Whisper, `hyperframes`. Chỉ khi máy chặn quyền cài mới hỏi JC.
- Tạo sẵn thư mục `input/` (bỏ video vào) và `output/` (thành phẩm).

## Bước 1 — Chọn kiểu (hoặc để Cole chọn)
**Không chắc? Chỉ cần nói: `edit video này, chọn phù hợp`.** Cole tự chọn theo độ dài và nội dung video (video dài → Cấp độ 1/2; clip ngắn → Dạng 1/2/3/4), báo chị 1 dòng "chọn Dạng X vì…", rồi dựng luôn. Không hợp ý thì nói "đổi sang Dạng Y".

Muốn tự chọn thì dùng bảng:

| JC muốn | Nói câu này |
|---|---|
| Short nói chuyện gọn, sạch | `edit Dạng 1 cho video này` |
| Nhiều hiệu ứng, zoom, minh hoạ | `edit Dạng 2 cho video này` |
| Sạch, sang, kiểu chuyên gia/coach | `edit Dạng 3 cho video này` |
| Xen slide infographic trắng | `edit Dạng 4 cho video này` |
| Video dài 1 người → nhiều short | `cắt video này thành short, Cấp độ 1` |
| Podcast 2 người → short 2 ô | `cắt video podcast này thành short, Cấp độ 2` |

Hợp brand JC:
- 3 Sisters, Viet Food, JCExpress (bán hàng, giới thiệu): Dạng 1 hoặc 2.
- Khai Tâm Chay, The Jessie (chia sẻ, dạy): Dạng 3.
- Video giải thích quy trình/so sánh (ví dụ VN–SG gửi hàng thủ công vs dùng dịch vụ): Dạng 4.
- Video dài, livestream, Zoom: Cấp độ 1; có khách mời: Cấp độ 2.

## Bước 2 — Đưa đồ vào
1. Bỏ video vào `input/`.
2. Có thì nói luôn trong câu lệnh: màu thương hiệu, câu CTA, bài nhạc riêng, đoạn muốn ưu tiên.

Ví dụ:
- `edit Dạng 3 cho video này, CTA: inbox mình nhận báo giá gửi hàng`
- `cắt video này thành short, Cấp độ 1, ưu tiên đoạn nói về giá, mỗi short 30–60 giây`

## Bước 3 — Cole tự làm
Kiểm tra máy → tải font/icon/SFX/nhạc free thiếu → nghe và cắt khoảng lặng, từ đệm → viết thumbnail → caption chạy theo lời → thêm lớp riêng của kiểu đã chọn → xuất → báo đường dẫn.

## Bước 4 — Xem và sửa
Mở file trong `output/` (`...-dang1.mp4`, hoặc `...-short-01.mp4`, `-02`... đã xếp theo đoạn hay nhất trước). Sửa bằng một câu: *"thumbnail đổi chữ…"*, *"bớt zoom"*, *"đoạn 2 cắt ngắn hơn"*. Cole chỉ dựng lại đúng phần đó.

## Lưu ý
- **Nhạc trend TikTok**: Cole không tự tải (có bản quyền). JC đưa file, hoặc để Cole dùng nhạc free.
- Podcast 2 người: mặc định Cole đoán ai đang nói bằng âm thanh + chuyển động môi. Nếu hay nhận nhầm người thì thêm token HuggingFace (miễn phí, JC tự tạo 1 lần).
- Skill này chưa được chạy thử trên máy của JC. Lần đầu nên thử với 1 clip ngắn trước khi chạy hàng loạt.
- Làm xong → đăng: YouTube dùng Út Chi (`ut-chi-seo-video`), Facebook dùng `reel-facebook-viral`, caption dùng Chị Tư.
