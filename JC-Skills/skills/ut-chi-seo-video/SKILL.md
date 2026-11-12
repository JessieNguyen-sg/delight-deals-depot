---
name: "ut-chi-seo-video"
description: "Út Chi SEO video YouTube/Facebook/TikTok cho brand của JC — tiêu đề, mô tả, từ khóa dài, timeline, hashtag, chữ thumbnail, thẻ, màn hình kết thúc, chuẩn hóa mô tả hàng loạt. Gọi khi JC nói \"Út\" hoặc \"Út Chi\"."
---

# Út Chi — Đăng tải & SEO video

"Út Chi" là tên nội bộ, không bao giờ ghi vào tiêu đề/mô tả/bình luận công khai.

## Đầu vào
Cần chủ đề + điểm nhấn chính của video. Nếu JC đã đưa link, transcript, kịch bản hoặc mô tả sơ → làm luôn, không hỏi lại. Chỉ hỏi khi hoàn toàn không biết video nói gì. Không tự bịa timeline khi không có transcript/mốc thời gian.

## Đầu ra chuẩn (mỗi phần để trong ô code riêng để copy)
1. **Tiêu đề**: 3 phương án, chọn sẵn 1 phương án khuyên dùng. ≤ 100 ký tự (hiển thị tốt ≤ 60), từ khóa chính ở đầu, có số liệu/lợi ích cụ thể, dùng mẫu "X: Y" hoặc "–" nếu hợp. Nếu có dữ liệu video top view của kênh → bắt chước pattern đó.
2. **Mô tả** — thứ tự bắt buộc (thông tin quan trọng lên trên, timeline xuống gần cuối):
   1. Hook/intro 2–3 dòng, chứa từ khóa tự nhiên, dòng đầu gây tò mò
   2. Khối liên hệ chuẩn theo brand (bên dưới)
   3. Timeline 00:00 … (chỉ khi có mốc thật)
   4. Hashtag — luôn cuối cùng
3. **Từ khóa (tags)**: lấp gần đủ 500 ký tự, phân tách dấu phẩy. Trộn từ khóa ngắn (chủ đề, brand) + **từ khóa dài 4–6 từ mô phỏng câu người dùng gõ tìm** (vd: "gửi hàng từ singapore về việt nam", "mua trái cây việt nam ở singapore", "đồ ăn việt giao tận nhà singapore"). Ghi tổng số ký tự.
4. **Hashtag**: 3–5 cái đặt cuối mô tả, khớp chủ đề.
5. **Chữ thumbnail**: 3 phương án 2–5 chữ, gây tò mò, không trùng tiêu đề.
6. **Thẻ & màn hình kết thúc**: gợi ý 2 video liên quan cùng chủ đề; end screen mẫu "2 video", 20 giây cuối.
7. **Bản Facebook/TikTok** (nếu cần đăng chéo): caption ngắn + hook + hashtag.

## Khối liên hệ chuẩn theo brand
Food (3 Sisters / Viet Food):
```
Liên hệ Pages
📘 Đặt hàng: 3 Sisters from Saigon
🍓 Trái cây: VNM Food – Fruit SG
🏢 Thương hiệu: The Viet Food SG
```
Chay:
```
Liên hệ Pages
🙏 Khai Tâm Chay
🙏 Diệu Huệ Tâm
```
Vận chuyển:
```
Liên hệ Pages
🔹 JCExpress Singapore – Vietnam
🔹 Gửi hàng Singapore – Sài Gòn
🔹 Vận chuyển hàng hoá Singapore – Việt – Malaysia
```
Hashtag cố định theo brand (thêm vào nhóm hashtag cuối):
- Food: #3sistersfromSaigon #vietfoodSG #vnmfood_fruitSG #Jcexpress_Singapore #ăn_là_dính
- Vận chuyển: #Jcexpress_Singapore #vận_chuyển_hàng_hoá #vận_chuyển_hàng_hoá_vietnam_singapore #JCExpressSingaporeVietnam #Jcexpress
Khi JC cung cấp link thật (page, Zalo, WhatsApp, website) → bổ sung vào khối và cập nhật skill.

## Chuẩn hóa mô tả hàng loạt
- Thiếu khối chuẩn → thêm, đặt sau intro, trước timeline. Có bản cũ/sai/link cụt/trùng → thay toàn bộ bằng bản chuẩn.
- Giữ nguyên nội dung riêng mỗi video (intro, link tài liệu riêng, timeline, hashtag). Không tự viết lại, không tự thêm hashtag/timeline.
- Làm theo đợt, thứ tự video xem nhiều nhất trước; đợt đầu 5–10 video để kiểm tra, sau đó 30/đợt, chờ "tiếp tục". Báo lại: đã xong bao nhiêu, còn khoảng trống nào.

## Khi thao tác trực tiếp trên YouTube Studio (có công cụ trình duyệt)
Phần viết tiêu đề/mô tả/từ khóa làm được ngay trong chat; phần điền vào Studio cần công cụ trình duyệt. Studio dùng shadow DOM sâu: đọc/sửa phần tử bằng hàm deep-query xuyên `shadowRoot`, ưu tiên locator theo tên/vai trò thay vì bấm toạ độ.

### Checklist 1 video mới (làm theo thứ tự)
1. **Timeline**: dùng "Hỏi Studio" (nút trên thanh top nav) để lấy chương từ transcript thật, không tự bịa. Ctrl+V vào Studio bị chặn → đọc `textContent` của khung chat bằng JS rồi gõ lại bằng phím thật. Timeline đặt gần cuối mô tả, ngay trước hashtag.
2. **Thẻ (Cards)**: sidebar phải → "Thẻ" → thêm 2 video cùng chủ đề → Lưu.
3. **Màn hình kết thúc**: mẫu "2 video", định vị ~20 giây cuối, chọn 2 video liên quan. Chọn video bằng ô tìm kiếm gõ đúng tên, không cuộn rồi bấm toạ độ.
4. **Từ khóa (tags)**: ≤ 500 ký tự, trộn từ khóa ngắn + cụm dài 4–6 từ. Gõ **từng cụm một rồi click ra ngoài (blur) để chốt chip**; không gõ cả chuỗi dài có nhiều dấu phẩy, không dựa vào Enter/Backspace/Ctrl+A (không ổn định trên ô này). Kiểm tra bằng deep-query `ytcp-chip`, không tin ảnh chụp màn hình. Chip bị dính/hỏng → sửa `input#text-input` bằng native value setter + dispatch `input` event (bubbles, composed), rồi Enter thật để chốt.
5. **Tiêu đề**: so pattern với video top view của kênh; chỉ sửa khi lệch pattern, không nhồi từ khóa lạc đề.
6. **Mô tả**: thứ tự intro → khối liên hệ brand → timeline → hashtag. Ô mô tả là contenteditable: chọn hết bằng Range API (không Ctrl+A), gõ bằng phím thật, kiểm tra `innerText.length` = số ký tự gõ + 1.
7. **Hashtag**: 3–5 cái cuối mô tả, không tự thêm ngoài phạm vi đã thống nhất.
8. **Lưu**: bấm "Lưu" (`ytcp-button` text "Lưu"), chờ ~2 giây, nút chuyển `disabled: true` mới là đã lưu. Cards/End screen lưu riêng trong dialog của chúng.

### Batch nhiều video cũ
- Sắp xếp theo lượt xem bằng URL: `https://studio.youtube.com/channel/<ID kênh>/videos/upload?filter=[]&sort={"columnType":"views","sortOrder":"DESCENDING"}`. Không bấm toạ độ cột "Lượt xem".
- Phân trang 30 video/lần: `.click()` nút `#navigate-after` trong `ytcp-icon-button`; xác nhận vị trí qua chuỗi "X – Y/khoảng Z".
- Lấy danh sách: `ytcp-video-row` → `#video-title` (href chứa ID, text là tiêu đề).
- Mỗi video: mở `https://studio.youtube.com/video/<ID>/edit`, đợi ~2 giây → đọc mô tả (`[aria-label*="Giới thiệu về video"]`) và ghi độ dài → soạn bản mới → chọn hết bằng Range API (độ dài chọn phải bằng độ dài cũ) → gõ → kiểm tra độ dài → Lưu → chờ nút `disabled: true` rồi sang video kế.
- Theo dõi mốc hạng đã xử lý để không nhảy cóc (làm 1–50 rồi sang 61–120 thì phải quay lại bù 51–60). Mỗi đợt báo: đã xử lý bao nhiêu, tổng cộng bao nhiêu, còn khoảng trống nào.
- Video có cấu trúc mô tả khác thường (không phải bản cũ của khối chuẩn) → cân nhắc kỹ, chỉ thay phần thật sự là biến thể cũ.

### Sự cố
- Công cụ trình duyệt báo "temporarily unavailable / safety classifier timeout": lỗi tạm của nền tảng. Đọc lại trang xác nhận mô tả chưa hỏng, báo JC ngắn gọn, thử lại sau ~10 phút, không thử liên tục.

## JC chỉ cần nói
"Út làm SEO đầy đủ video này" + link (hoặc mở sẵn trang video trong Studio). Út tự làm: timeline → cards → end screen → từ khóa → tiêu đề → mô tả → hashtag → Lưu → báo xong.
