---
name: "reel-facebook-viral"
description: "Xây kênh Facebook tự động: phân tích kênh mẫu, dựng Reel dọc 9:16 đều đặn từ kho tư liệu, rồi đăng hoặc lên lịch qua Meta Business Suite sau khi khách duyệt."
---

# Xây kênh Facebook tự động — dựng Reel và hẹn lịch đăng đều đặn

## Skill này làm gì
Hệ thống sản xuất Reel Facebook dùng lại được cho BẤT KỲ thương hiệu nào:
phân tích kênh mẫu để học cấu trúc → lập kho tư liệu (video gốc, nhạc, logo) →
dựng Reel dọc 9:16 có chữ cố định + nhạc nền + logo đúng ngữ cảnh → kiểm tra
xem trước → mở Facebook/Meta Business Suite, tải Reel lên, điền caption, chọn
giờ đăng — và **dừng lại xin khách duyệt lần cuối trước khi bấm Đăng/Lên lịch**.

**Yêu cầu**: AI chạy được lệnh trên máy (Claude Code/Codex) để dựng bằng ffmpeg
+ Python; phần đăng Reel cần thêm quyền điều khiển trình duyệt. Mọi danh tính,
nội dung, tư liệu, thông tin đăng nhập của khách nằm NGOÀI skill này.

## Nguyên tắc cốt lõi
1. Lệnh mới nhất của khách là thẩm quyền cao nhất.
2. **Không sao chép** tuyên bố, danh tính, tư liệu riêng hay giọng của kênh mẫu.
   Chỉ học cấu trúc.
3. **Không đọc/lưu mật khẩu, cookie, mã OTP, token, thông tin thanh toán.**
   Cần đăng nhập thì mở trang đăng nhập cho khách tự nhập.
4. Chuẩn bị đủ Reel + caption + trang đích + lịch trước, rồi mới xin duyệt.
5. **Phải có duyệt rõ ràng của khách ngay trước khi bấm Đăng/Lên lịch.** Không
   bật boost, quảng cáo hay tuỳ chọn trả phí.
6. Khi `content_mode` là `verbatim`: giữ nguyên từng chữ của nội dung đã duyệt,
   chỉ được đổi chỗ xuống dòng.
7. Không sửa video gốc. Mọi đầu ra và sổ ghi chép nằm trong thư mục làm việc.

## Định tuyến yêu cầu
- Lần đầu / khách đưa kênh mẫu → **Thiết lập thương hiệu**.
- "Làm video tiếp theo" → **Làm Reel tiếp theo**.
- Sửa → chỉ đổi đúng phần được yêu cầu, dựng lại, kiểm tra lại.
- Đăng/lên lịch → **Đăng qua trình duyệt**.
- "Mở thư mục video" → mở thư mục làm việc/thư mục con được yêu cầu.

## Chuẩn bị công cụ (làm 1 lần)
1. Kiểm tra `ffmpeg -version`, `ffprobe -version`, `python --version` (cần
   Python 3.10+). Thiếu thì cài (Windows: `winget install Gyan.FFmpeg`; Mac:
   `brew install ffmpeg`).
2. Tạo thư mục `reel-tools/` gồm `scripts/` và `assets/`, rồi ghi 5 tệp ở mục
   "Mã nguồn" cuối bài vào đúng chỗ:
   `reel-tools/scripts/setup_workspace.py`, `select_media.py`,
   `render_reel.py`, `validate_output.py` và `reel-tools/assets/default-config.json`.
   (`setup_workspace.py` tự đọc `../assets/default-config.json` nên phải đúng cấu trúc.)
3. Chỉ dùng cờ `--open` của `setup_workspace.py` trên Windows (nó gọi
   `os.startfile`); Mac/Linux thì bỏ cờ đó và tự mở thư mục bằng `open`/`xdg-open`.

## Thiết lập thương hiệu (lần đầu)
1. Chỉ hỏi những thứ thiếu và không suy ra được: link kênh mẫu, trang đích
   (fanpage sẽ đăng), nơi đặt thư mục làm việc, khách tự cung cấp video/nhạc/logo không.
2. Có công cụ trình duyệt thì mở kênh mẫu; chỉ nhờ khách đăng nhập khi bị chặn.
   Không bao giờ nhờ khách dán mật khẩu vào khung chat.
3. Thu thập ví dụ quan sát được + số liệu hiển thị. Tách **sự kiện nhìn thấy**
   khỏi **suy luận**. Không khẳng định "viral" nếu không có bằng chứng tương tác.
4. Rút ra mẫu dùng lại: chủ đề, kiểu mở đầu (hook), cấu trúc, mật độ chữ, thứ
   bậc hình ảnh, độ dài caption, cách kết, nhịp đăng. Không bắt chước câu chữ đặc trưng.
5. Tạo thư mục làm việc:
   `python reel-tools/scripts/setup_workspace.py --root <thư-mục> --brand-name <tên> --reference-url <url> --destination-url <url>`
6. Ghi các thiết lập đã xác nhận vào `BRAND_CONFIG.json`. Giá trị chưa chắc để
   `null`, chỉ hỏi khi thật sự chặn việc sản xuất.
7. Mở `01_VIDEO_GOC`, `02_NHAC_NEN`, `03_LOGO` để khách bỏ tư liệu vào; có đủ
   tư liệu thì tự làm tiếp.

### Cách phân tích kênh mẫu
Chỉ phân tích nội dung khách được phép xem. Mỗi bài ghi: URL/mã bài, ngày và
loại bài, toàn văn hiển thị được, số reaction/bình luận/chia sẻ/lượt xem nếu
thấy, chủ đề + vấn đề của khán giả + kiểu hook, công thức (so sánh, tổng hợp
danh sách, hướng dẫn, AIDA, lỗi thường gặp, trước/sau, quan điểm), cách kết,
định dạng hình ảnh, mật độ chữ.

Xếp hạng ứng viên: nếu có số người theo dõi/tiếp cận thì chuẩn hoá theo mức nền
của kênh; không thì dùng công thức minh bạch và giữ số liệu gốc:
`score = reactions + 2*comments + 3*shares + 0.02*views`
Đây chỉ là công cụ chọn lọc, không chứng minh nhân quả. Ưu tiên bài "xanh" (đứng
được một mình) làm được bản hình ảnh ngắn. Loại bài riêng tư, nhạy cảm, đi
chép, đang tranh cãi hay phụ thuộc ngữ cảnh. Lưu kết quả vào
`08_PHAN_TICH_KENH/reference_analysis.json`, ứng viên vào `04_NOI_DUNG`.

## Làm Reel tiếp theo
1. Đọc `BRAND_CONFIG.json`, `07_NHAT_KY/media_usage.csv`,
   `07_NHAT_KY/publishing_schedule.csv`.
2. Chọn tư liệu chưa dùng: `python reel-tools/scripts/select_media.py --workspace <thư-mục> --kind video`
   (lặp lại với `music`, `logo` khi cần). Bỏ mọi mục bị đánh dấu `blocked`.
3. Soạn tệp JSON nội dung (xem mẫu bên dưới). Dùng `verbatim` cho văn bản đã
   duyệt; chỉ dùng `adapted` khi khách cho phép viết lại.
4. Dựng: `python reel-tools/scripts/render_reel.py --workspace <thư-mục> --content <content.json>`
5. Kiểm tra kỹ thuật: `python reel-tools/scripts/validate_output.py --video <output.mp4> --duration <giây>`
6. **Tự xem ảnh xem trước tại nhiều mốc thời gian** (đặc biệt khi chủ thể
   chuyển động) theo bộ kiểm tra hình ảnh bên dưới.
7. Chữ tràn, logo che chủ thể, tương phản yếu, khoảng cách không đều → tự chỉnh
   và dựng lại, đừng bắt khách chẩn đoán lỗi kỹ thuật.
8. Trình bày video + caption để khách xem. **Chưa đăng.**
9. Chỉ cập nhật sổ sử dụng tư liệu SAU KHI dựng thành công; lần dựng lỗi không
   bao giờ được đánh dấu "đã dùng".

## Mặc định của video
- H.264/AAC MP4, 1080×1920, 30fps, `yuv420p`, có fast-start.
- Mặc định 20 giây, footage chạy 0.5×, nền tối đi và hơi mờ, âm thanh fade-out ngắn.
- Chữ đã duyệt hiện thành MỘT khối cố định suốt video khi `show_full_text` bật.
- Chữ hoa/thường tự nhiên, màu trắng, nhấn vàng-chanh mờ không hào quang/viền (trừ khi cấu hình khác).
- Chỉ đặt logo khi có thêm ngữ cảnh. Giữ tỉ lệ, đặt ở vùng trống đã kiểm tra, thẳng
  trục với khối nội dung; không bao giờ che mặt, mắt, tay, vật chính hay chữ.
- Xoay vòng hết tư liệu chưa dùng rồi mới dùng lại; không dùng cùng một nguồn cho hai video liền nhau.

### Cấu hình mặc định (`assets/default-config.json`)
Các khoá quan trọng: `content_mode` (verbatim/adapted), `video_duration_seconds`,
`footage_speed`, `highlight_color`, `background_brightness`, `music_volume`,
`direct_cta` (false = không kêu gọi trực tiếp), `hashtags`, `posting_times`,
`max_posts_per_day`, `timezone`, `require_final_publish_approval` (luôn true).

## Nội dung và caption

**Verbatim**: giữ từng từ, dấu câu, kiểu viết hoa, thứ tự của nguồn đã duyệt;
chỉ đổi chỗ xuống dòng. Không âm thầm rút gọn cho vừa khung — quá dày thì giảm cỡ
chữ trong giới hạn đọc được, chỉnh giãn dòng, hoặc hỏi khách có muốn bản rút gọn không.

**Adapted**: chỉ viết lại khi được phép. Giữ đúng nghĩa và sự thật; không thêm
trải nghiệm cá nhân, kết quả, doanh thu, bằng cấp hay lời chứng thực khách không cung cấp.

**Bản nháp mới**: chọn công thức có cơ sở từ phân tích kênh (so sánh, tổng hợp,
hướng dẫn, AIDA, lỗi thường gặp, trước/sau, quan điểm có lý lẽ). Có tuyên bố mới
hoặc giọng thương hiệu mới thì đưa khách xem bản nháp TRƯỚC khi dựng.

**Mẫu JSON nội dung**:
```json
{
  "id": "CONTENT_001",
  "mode": "verbatim",
  "title": "Tiêu đề đã duyệt",
  "body": "Nội dung đã duyệt",
  "highlights": ["cụm quan trọng"],
  "caption": "Caption đầy đủ cho nền tảng",
  "video_file": null,
  "music_file": null,
  "logo_file": null,
  "logo_y": 280,
  "font_name": "Arial",
  "title_font_size": 70,
  "body_font_size": 45
}
```
Đường dẫn nên tính từ thư mục làm việc. Font phải có dấu tiếng Việt.

**Caption**: viết caption hoàn chỉnh, khác với thứ bậc chữ trên hình. Mở bằng
kết quả, mâu thuẫn hoặc điều phát hiện. Thêm ngữ cảnh/ví dụ/bước hữu ích. Kết
bằng một nhận xét mở hoặc câu hỏi tự nhiên khi CTA trực tiếp đang tắt. Tôn trọng
cấu hình hashtag/CTA. Không khẳng định "viral", hiệu quả sản phẩm hay đã dùng thật nếu không có bằng chứng.

## Kiểm tra chất lượng hình ảnh

**Chữ**: lề ngang ≥7%; giữ chữ hoa/thường và dấu tiếng Việt; tiêu đề lớn hơn rõ
so với chữ phụ; giãn dòng gọn mà dễ thở, không khoảng trống vô cớ; nhấn màu mờ
không hào quang; khối chữ nằm trong vùng an toàn giữa khung.

**Logo**: giữ tỉ lệ và độ trong suốt; bắt đầu khoảng 7-10% bề rộng khung; thẳng
trục với khối nội dung; ưu tiên vùng trống ổn định suốt clip; không chồng lên
mặt/mắt/tay/sản phẩm/tiêu đề/chữ. Xem tại 25%, 50%, 75% thời lượng; không có vùng an toàn
ổn định thì dời hoặc bỏ logo.

**Danh sách xem trước**: đúng 9:16 và thời lượng; chữ khớp nguồn đã duyệt;
không dòng bị cắt/tràn; đọc được ở cỡ điện thoại; nền còn nhận ra nhưng dịu;
logo liên quan, cân đối, không phô; có âm thanh, cân bằng, fade sạch; không khung
đen, cuối video đứng hình, âm thanh gốc lọt vào ngoài ý muốn, hay trùng
footage liền kề. Lỗi nào thì sửa và dựng lại TRƯỚC khi trình khách.

## Đăng qua trình duyệt
1. Ưu tiên kết nối/API chính thức nếu có và được phép; không thì dùng công cụ
   trình duyệt (chỉ dùng điều khiển máy tính cho phần giao diện máy trình duyệt không thao tác được).
2. Mở trang đích hoặc Meta Business Suite.
3. Trình duyệt chưa kết nối → hướng dẫn khách kết nối. Facebook đòi đăng nhập →
   mở trang đăng nhập và nhờ khách tự đăng nhập tại đó; **không bao giờ xử lý thông tin đăng nhập**.
4. Xác nhận đúng trang bằng tên hiển thị + URL trang đích.
5. Mở trình soạn Reel (Thước phim), tải MP4 đã duyệt, chèn caption đã duyệt, kiểm
   tra bài vẫn là Reel; giữ quảng cáo/boost/tuỳ chọn trả phí TẮT.
6. Chọn giờ: đọc giờ đã cấu hình, giới hạn mỗi ngày, múi giờ và sổ lịch đăng. Nếu
   có lịch thật trên nền tảng thì lấy đó làm chuẩn. Dùng ô trống tương lai sớm
   nhất theo giờ cấu hình; ngày đầy thì sang ngày kế. **Không bao giờ hẹn 2 bài
   cùng một thời điểm cho cùng một trang.**
7. **Dừng lại và tóm tắt cụ thể**: tên trang, tên tệp video, phần mở đầu caption,
   ngày, giờ, múi giờ, chế độ (đăng ngay/hẹn). Xin duyệt rõ ràng ("Duyệt", "Đăng",
   "Lên lịch"). Lời duyệt cũ cho video khác KHÔNG có giá trị cho video này.
8. Sau khi được duyệt mới bấm Đăng/Lên lịch, kiểm tra xác nhận hoặc mục đã hẹn,
   rồi ghi thêm 1 dòng vào `07_NHAT_KY/publishing_schedule.csv`. Không xác minh
   được thành công thì báo rõ sự không chắc chắn và **không tự tạo lần đăng trùng**.
9. Có cảnh báo bản quyền/xử lý/tải lên → giữ nguyên bản nháp, báo đúng cảnh báo,
   chỉ thay tư liệu khi được phép.

## Xử lý lỗi
- Thiếu FFmpeg/FFprobe → báo phụ thuộc thiếu và cách chỉnh PATH cụ thể.
- Thiếu video hoặc nhạc → mở đúng thư mục và nói rõ cần gì.
- Giao diện nền tảng đổi → đọc giao diện hiện tại, đừng dùng toạ độ nhớ sẵn.
- Không kết nối được trình duyệt → chỉ cách bật điều khiển máy tính/kết nối
  trình duyệt được hỗ trợ; làm xong mọi thứ cục bộ trước.
- Giữ bản nháp và nhật ký có thể phục hồi. **Không bao giờ xoá tư liệu của khách để sửa lỗi.**

## Mã nguồn công cụ (ghi nguyên văn vào reel-tools/)

### reel-tools/assets/default-config.json
```json
{
  "brand_name": null,
  "reference_channel_url": null,
  "destination_page_url": null,
  "platform": "Facebook Reels",
  "language": "vi",
  "content_mode": "verbatim",
  "video_duration_seconds": 20,
  "footage_speed": 0.5,
  "output_width": 1080,
  "output_height": 1920,
  "fps": 30,
  "show_full_text": true,
  "primary_text_color": "#FFFFFF",
  "highlight_color": "#DFFF00",
  "background_brightness": -0.24,
  "background_blur_sigma": 0.8,
  "music_volume": 0.42,
  "direct_cta": false,
  "hashtags": false,
  "posting_times": ["09:00", "20:00"],
  "max_posts_per_day": 2,
  "timezone": "local",
  "require_final_publish_approval": true
}

```

### reel-tools/scripts/setup_workspace.py
```python
import argparse
import csv
import json
import os
import shutil
from pathlib import Path


FOLDERS = [
    "01_VIDEO_GOC", "02_NHAC_NEN", "03_LOGO", "04_NOI_DUNG",
    "05_VIDEO_DA_XU_LY", "06_ANH_XEM_TRUOC", "07_NHAT_KY",
    "08_PHAN_TICH_KENH"
]


def main():
    parser = argparse.ArgumentParser(description="Initialize a portable Reel workspace")
    parser.add_argument("--root", required=True)
    parser.add_argument("--brand-name", required=True)
    parser.add_argument("--reference-url")
    parser.add_argument("--destination-url")
    parser.add_argument("--open", action="store_true", dest="open_folder")
    args = parser.parse_args()

    root = Path(args.root).expanduser().resolve()
    root.mkdir(parents=True, exist_ok=True)
    for folder in FOLDERS:
        (root / folder).mkdir(exist_ok=True)

    default_path = Path(__file__).resolve().parent.parent / "assets" / "default-config.json"
    config = json.loads(default_path.read_text(encoding="utf-8"))
    config.update({
        "brand_name": args.brand_name,
        "reference_channel_url": args.reference_url,
        "destination_page_url": args.destination_url,
    })
    (root / "BRAND_CONFIG.json").write_text(
        json.dumps(config, ensure_ascii=False, indent=2), encoding="utf-8"
    )

    ledgers = {
        "media_usage.csv": ["kind", "file", "status", "use_count", "last_content", "last_used"],
        "publishing_schedule.csv": ["content_id", "page", "video", "date", "time", "timezone", "status", "platform_id"],
    }
    for name, header in ledgers.items():
        path = root / "07_NHAT_KY" / name
        if not path.exists():
            with path.open("w", newline="", encoding="utf-8-sig") as f:
                csv.writer(f).writerow(header)

    analysis = root / "08_PHAN_TICH_KENH" / "reference_analysis.json"
    if not analysis.exists():
        analysis.write_text(json.dumps({"channel": args.reference_url, "facts": [], "inferences": [], "posts": []}, ensure_ascii=False, indent=2), encoding="utf-8")

    if args.open_folder:
        os.startfile(root)
    print(json.dumps({"workspace": str(root), "config": str(root / "BRAND_CONFIG.json")}, ensure_ascii=False))


if __name__ == "__main__":
    main()

```

### reel-tools/scripts/select_media.py
```python
import argparse
import csv
import json
from pathlib import Path


KINDS = {
    "video": ("01_VIDEO_GOC", {".mp4", ".mov", ".mkv", ".webm", ".avi"}),
    "music": ("02_NHAC_NEN", {".mp3", ".wav", ".m4a", ".aac", ".flac"}),
    "logo": ("03_LOGO", {".png", ".webp", ".jpg", ".jpeg"}),
}


def read_usage(path):
    result = {}
    if not path.exists():
        return result
    with path.open("r", newline="", encoding="utf-8-sig") as f:
        for row in csv.DictReader(f):
            result[(row.get("kind", ""), row.get("file", ""))] = row
    return result


def main():
    parser = argparse.ArgumentParser(description="Select least-used eligible media")
    parser.add_argument("--workspace", required=True)
    parser.add_argument("--kind", required=True, choices=KINDS)
    parser.add_argument("--exclude")
    args = parser.parse_args()

    root = Path(args.workspace).expanduser().resolve()
    folder, extensions = KINDS[args.kind]
    assets = sorted(p for p in (root / folder).iterdir() if p.is_file() and p.suffix.lower() in extensions)
    usage = read_usage(root / "07_NHAT_KY" / "media_usage.csv")
    eligible = []
    for path in assets:
        rel = path.relative_to(root).as_posix()
        row = usage.get((args.kind, rel), {})
        if row.get("status") == "blocked" or rel == args.exclude:
            continue
        eligible.append((int(row.get("use_count") or 0), row.get("last_used") or "", rel, path))
    if not eligible:
        raise SystemExit(f"No eligible {args.kind} found in {root / folder}")
    eligible.sort(key=lambda x: (x[0], x[1], x[2].lower()))
    count, last_used, rel, path = eligible[0]
    print(json.dumps({"kind": args.kind, "file": rel, "absolute_path": str(path), "use_count": count, "last_used": last_used}, ensure_ascii=False))


if __name__ == "__main__":
    main()

```

### reel-tools/scripts/render_reel.py
```python
import argparse
import csv
import datetime as dt
import json
import re
import shutil
import subprocess
import textwrap
from pathlib import Path


def ass_color(hex_color):
    value = hex_color.lstrip("#")
    if len(value) != 6:
        raise ValueError(f"Invalid color: {hex_color}")
    r, g, b = value[0:2], value[2:4], value[4:6]
    return f"&H00{b}{g}{r}"


def ass_escape(value):
    return value.replace("\\", "\\\\").replace("{", "\\{").replace("}", "\\}")


def wrap_text(value, width):
    lines = []
    for paragraph in value.splitlines() or [""]:
        wrapped = textwrap.wrap(paragraph, width=width, break_long_words=False, break_on_hyphens=False) or [""]
        lines.extend(wrapped)
    return "\\N".join(ass_escape(line) for line in lines)


def highlight(text, phrases, color):
    for phrase in sorted((p for p in phrases if p), key=len, reverse=True):
        escaped = ass_escape(phrase)
        text = re.sub(re.escape(escaped), lambda m: "{\\c" + color + "}" + m.group(0) + "{\\c&H00FFFFFF}", text, flags=re.IGNORECASE)
    return text


def resolve(root, value, folder, extensions):
    if value:
        p = Path(value)
        p = p if p.is_absolute() else root / p
        if not p.exists():
            raise FileNotFoundError(p)
        return p.resolve()
    choices = sorted(p for p in (root / folder).iterdir() if p.is_file() and p.suffix.lower() in extensions)
    if not choices:
        raise FileNotFoundError(f"No media in {root / folder}")
    return choices[0].resolve()


def log_usage(root, kind, path, content_id):
    ledger = root / "07_NHAT_KY" / "media_usage.csv"
    rows = []
    if ledger.exists():
        with ledger.open("r", newline="", encoding="utf-8-sig") as f:
            rows = list(csv.DictReader(f))
    rel = path.relative_to(root).as_posix() if path.is_relative_to(root) else str(path)
    found = False
    for row in rows:
        if row.get("kind") == kind and row.get("file") == rel:
            row.update(status="used", use_count=str(int(row.get("use_count") or 0) + 1), last_content=content_id, last_used=dt.date.today().isoformat())
            found = True
    if not found:
        rows.append({"kind": kind, "file": rel, "status": "used", "use_count": "1", "last_content": content_id, "last_used": dt.date.today().isoformat()})
    with ledger.open("w", newline="", encoding="utf-8-sig") as f:
        writer = csv.DictWriter(f, fieldnames=["kind", "file", "status", "use_count", "last_content", "last_used"])
        writer.writeheader(); writer.writerows(rows)


def main():
    parser = argparse.ArgumentParser(description="Render a fixed-text vertical Reel with FFmpeg")
    parser.add_argument("--workspace", required=True)
    parser.add_argument("--content", required=True)
    args = parser.parse_args()

    if not shutil.which("ffmpeg") or not shutil.which("ffprobe"):
        raise SystemExit("FFmpeg and FFprobe must be available on PATH")
    root = Path(args.workspace).expanduser().resolve()
    config = json.loads((root / "BRAND_CONFIG.json").read_text(encoding="utf-8"))
    content_path = Path(args.content).expanduser().resolve()
    content = json.loads(content_path.read_text(encoding="utf-8"))
    video = resolve(root, content.get("video_file"), "01_VIDEO_GOC", {".mp4", ".mov", ".mkv", ".webm", ".avi"})
    music = resolve(root, content.get("music_file"), "02_NHAC_NEN", {".mp3", ".wav", ".m4a", ".aac", ".flac"})
    logo = resolve(root, content.get("logo_file"), "03_LOGO", {".png", ".webp", ".jpg", ".jpeg"}) if content.get("logo_file") else None
    duration = float(config.get("video_duration_seconds", 20))
    speed = float(config.get("footage_speed", 0.5))
    width, height = int(config.get("output_width", 1080)), int(config.get("output_height", 1920))
    fps = int(config.get("fps", 30))
    output_dir = root / "05_VIDEO_DA_XU_LY"; output_dir.mkdir(exist_ok=True)
    preview_dir = root / "06_ANH_XEM_TRUOC"; preview_dir.mkdir(exist_ok=True)
    content_id = re.sub(r"[^A-Za-z0-9_-]+", "_", content.get("id") or content_path.stem)
    output = output_dir / f"{content_id}.mp4"
    ass_file = output_dir / f"{content_id}.ass"

    title = wrap_text(content.get("title", ""), 25)
    body = wrap_text(content.get("body", ""), 38)
    hi_color = ass_color(config.get("highlight_color", "#DFFF00"))
    title = highlight(title, content.get("highlights", []), hi_color)
    body = highlight(body, content.get("highlights", []), hi_color)
    font = content.get("font_name", "Arial")
    title_size = int(content.get("title_font_size", 70)); body_size = int(content.get("body_font_size", 45))
    ass = f"""[Script Info]
ScriptType: v4.00+
PlayResX: {width}
PlayResY: {height}
WrapStyle: 2
ScaledBorderAndShadow: yes

[V4+ Styles]
Format: Name,Fontname,Fontsize,PrimaryColour,SecondaryColour,OutlineColour,BackColour,Bold,Italic,Underline,StrikeOut,ScaleX,ScaleY,Spacing,Angle,BorderStyle,Outline,Shadow,Alignment,MarginL,MarginR,MarginV,Encoding
Style: Title,{font},{title_size},&H00FFFFFF,&H00FFFFFF,&H00000000,&H00000000,-1,0,0,0,100,100,0,0,1,0,0,8,76,76,650,1
Style: Body,{font},{body_size},&H00FFFFFF,&H00FFFFFF,&H00000000,&H00000000,0,0,0,0,100,100,0,0,1,0,0,8,90,90,930,1

[Events]
Format: Layer,Start,End,Style,Name,MarginL,MarginR,MarginV,Effect,Text
Dialogue: 0,0:00:00.00,0:59:59.00,Title,,0,0,0,,{title}
Dialogue: 0,0:00:00.00,0:59:59.00,Body,,0,0,0,,{body}
"""
    ass_file.write_text(ass, encoding="utf-8-sig")

    dark = float(config.get("background_brightness", -0.24)); blur = float(config.get("background_blur_sigma", 0.8))
    filters = [f"[0:v]setpts=PTS/{speed},scale={width}:{height}:force_original_aspect_ratio=increase,crop={width}:{height},gblur=sigma={blur},eq=brightness={dark}:contrast=1.02[base]"]
    inputs = ["-stream_loop", "-1", "-i", str(video), "-stream_loop", "-1", "-i", str(music)]
    if logo:
        inputs += ["-loop", "1", "-i", str(logo)]
        logo_y = int(content.get("logo_y", 280))
        filters += ["[2:v]scale=96:96:force_original_aspect_ratio=decrease[logo]", f"[base][logo]overlay=(W-w)/2:{logo_y}[branded]", f"[branded]ass={ass_file.name}[v]"]
    else:
        filters += [f"[base]ass={ass_file.name}[v]"]
    fade_start = max(0, duration - 1)
    filters += [f"[1:a]volume={float(config.get('music_volume', 0.42))},afade=t=out:st={fade_start}:d=1[a]"]
    command = ["ffmpeg", "-y", *inputs, "-filter_complex", ";".join(filters), "-map", "[v]", "-map", "[a]", "-t", str(duration), "-r", str(fps), "-c:v", "libx264", "-preset", "medium", "-crf", "18", "-pix_fmt", "yuv420p", "-c:a", "aac", "-b:a", "192k", "-movflags", "+faststart", str(output)]
    subprocess.run(command, cwd=output_dir, check=True)
    for frac, suffix in [(0.25, "25"), (0.5, "50"), (0.75, "75")]:
        preview = preview_dir / f"{content_id}_{suffix}.png"
        subprocess.run(["ffmpeg", "-y", "-ss", str(duration * frac), "-i", str(output), "-frames:v", "1", str(preview)], check=True, stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
    log_usage(root, "video", video, content_id); log_usage(root, "music", music, content_id)
    if logo: log_usage(root, "logo", logo, content_id)
    print(json.dumps({"video": str(output), "previews": str(preview_dir), "content_id": content_id}, ensure_ascii=False))


if __name__ == "__main__":
    main()

```

### reel-tools/scripts/validate_output.py
```python
import argparse
import json
import shutil
import subprocess
from pathlib import Path


def main():
    parser = argparse.ArgumentParser(description="Validate technical Reel properties")
    parser.add_argument("--video", required=True)
    parser.add_argument("--duration", type=float, required=True)
    parser.add_argument("--tolerance", type=float, default=0.2)
    args = parser.parse_args()
    if not shutil.which("ffprobe"):
        raise SystemExit("FFprobe must be available on PATH")
    video = Path(args.video).expanduser().resolve()
    raw = subprocess.check_output(["ffprobe", "-v", "error", "-show_streams", "-show_format", "-of", "json", str(video)], text=True, encoding="utf-8")
    data = json.loads(raw)
    streams = data.get("streams", [])
    v = next((s for s in streams if s.get("codec_type") == "video"), None)
    a = next((s for s in streams if s.get("codec_type") == "audio"), None)
    duration = float(data.get("format", {}).get("duration", 0))
    checks = {
        "file_exists": video.exists() and video.stat().st_size > 0,
        "duration": abs(duration - args.duration) <= args.tolerance,
        "vertical_1080x1920": bool(v and v.get("width") == 1080 and v.get("height") == 1920),
        "h264_video": bool(v and v.get("codec_name") == "h264"),
        "audio_present": a is not None,
    }
    result = {"ok": all(checks.values()), "checks": checks, "actual_duration": duration, "video": str(video)}
    print(json.dumps(result, ensure_ascii=False, indent=2))
    if not result["ok"]:
        raise SystemExit(1)


if __name__ == "__main__":
    main()

```

## Khách chỉ cần làm gì
1. Lần đầu: đưa link kênh mẫu, trang đích, và bỏ video/nhạc/logo vào các thư mục AI mở ra.
2. Các lần sau: nói *"làm Reel tiếp theo"* (kèm nội dung đã duyệt nếu có).
3. Xem video + caption AI đưa; nói "Duyệt/Lên lịch" khi ưng ý — AI mới bấm đăng.

## Nối với các skill khác của JC
- Chấm ý tưởng/kịch bản trước khi dựng: `video-trieu-view-8-yeu-to`. Video tin tức/review có lời dẫn: `tao-video-viral`.
- Caption và cụm cuối bài đúng brand: `chi-tu-viet-bai`.
- Skill này đã gồm đủ bộ mã `viral-facebook-reel-maker` (bản tiếng Anh, cùng script) nên chỉ cần giữ một.
