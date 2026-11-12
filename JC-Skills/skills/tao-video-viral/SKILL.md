---
name: "tao-video-viral"
description: "Tạo video dọc viral hoặc TVC ngắn dạng tin tức/review/giới thiệu từ ý tưởng, URL hay ảnh tham chiếu, dùng tư liệu thật, phụ đề karaoke, xuất MP4."
---

# Tạo video viral — dọc, hook 2 giây, tư liệu thật

## Skill này làm gì
Dựng video dọc hoàn chỉnh (TikTok/Reels/Shorts) hoặc cảnh TVC ngắn không
thoại, xuất thẳng MP4 — không dừng ở kịch bản/storyboard khi khách đã yêu
cầu xuất hay cho xem.

**Yêu cầu**: cần Claude Code/Codex (dựng bằng framework composition video có
sẵn trong hệ thống, ví dụ `hyperframes`) để render thật ra file MP4 — không
làm được trên chat AI thường.

## Chọn máy dựng theo đầu ra
- Video viral hoàn chỉnh, nhiều cảnh, có lời dẫn/phụ đề: dùng framework
  composition/video có sẵn trong hệ thống AI đang dùng (skill `hyperframes`
  nếu có), theo đúng workflow nó chọn.
- Cảnh TVC 4-10 giây từ ảnh tham chiếu: dùng Flow Omni (xem mục "Cảnh TVC
  bằng Flow Omni" bên dưới), rồi ghép các cảnh lại nếu video dài hơn 1 cảnh.
- Mọi nhu cầu ảnh/video/giọng/nhạc/phụ đề: dùng đúng công cụ xử lý media có
  sẵn trong hệ thống AI đang dùng nếu có (đừng tự chế cách làm riêng khi đã
  có công cụ chuyên biệt).

## Mẫu hình ảnh vàng (mặc định, chỉ đổi khi khách yêu cầu rõ)
- Dọc 9:16, mặc định 1080×1920, 30fps.
- Ảnh/video thật phủ toàn màn hình; crop ưu tiên khuôn mặt và hành động.
- Lớp phủ tối ấm giúp chữ rõ nhưng không mất chi tiết chủ thể.
- Nhãn chương trên trái, nguồn/chủ đề trên phải, headline nửa dưới.
- Màu: than `#242321`, kem `#F2E8D8`, trắng kem `#FFF9EE`, vàng nhấn
  `#E6B93F`, cam đỏ phụ `#D9653B`.
- Headline: font display đậm hỗ trợ tiếng Việt đã xác minh (đừng dùng font
  lỗi dấu); metadata dùng font mono, body dùng font sans thường.
- Headline 2-4 dòng, một từ khoá tô vàng, căn trái, không che mặt.
- Chuyển động: push-in ảnh nhẹ 1.00→1.06/1.08 toàn cảnh; headline vào bằng
  dịch chuyển + mờ dần trong 0.5-0.8s; timeline vẽ bằng kéo giãn ngang; card
  dữ kiện vào so le ngắn. Không lạm dụng glitch/neon/shader làm khó đọc.
- Nhịp kể: mỗi cảnh một ý + một bằng chứng chính. Hook → bối cảnh → mục
  đích/lợi ích → hoạt động/minh chứng → số liệu/cộng đồng → kết luận. Cảnh
  giữ 6-10s; nội dung 90 giây thường dùng 9-12 cảnh.

## Cấu trúc theo định dạng (45 giây mặc định)

**Tin tức**: 0-3s hook câu hỏi/hệ quả đáng chú ý → 3-10s sự việc/xu hướng là
gì → 10-20s ví dụ/nhân vật tiêu biểu → 20-30s vì sao quan trọng → 30-38s
giới hạn/phản biện/góc nhìn con người → 38-45s kết luận + nguồn. Giọng đọc
nhanh vừa, trung lập, hiện tại đơn. Hiển thị nhãn nguồn/ngày khi tin có tính
thời sự.

**Review**: 0-3s phán đoán/câu hỏi mua-không → 3-10s sản phẩm dành cho ai →
10-24s 2-3 ưu điểm có bằng chứng hình ảnh → 24-34s nhược điểm/điều cần biết
→ 34-41s kết luận theo nhóm người dùng → 41-45s giá/nguồn/CTA nếu đã xác
minh. **Không tuyên bố đã trải nghiệm nếu chỉ tổng hợp tài liệu** — dùng
cụm "theo thông số", "theo nhà sản xuất", "dựa trên nguồn...".

**Giới thiệu**: 0-3s lời hứa/vấn đề chính → 3-10s đối tượng là ai/cái gì →
10-25s ba điểm nổi bật → 25-35s cách hoạt động/minh hoạ thực tế → 35-42s lợi
ích + đối tượng phù hợp → 42-45s tên/nguồn/CTA nhẹ. Nội dung tài trợ/quảng
cáo: giữ nguyên nhận diện, tránh biến nhận định thành dữ kiện.

**Điều chỉnh thời lượng**: 15-30s → 4 cảnh, 1 ý chính, tối đa 2 bằng chứng.
45-60s → 6-8 cảnh, 1 phản biện/hạn chế. 60-90s → chia 3 hồi, thêm ngữ cảnh/
ví dụ/kết luận.

## Hàng rào bắt buộc — tư liệu thật
- Mỗi video phải có cả ảnh thật và video thật, trừ khi nguồn công khai không
  có video và khách chấp nhận ngoại lệ. **Ít nhất 70% thời lượng hình ảnh là
  media thật liên quan trực tiếp** — motion graphics chỉ giải thích, không
  thay thế bằng chứng.
- Thứ tự nguồn ưu tiên: (1) media khách cung cấp, (2) website/Facebook/
  YouTube/TikTok/press kit chính thức, (3) bài báo/đơn vị phát hành gốc, (4)
  stock có giấy phép chỉ dùng cho bối cảnh chung, đúng ngữ cảnh.
- Lập ledger khi lấy media: đường dẫn local, URL nguồn, loại media, chủ thể,
  ngày lấy, cảnh sử dụng. Tải về local trước khi dựng, không dùng URL mạng
  làm tài sản render trực tiếp.
- Nếu không đủ media thật: **dừng và báo phần thiếu**. Không tạo hình AI để
  giả làm tư liệu thật, không dùng stock/thumbnail sai ngữ cảnh.
- Không bịa video, số liệu, trích dẫn, trải nghiệm review hay thành tích.
  Không sao chép dài nguyên văn nguồn; diễn đạt lại, ghi nguồn gần dữ kiện.

## Phụ đề karaoke (mặc định)
- Chỉ dùng phụ đề karaoke trên video thật; không thêm headline lớn/chapter
  label/data card/khung giá/CTA thẻ nếu khách không yêu cầu rõ.
- Chia lời thành cụm 2-5 từ, ưu tiên kết thúc tại dấu câu/ranh giới ý nghĩa.
  Mỗi thời điểm chỉ hiện 1 cụm, không chồng nhau ở điểm chuyển.
- Đặt phụ đề ở vùng an toàn phía dưới, chừa giao diện TikTok/Reels.
- Chữ chưa đọc màu trắng kem; từ đang đọc màu vàng `#E6B93F`, có thể scale
  nhẹ tối đa 1.08. Dùng bóng chữ/gradient tối nhẹ phía dưới tăng tương phản,
  không dùng hộp nền lớn.
- Đồng bộ bằng word timing THẬT (TTS có timestamps, forced alignment, hoặc
  transcription word-level) — không chia đều theo số chữ. Mỗi cụm cách cụm
  kế tiếp ≥0.02s để tránh chồng hình.
- Không render nếu còn cụm 1 từ, cụm >5 từ, hai dòng chồng nhau, hoặc
  highlight lệch lời rõ rệt.

## Cảnh TVC bằng Flow Omni (khi cần cảnh 4-10s từ ảnh tham chiếu)
- Chế độ Video, Omni 1.1 Flash (hoặc bản Omni mới nhất khách chọn), tỷ lệ
  9:16, chất lượng cao nhất khả dụng, 10 giây (trừ khi khách yêu cầu khác),
  x1 để thử nhận diện trước.
- Dùng đúng 1 ảnh tham chiếu chính cho mỗi nhân vật cần khoá nhận diện, gắn
  vào ô "Bắt đầu". Nêu rõ thuộc tính phải giữ: exact face, hairstyle,
  glasses, skin tone, body proportions, outfit and props.
- Chuyển động nhỏ, sang, tự nhiên: eye contact, gentle head turn, subtle hand
  movement, slow push-in. Tránh xoay đầu nhanh, đổi góc toàn thân đột ngột,
  thêm người — dễ làm lệch mặt.
- Prompt khung mẫu: `Premium vertical fashion TVC. Preserve the exact identity, face, hairstyle, glasses, skin tone, body proportions, outfit and props from the reference. The subject makes elegant eye contact, a subtle head turn and one refined hand movement. Slow cinematic push-in, soft champagne beauty lighting, realistic luxury editorial photography, stable anatomy, no extra people, no text, no logo, no identity change.`
- Cổng duyệt: mặt không trôi/méo/đổi người; tay/kính/tóc/trang phục/đạo cụ
  không biến dạng; không chữ rác/logo tự sinh; crop dọc không cắt mắt/cằm/
  bàn tay/sản phẩm chính; chuyển động có chủ đích, không rung giật.
- Xem toàn bộ video trước khi duyệt, chỉ tải MP4 hoặc đưa vào dựng tiếp sau
  khi đã xem hết.

## Quy trình bắt buộc
1. Phân tích đầu vào: URL thì đọc nội dung/ngày/tác giả/dữ kiện/ảnh/video
   nhúng; ý tưởng thì nghiên cứu nguồn chính thức; tệp thì ưu tiên tài liệu
   khách đưa.
2. Chọn cấu trúc tin tức/review/giới thiệu phù hợp (xem trên).
3. Mặc định 1080×1920, 30fps, tiếng Việt, hook trong 2 giây đầu. Không có
   thời lượng yêu cầu thì dùng 45 giây; 60-90 giây thì chia ba hồi.
4. Viết brief + storyboard + kịch bản trước khi dựng — phân biệt rõ dữ kiện,
   suy luận và đề xuất.
5. Thực hiện cổng media thật (mục trên) trước khi dựng. Không dựng khi chưa
   có bộ tư liệu đạt yêu cầu.
6. Tải toàn bộ media cần render về dự án local.
7. Dựng theo mẫu vàng về màu/crop/nhịp hình; mặc định chỉ hiển thị phụ đề
   karaoke, không thêm tiêu đề lớn/nhãn chương/khung giá/CTA thẻ nếu khách
   không yêu cầu rõ.
8. Chạy cổng chữ tiếng Việt (mục dưới) trước và sau khi dựng. Không cho
   duyệt khi còn chữ lỗi, tràn, che mặt hoặc xuống dòng xấu.
9. Giọng đọc là mô-đun thay thế được — nếu chưa có giọng cụ thể, dùng giọng
   tiếng Việt tự nhiên khả dụng và ghi rõ là giọng tạm. Nhạc nền thấp hơn
   lời đọc.
10. Kiểm tra kỹ thuật (hyperframes check nếu dùng framework đó), chụp
    midpoint mỗi cảnh, xem contact sheet ở kích thước điện thoại. Sửa lỗi
    chữ/crop/cảnh đen/media đóng băng/sai nguồn trước khi cho duyệt.
11. Cho khách duyệt contact sheet/preview. Chỉ render khi khách nói "xuất",
    "bật", "cho xem" hoặc đồng ý rõ ràng.
12. Render MP4 chất lượng cao; xác minh hình/tiếng/dung lượng/thời lượng
    bằng `ffprobe`; hiển thị video bằng đường dẫn tuyệt đối.

## Cổng chữ tiếng Việt (bắt buộc trước và sau khi dựng)
- UTF-8 mọi file; `<meta charset="UTF-8">` trong composition.
- Không chuyển chữ Việt qua shell/code page có thể mất dấu. Tìm trước duyệt:
  `�`, ô vuông, dấu hỏi thay thế, mojibake kiểu `Ã`, `Æ`, `áº`, `á»`.
- Chỉ dùng font bundled/local đã xác minh có glyph tiếng Việt. Nếu font
  display làm dấu lệch/rơi, đổi sang font sans phổ biến hỗ trợ tiếng Việt
  tốt (không giữ font đẹp nhưng lỗi dấu).
- Headline tối đa 7 từ/cụm, 2-4 dòng. Vùng an toàn tối thiểu 6% mỗi cạnh.
  Không để chữ che mắt/miệng/tay/sản phẩm chính. Không đặt 2 khối chữ dài
  cùng 1 vùng.
- Kiểm 2 vòng: trước dựng soát chính tả/dấu câu/tên riêng/số/cách đọc TTS;
  sau dựng chạy kiểm tra kỹ thuật + snapshot midpoint mọi cảnh, xem contact
  sheet kích thước nhỏ. Không cho duyệt nếu còn mất dấu/font vuông/mojibake/
  chữ tràn/tương phản kém/phụ đề che chủ thể.

## Cổng kiểm tra chất lượng trước bàn giao
- **Nội dung**: hook 2 giây đầu; số liệu/tên riêng/tuyên bố quan trọng đều
  có nguồn; không câu đọc dài hơn thời lượng cảnh; kết luận trả lời đúng hook.
- **Hình ảnh**: ≥70% thời lượng là media thật liên quan trực tiếp, đã tải
  local và có credit; chủ thể không bị crop mất mặt; chữ không chạm biên;
  không cảnh đen/media đóng băng ngoài chủ ý.
- **Âm thanh**: lời dẫn rõ, phát âm đúng tên riêng, không cắt cuối câu; nhạc
  nền thấp hơn lời dẫn, fade đầu/cuối; phụ đề khớp ý lời nói.
- **Kỹ thuật**: không lỗi chặn render; media có timing hợp lệ; MP4 có hình +
  âm thanh + dung lượng khác 0, thời lượng nằm trong ±0.25s so với yêu cầu.

## Hàng rào tuyệt đối
- Không thay tư liệu thật bằng hình AI chỉ vì dễ tìm hơn.
- Không dùng ảnh stock chung chung để giả làm nhân vật/sản phẩm/địa điểm/sự
  kiện cụ thể. Không dùng ảnh tham chiếu của người này để tạo thành người khác.
- Không bịa video/số liệu/trích dẫn/trải nghiệm/thành tích.
- Không render nếu còn lỗi chặn chữ/media hoặc chưa xem contact sheet bằng mắt.
- Không đưa khoá API, OTP, cookie hay thông tin đăng nhập vào bất kỳ file
  bàn giao nào.

## Bàn giao
Trả về video phát được, link tải MP4, thời lượng, tỷ lệ, nguồn chính đã
dùng, giọng đã dùng. Mời khách gửi voice mới nếu muốn thay giọng mà không
phải dựng lại hình.

## Khách chỉ cần làm gì
1. Đưa ý tưởng/văn bản/URL/ảnh tham chiếu, và media thật nếu có sẵn.
2. Nói rõ định dạng mong muốn (tin tức/review/giới thiệu) + thời lượng nếu có.
3. Duyệt contact sheet/preview trước khi nói "xuất".

Agent tự động: nghiên cứu + soạn brief/storyboard/kịch bản → tìm & tải media
thật → dựng theo mẫu vàng + phụ đề karaoke → chạy đủ cổng kiểm tra → cho
khách duyệt → render MP4 → xác minh kỹ thuật → giao file.

## Trước và sau khi dựng (nối với các skill khác của JC)
- **Trước:** ý tưởng/kịch bản chưa chắc → chạy `video-trieu-view-8-yeu-to` chấm 8 yếu tố; cần hook/tiêu đề → `the-jessie-hook-tieu-de`.
- **Sau:** đăng Facebook đều đặn → `reel-facebook-viral`; đăng YouTube → `ut-chi-seo-video`; caption/hashtag cuối bài đúng brand → `chi-tu-viet-bai`.
- Skill này đã gồm toàn bộ quy trình của `videoviral` (bản gốc ngắn hơn, trỏ tới tệp tham chiếu không có sẵn) nên không cần dùng hai skill song song.
