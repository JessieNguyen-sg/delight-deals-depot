---
name: "edit-video-talking-head"
description: "Edit video người nói trước camera thành short 9:16, gộp 6 kiểu: Dạng 1 (thoại + thumbnail), Dạng 2 (hiệu ứng cao cấp), Dạng 3 (tối giản cho chuyên gia), Dạng 4 (infographic trắng), Cấp độ 1 (video dài → nhiều short khung đơn bám mặt), Cấp độ 2 (podcast 2 người → short postcard 2 ô). Gọi khi JC nói 'edit Dạng 1/2/3/4', 'cắt short Cấp độ 1/2', 'edit video talking-head'."
---

# Edit video talking-head — 1 skill, 6 kiểu

Gộp từ `dang-1-thoai-thumbnail`, `dang-2-hieu-ung-cao-cap`, `dang-3-huong-dan-toi-gian`, `dang-4-infographic-trang`, `cap-do-1-khung-don`, `cap-do-2-postcard-2-nguoi`. Phần lõi và cài đặt dùng chung viết một lần ở đây.

## Chọn kiểu (JC không nói rõ thì chọn theo bảng, không hỏi lại nhiều)
| JC muốn | Kiểu | Đầu vào | Đầu ra |
|---|---|---|---|
| Short nói chuyện nhanh, sạch, đủ dùng (mặc định) | **Dạng 1** | 1 clip ngắn, 1 người nói | `output/<tên>-dang1.mp4` |
| Video sinh động, nhiều hiệu ứng, giữ người xem | **Dạng 2** | 1 clip ngắn | `<tên>-dang2.mp4` |
| Video hướng dẫn sạch, sang, kiểu coach/chuyên gia | **Dạng 3** | 1 clip ngắn | `<tên>-dang3.mp4` |
| Xen slide infographic sáng toàn màn hình, kiểu HeyGen | **Dạng 4** | 1 clip ngắn | `<tên>-dang4.mp4` |
| Cắt video dài (bài giảng, 1 khách) thành nhiều short | **Cấp độ 1** | video dài 1 người | `<tên>-short-01.mp4`, `-02`… theo điểm giảm dần |
| Cắt podcast/phỏng vấn 2 người thành short | **Cấp độ 2** | video dài 2 người | `<tên>-short-01.mp4`… |

Dạng 1 là nền; Dạng 2/3/4 chạy Lõi rồi thêm lớp riêng. Cấp độ 1/2 chọn đoạn hay trước, rồi chạy Lõi trên từng đoạn.

## Lõi chung (mọi kiểu đều làm)
1. **Transcribe**: Whisper `word_timestamps=True`, cố định ngôn ngữ (tiếng Việt thì ghi rõ `vi`, không để auto).
2. **Cắt gọn tự nhiên**: `ffmpeg -af silencedetect=noise=-25dB:d=0.4`; chỉ cắt khoảng lặng ≥0.6s (0.4–0.6s là nhịp thở). Cắt thêm từ đệm ("ừm", "à", "kiểu như"), câu vấp/nói lại (giữ bản tốt nhất), rác đầu/cuối (đếm 1-2-3, "ok bắt đầu quay"). Luật: jump cut dứt khoát; cắt tại hết ý; 2 điểm cắt cách nhau <0.4s thì gộp; chừa ≥0.15s đệm; không cắt quá 40% thời lượng gốc/lần. **Cắt xong MỚI transcribe lại**; mọi mốc caption/thumbnail lấy từ transcript sau cắt.
3. **Thumbnail mở đầu** (~2–3s đầu): chọn 1 trong 6 bố cục theo tông: `stack_hierarchy` (bán hàng/tuyên bố mạnh), `magazine` (series/tập), `serif_mix` (câu hỏi/chia sẻ), `lifestyle` (vlog đời thường), `brand_word` (1 từ thương hiệu lớn), `spaced_caps` (studio/agency). `title` 4–9 từ, viết lại cho tò mò, không copy câu chào; `accent` = 1 cụm nằm nguyên văn trong title, tô màu nhấn. *(Dạng 3 bỏ thumbnail nhiều tầng.)*
4. **Caption động**: chữ trắng dày, 1–3 từ/cụm, khớp word-timestamp, nằm dưới 1/3 khung, không che mặt.
5. **Dựng bằng `hyperframes`** (track video + thumbnail + caption, seek-safe). Xuất 9:16, 1080×1920, giữ audio gốc.

## Lớp riêng từng kiểu

### Dạng 2 — 7 trụ cột
1. Zoom theo cảm xúc giọng (punch-in 4–8%, ease mượt, zoom out khi hết nhấn). 1b. Cắt đoạn "lấy đà" đầu (đếm số, nói nháp); không có thì giữ nguyên hook.
2. Overlay hoạt hoạ minh hoạ (bước hiện dần, đường nối chạy), đa dạng kiểu, đặt dưới cằm (~+6%), tuyệt đối không che mặt.
3. SFX khớp từng hiệu ứng lớn (whoosh/pop/tick), tinh tế.
4. Từ khoá 2 màu, to hơn caption, dưới vùng mặt; **tạm ngưng caption khi hiệu ứng lớn đang chạy**.
5. Lớp phủ biến cảnh thành B-roll (đoạn liệt kê/số liệu).
6. Crop bám mặt tròn/vuông khi overlay lớn; cắt RỘNG (đầu + mặt + tới ngực); ≤1 lần/video, giữa video, ~5–6s.
7. So sánh `before_after` / `vs` / `side_by_side`, đặt gần cuối (né trùng crop giữa video).
Nguyên tắc: hiệu ứng lớn cách nhau ≥6s, tổng ≤~40% video; nội dung mỗi hiệu ứng lấy từ đúng đoạn nói lúc đó; đổi kiểu giữa các lần. Cần thêm: face-detect, SFX .wav, icon Lucide, ảnh nền free-license.

### Dạng 3 — Tối giản (5 trụ cột)
1. Tiêu đề trắng lớn ~2 dòng trên khung (hiện suốt video, hoặc 4–5s đầu), dòng CTA phụ trong ngoặc, nhỏ và mờ; tùy chọn ⬇️⬇️⬇️.
2. Các Bước: tự chia ý theo nội dung thật (không ép "Step 1/2/3" nếu không phải quy trình), chữ trắng reveal theo lời, tô màu thương hiệu tối đa 1 từ/bước.
3. CTA chèn như một phần nội dung (dòng ngoặc dưới tiêu đề hoặc câu khuyên cuối video).
4. **Nhạc dẫn dắt (quan trọng nhất)**: không lời → nhạc to (~0.7–0.85); có lời → duck còn ~0.12–0.2 (ffmpeg `volume`/sidechain). Tự nhận có lời/không lời từ transcript.
5. Zoom cực nhẹ, chỉ ở điểm chuyển ý.
Không có: overlay dày, progress hoạt hoạ, so sánh, crop mặt, SFX, thumbnail nhiều tầng. Vẫn cắt gọn khoảng lặng. Cần: nhạc free-license (Pixabay Music), font trắng lớn, câu CTA của JC.

### Dạng 4 — Infographic trắng
- Lớp phủ toàn màn hình, nền sáng/trắng, **xen kẽ** talking-head. Khối: tiêu đề hero · VS so sánh · sơ đồ bước/flow (node icon + mũi tên) · danh sách · số liệu · quote. Mỗi lần một kiểu, **không lặp mẫu trong 1 video** (bắt buộc).
- **Không vẽ HTML có CSS `@keyframes`** (lệch khung khi render seek từng frame). AI viết **spec có cấu trúc** (kiểu khối, bố cục, nội dung, màu, thứ tự reveal) rồi composition `hyperframes` với `data-*` timing vẽ + chạy animation.
- Zoom cảm xúc mạnh hơn Dạng 3; SFX whoosh/pop/typing; **không dùng từ khoá 2 màu** (điểm nhấn nằm ở infographic); B-roll trám khi cần; 1 preset màu pro mặc định bằng ffmpeg (`eq`, `unsharp`, `hqdn3d`) — nói thật: 1080p không thành 4K thật.
- Màu mặc định đỏ + navy nếu JC chưa đưa 2 màu thương hiệu.

### Cấp độ 1 — Video dài → nhiều short, khung đơn bám mặt
1. Transcribe toàn video. 2. Chia cửa sổ ứng viên theo độ dài (<30s / 30–60s / 60–90s / tự chọn); chấm điểm: mật độ ý đắt, câu chốt, cấu trúc mở–thân–kết trọn vẹn; chọn N đoạn không chồng lấn (mặc định ước 5–8 đoạn). JC mô tả đoạn muốn ("đoạn nói về giá") → so khớp ngữ nghĩa ưu tiên.
3. Crop bám mặt (mediapipe/OpenCV): tâm crop pan mượt theo mặt, không cắt đầu; nhiều người → ưu tiên người đang nói (chuyển động môi/âm lượng).
4. Chạy Lõi trên từng đoạn (transcribe lại sau cắt). 5. Xuất từng file, đặt tên theo điểm giảm dần.

### Cấp độ 2 — Podcast 2 người → postcard 2 ô
Làm như Cấp độ 1 bước 1–2, rồi:
- **Diarization** (ai nói khi nào): mặc định heuristic (biên độ âm thanh khớp chuyển động môi từng mặt), đủ khi 2 người ngồi cố định, rõ mặt. Chính xác hơn: `pyannote.audio` (cần tài khoản HuggingFace miễn phí + token do JC tự làm một lần; chỉ đề xuất khi heuristic chưa đủ).
- Gom câu liên tiếp cùng người thành "cụm". **Cụm 1 người nói dài → 1 khung lớn. Hai người qua lại nhanh → 2 ô trên/dưới.** Chuyển 1↔2 khung snap theo điểm chuyển câu (không cắt giữa câu), crossfade ngắn hoặc scale nhẹ. Mỗi ô crop bám mặt. Caption nằm vùng giữa 2 ô khi đang 2 khung.
- `hyperframes` dựng 2 track video (1/người), ẩn/hiện theo cụm bằng `data-*` timing.

## Cài đặt môi trường (1 lần cho máy này)
Tự kiểm tra trước, đừng hỏi JC nếu tự làm được; chỉ dừng khi bước cần quyền hệ thống mà môi trường chặn.
```bash
ffmpeg -version
python --version || python3 --version
node --version
```
1. **ffmpeg**: Windows `winget install Gyan.FFmpeg` · macOS `brew install ffmpeg` · Linux `sudo apt install ffmpeg`.
2. **Python 3.10+**: `python -m venv .venv`, kích hoạt, rồi `pip install faster-whisper librosa numpy opencv-python mediapipe`. Không có GPU: dùng Whisper `small`/`medium`.
3. **Node.js LTS (≥18) + skill `hyperframes`**: gọi `hyperframes` lần đầu, rồi chạy `hyperframes doctor` để nó cài nốt phần thiếu.
4. Thư mục: `input/` (video của JC), `output/` (thành phẩm), `assets/{sfx,music,fonts,icons,luts}/`.
5. Chạy thử `python -c "import faster_whisper, librosa, cv2, mediapipe; print('OK')"` + `ffmpeg -version` + `node --version` đều không lỗi mới bắt đầu dựng.

## Tài nguyên: tự lấy trước, chỉ hỏi JC khi không có nguồn free hợp lệ
- **Font**: Google Fonts (ưu tiên Be Vietnam Pro / Inter, có dấu tiếng Việt; font lỗi dấu thì đổi).
- **Icon**: Lucide (MIT) qua `https://unpkg.com/lucide-static/icons/<tên>.svg`.
- **SFX / nhạc không lời**: Pixabay hoặc Mixkit, chỉ lấy khi ghi rõ free for commercial use.
- **Ảnh/B-roll nền**: Pexels/Unsplash, chọn ảnh free-license thương mại.
- **Nhạc TREND** (đang hot TikTok/Reels): KHÔNG tự tải (nhạc có bản quyền). JC tự đưa file, hoặc Cole gợi ý nhạc free-license thay thế.
- **LUT/bộ lọc màu**: dựng bằng ffmpeg `eq`/`curves`/`colorbalance`; chỉ cần file `.cube` khi JC đưa sẵn.

## JC chỉ cần làm
1. Bỏ video vào `input/` (+ màu thương hiệu / câu CTA / nhạc riêng nếu có).
2. Nói một câu, ví dụ: *"edit Dạng 1 cho video này"*, *"edit Dạng 3, CTA: inbox mình nhận tư vấn"*, *"cắt video này thành short, Cấp độ 1, ưu tiên đoạn nói về giá"*.
3. Xem file trong `output/`, nói chỗ cần sửa.

Cole tự làm: kiểm tra môi trường → tải tài nguyên thiếu → chạy Lõi → thêm lớp riêng → xuất → báo đường dẫn file. Xem kỹ thuật đăng sau đó ở `ut-chi-seo-video` (YouTube) hoặc `reel-facebook-viral` (Facebook); caption/hashtag ở `chi-tu-viet-bai`.
