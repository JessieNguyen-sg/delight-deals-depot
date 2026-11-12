---
name: "the-jessie-chan-dung-giu-guong-mat"
description: "The Jessie – Bộ ảnh chân dung giữ nguyên khuôn mặt từ 1 ảnh: gộp 3 bộ concept cố định: Blue Floral Luxury (4 ảnh), Six Fashion (6 ảnh: Old Money Café, Gen Z Street, High Fashion City, Commercial Lifestyle, Luxury Resort, Monaco Business Luxury), LUCKY LE Phượng Hoàng Lửa Couture (6 ảnh). Gọi khi JC gửi ảnh mặt rồi nói 'blue floral', 'bộ 6 ảnh thời trang', 'LUCKY LE', hoặc 'làm bộ chân dung' / 'chọn phù hợp' (Cole tự chọn bộ). Concept tự do theo ảnh hoặc sản phẩm → dùng the-jessie-auto-5."
---

# The Jessie – Bộ ảnh chân dung giữ nguyên khuôn mặt

Gộp từ `blue-floral-luxury-portrait-4x`, `create-six-fashion-portraits`, `lucky-le`. Ba bộ này lặp lại cùng một khung: khóa danh tính, khóa phong cách, tạo từng ảnh riêng, kiểm tra từng ảnh. Khung chung viết một lần dưới đây; mỗi bộ chỉ giữ phần concept riêng.

Không gộp (việc khác hẳn): `the-jessie-auto-5` (5 concept tự do theo thư viện DNA, người/sản phẩm), `jc-ai-fashion-sg-vn` (ảnh bán quần áo SG–VN, giữ đúng món đồ thật).

## Chọn bộ
| JC muốn | Bộ | Số ảnh |
|---|---|---|
| Sang trọng, hoa xanh, đầm pha lê sapphire | **Blue Floral Luxury** | 4 |
| Đa phong cách thời trang đời thường – cao cấp (café, street, city, resort, Monaco) | **Six Fashion** | 6 |
| Couture đỏ ruby, phượng hoàng lửa, điện ảnh | **LUCKY LE** | 6 |

**Chế độ tự chọn** (JC nói "làm bộ chân dung", "chọn phù hợp", chỉ gửi ảnh): ảnh/yêu cầu nói tông xanh, hoa, pha lê → Blue Floral; nói đỏ, quyền lực, phượng hoàng → LUCKY LE; còn lại → **Six Fashion** (đa dạng, an toàn nhất). Báo 1 dòng "Cole chọn bộ X vì …" rồi làm luôn, không hỏi lại. JC muốn đổi thì nói "đổi sang bộ Y".

## Khung chung cho cả 3 bộ

### Đầu ra: tạo ảnh hay xuất prompt?
- Có công cụ sinh ảnh trong phiên → tạo từng ảnh riêng (không collage, không sprite sheet, không chèn chữ lên ảnh).
- Không có công cụ sinh ảnh (mặc định của Claude) → xuất **prompt tiếng Anh, mỗi ảnh một ô code riêng** + negative prompt trong ô code thứ hai, kèm 1–2 dòng tiếng Việt hướng dẫn dán sang Gemini / ChatGPT / Midjourney và đính kèm ảnh mặt gốc. Mỗi lượt 1 prompt; JC gõ "2", "tiếp" thì ra ảnh kế (trừ khi JC nói "cho hết luôn").
- Midjourney: thêm đuôi `--ar 3:4 --style raw --v 7` (Blue Floral) hoặc `--ar 9:16` (LUCKY LE) và đổi negative thành `--no ...`.

### Khóa nhận diện (bắt buộc, đặt ở ĐẦU mọi prompt)
> Use the uploaded face photo as the exact identity reference. This is exactly the same person as in the reference photo, not a new person with similar features. Preserve 100%: facial structure and proportions, forehead and hairline, eyebrows and eye spacing, eye shape and eyelids, nose bridge and tip, lips, chin and jawline, apparent age, skin tone, glasses if present, characteristic hairstyle and hair colour. Do not beautify into a different face.

- Dùng ảnh gốc làm nguồn nhận diện cho TỪNG ảnh; không dùng ảnh vừa sinh làm nguồn duy nhất cho ảnh sau (sai lệch tích lũy).
- Không Tây hóa, không trẻ hóa, không mắt anime, cằm nhọn, mũi quá nhỏ, da trắng bệch hay mặt nhựa. Giữ nét Việt Nam, lỗ chân lông, nếp cười.
- Chưa có ảnh khuôn mặt rõ → xin 1 ảnh (mặt rõ, không bị che, không quá mờ/nhỏ). Có nhiều người mà không xác định được nhân vật chính → hỏi người nào. Không bao giờ dùng hoặc đoán khuôn mặt của người khác.
- Ưu tiên độ giống mặt hơn độ hoàn hảo của thời trang/bối cảnh.

### Khóa phong cách (từ ảnh thứ 2 trở đi)
Lặp nguyên văn "bất biến" của bộ (đầm/trang phục, trang điểm, tóc, trang sức, bảng màu, ánh sáng) và chỉ đổi: dáng, góc máy, khoảng cách/crop, vị trí hoa/đạo cụ, hướng nhìn.

### Chất ảnh chung
Photorealistic, high-end editorial, tóc có sợi, vải có chất liệu, da có kết cấu thật, hậu cảnh có chiều sâu. Ánh sáng chính mềm chéo 30–45°, catchlight rõ trong mắt, viền sáng nhẹ tách nền, không cháy vùng sáng, không flare che mặt, không ám màu, không HDR giả.

### Negative prompt chuẩn
```
different person, identity drift, face change, different facial proportions, asymmetrical eyes, crossed eyes, deformed face, plastic skin, wax skin, oversmoothed skin, anime, cartoon, illustration, 3D render, bad hands, duplicate hands, extra fingers, missing fingers, fused fingers, extra limbs, distorted jewellery, blurred face, low resolution, overexposed skin, text, logo, watermark, extra people
```

### Kiểm tra từng ảnh (trước khi sang ảnh kế)
Đúng người? Tuổi, tông da, đường chân tóc có đổi không? Cổ, vai, tay, ngón, chân có tự nhiên không? Đạo cụ có dính tay/xuyên người không? Mắt cân đối, cùng hướng, có catchlight? Da có cháy/xám không? Không chữ/logo/watermark/người thừa. Lỗi → chỉ tạo lại ảnh đó (tối đa 2 lần), nhấn mạnh phần cần sửa, **không đổi các ảnh đã đạt**, không đổi "bất biến" khi sửa. Ảnh lệch mặt: viết lại prompt với khóa nhận diện đặt lên đầu, nhấn mạnh hơn, rút gọn bối cảnh. Không giao thiếu ảnh.

### Bài đăng kèm (nếu JC cần)
Viết mới theo đúng ảnh và CTA JC đưa; không bịa giá, số liệu, khan hiếm, kết quả. Cụm cuối bài theo brand: xem `chi-tu-viet-bai`.

---

## Bộ 1 — Blue Floral Luxury (4 ảnh, 3:4)
Bất biến: sapphire-blue off-shoulder crystal couture gown (silver gemstone details), makeup, hair, crystal jewellery, royal-blue palette, lighting.
Khối style chung (đưa vào cả 4 prompt): *Ultra-realistic high-end editorial beauty campaign, 85 mm portrait lens aesthetic, real visible skin texture and pores, shallow depth of field, soft cinematic studio lighting, dreamy bokeh, crystal sparkle, rainbow prism reflections. Royal/sapphire blue giant peonies. Crystal-covered sapphire off-shoulder ball gown with silver gemstone details and matching crystal jewellery. Vertical 3:4, 8K, premium magazine finish.*
Câu khóa style (từ ảnh 2): *Keep exactly the same sapphire-blue off-shoulder crystal couture gown, makeup, hair, crystal jewellery, royal-blue palette, and lighting as the previous image. Change only pose, camera angle, crop, flower placement, and gaze direction.*
1. **Giant Floral Fantasy**: three-quarter-body, bao quanh bởi cánh mẫu đơn xanh royal khổng lồ; một tay chạm cánh hoa, tay kia giữ váy; nhìn hơi xuống hoặc nghiêng mặt; ánh xanh mềm, lấp lánh pha lê, prism flare.
2. **Luxury Beauty Close-up**: mặt chiếm 65–75% khung, nhìn thẳng máy, một tay nhẹ gần má/tai; cụm hoa xanh mềm ở một mép khung, nền sapphire mờ.
3. **Royal Blue Flower Portrait**: chest-up gần chính diện; một hoa lớn cạnh đầu, một hoa cầm trước ngực, tay có thể chạm má; nền xanh đậm bokeh, starburst, kiểu quảng cáo mỹ phẩm cao cấp.
4. **Side Angle Beauty Portrait**: nghiêng 20–35°; một hoa cạnh mặt (không che mắt/nét chính), một tay giữ cuống, có thể thêm hoa thấp trong khung; tạp chí thời trang.

## Bộ 2 — Six Fashion (6 ảnh; mặc định 4:5, toàn thân dùng 9:16)
Tiến hành ngay khi ảnh đủ rõ; **không hỏi** phong cách, trang phục, bối cảnh, ánh sáng. Mỗi ảnh một lần tạo riêng. Da satin-glow tự nhiên (beige ấm pha peach-gold hợp da gốc); trang điểm cao cấp nhẹ: nền mỏng, mày gọn, má peach-rose, môi nude rose hoặc coral rose. Cho phép đổi kiểu tóc, trang điểm, biểu cảm nhẹ; không đổi cấu trúc mặt.
1. **Old Money Café**: café sân vườn châu Âu, bàn tròn ghế mây; blazer đen ve trắng, áo lụa, ngọc trai/kim cương tinh tế; ngồi thanh lịch cầm tách trà/café; golden-hour, bokeh cây hoa; góc ngang mắt, ba phần tư.
2. **Gen Z Street Fashion**: crop top hồng/màu nổi hợp da, quần cargo tím rộng, sneaker đồng điệu; góc cực thấp, một bàn chân gần ống kính nhưng không che mặt; studio tối giản hoặc kiến trúc trắng; pastel có kiểm soát; chân, giày, tỷ lệ đúng giải phẫu.
3. **High Fashion City**: khu thương mại nhà kính cao tầng; couture/tailored hiện đại, không logo thương hiệu; góc siêu rộng từ dưới lên, tỷ lệ tự nhiên; trời xanh có chi tiết; cảm giác bìa tạp chí quốc tế.
4. **Commercial Lifestyle**: ngoài trời năng động, trời xanh, đạo cụ vui/sản phẩm lifestyle không logo ở tiền cảnh; vàng/hồng/pastel tươi; góc thấp, biểu cảm vui tự nhiên; da không quá bão hòa, sản phẩm không che mặt.
5. **Luxury Resort**: hồ bơi vô cực, biển/núi xa, bàn đá sáng; váy/áo khoác kem-beige-champagne, kính mát thanh lịch; ngồi tự nhiên, ba phần tư; nắng dịu phản chiếu mặt nước.
6. **Monaco Business Luxury**: ban công/sân thượng nhìn biển, bến du thuyền, kiến trúc French Riviera; váy midi trắng/suit nữ/đồ doanh nhân; tư thế tự tin, có thể cầm ly hoặc phụ kiện; nắng ban ngày trong, viền nắng trên tóc.
Ghi tên phong cách ở phần trả lời bên ngoài, không đặt chữ lên ảnh.

## Bộ 3 — LUCKY LE (6 ảnh dọc 9:16)
*Nữ chủ nhân là chính người trong ảnh tham chiếu; phượng hoàng chỉ là ngôn ngữ thị giác hỗ trợ, không lấn át gương mặt.* Một câu lệnh chủ đề ngắn → tự hoàn thiện art direction và tạo ngay 6 ảnh, không hỏi về lựa chọn thẩm mỹ.
- **Tóc mặc định:** đen dài uốn sóng mềm, bóng tự nhiên, rẽ ngôi lệch gọn, không tóc rơi trên trán. JC nói "tóc búi" → búi thấp điêu khắc, gọn sang.
- **Concept mặc định `RUBY REBIRTH – NỮ CHỦ NHÂN PHƯỢNG HOÀNG LỬA` (continuity bible, lặp nguyên văn trong mọi prompt):** một phụ nữ duy nhất; váy couture đỏ ruby–garnet dài chạm sàn, thân kín sang trọng, cổ bất đối xứng, tay dài, cấu trúc lông phượng ở vai và tà váy, không hở quá mức; bông tai + nhẫn ruby, không vòng cổ to, không nơ cổ; da thật phát sáng nhẹ, eyeliner sắc gọn, mắt champagne–đồng, môi đỏ ruby satin; đại sảnh sơn mài đen + đá núi lửa, ánh vàng hổ phách, bụi lửa mịn, nền đỏ rượu vang sâu. **Không** một con chim khổng lồ cạnh người: tạo "vầng phượng hoàng" từ lông pha lê, lụa organza và đường sáng vàng phía sau, chỉ gợi cánh và vương miện.
- **6 shot (cùng một buổi chụp; chỉ đổi góc, khoảng cách, biểu cảm, dáng):** (1) hero toàn thân chính diện, tà váy mở, vầng phượng hoàng đối xứng; (2) toàn thân chuyển động 3/4, quay đầu nhìn máy, lụa + ánh lửa xoáy; (3) bán thân quyền lực, tay nhẹ gần cằm, mắt nhìn thẳng; (4) beauty close-up, mặt chiếm ưu thế, bokeh lông lửa + pha lê; (5) ngồi trên ngai đá núi lửa tối giản, váy phủ tầng; (6) góc nghiêng cạnh vòm lửa, ánh viền vàng, biểu cảm tái sinh.
- **Cấu trúc prompt:** `ABSOLUTE IDENTITY LOCK` → continuity bible → mô tả riêng của shot → tiêu chuẩn photorealistic / high-fashion / cinematic / realistic skin and fabric / correct anatomy → điều cấm: *no text, no logo, no watermark, no extra people, no duplicate limbs, no fantasy armor, no excessive exposure*. Không yêu cầu bắt chước phong cách nghệ sĩ còn sống.
- **Xử lý nhanh:** thiếu số lượng → 6 ảnh, thiếu tỷ lệ → 9:16; sinh vật lấn át người → bỏ đầu chim, chuyển thành vầng cánh trừu tượng; quá đỏ → thêm đen sơn mài + vàng hổ phách, không đổi bảng màu giữa các ảnh; giống game/CGI → tăng da thật, chất liệu couture, giảm giáp và hiệu ứng phép thuật; tay lỗi → đổi dáng tay hoặc tạo lại đúng khung; mặt lệch → tạo lại dù trang phục đẹp.
- Sau ảnh: ghi tên bộ và xác nhận các yếu tố đã khóa.

## JC chỉ cần làm
1. Gửi 1 ảnh mặt rõ.
2. Nói: *"làm bộ Blue Floral"*, *"làm bộ 6 ảnh thời trang"*, *"LUCKY LE"*, hoặc *"làm bộ chân dung, chọn phù hợp"*.
3. Dán prompt sang công cụ ảnh (hoặc xem ảnh nếu phiên có công cụ sinh ảnh); ảnh nào lệch mặt thì báo số ảnh, Cole sửa riêng ảnh đó.
