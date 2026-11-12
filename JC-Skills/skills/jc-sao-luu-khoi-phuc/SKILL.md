---
name: "jc-sao-luu-khoi-phuc"
description: "JC nói lưu đi, sao lưu, đóng gói, backup, cập nhật subagent, khôi phục, sắp cài lại máy: gom skill, subagent (đội mã A), script, nhạc, logo, ảnh mẫu của JC thành một gói, lưu lên Google Drive (CLAUDE_BACKUP) hoặc GitHub riêng tư và khôi phục khi cần."
---

# Sao lưu & khôi phục dữ liệu Claude của JC

Mục tiêu: JC cài lại máy (Windows/Mac) xong, đăng nhập lại là làm tiếp được, không phải làm lại từ đầu.

## Nói thật với JC
- Skill và bộ nhớ nằm trên TÀI KHOẢN Claude, cài lại máy không mất. Skill mới chỉ lưu khi JC bấm LƯU trên thẻ đề xuất → sau mỗi bộ /code mới nhắc JC bấm LƯU.
- Claude KHÔNG tự chạy ngầm; sao lưu chạy khi JC gọi, hoặc ngay sau khi Claude tạo/sửa subagent hay xong một bộ việc lớn (khi đó hỏi JC có muốn lưu không). Muốn lưu định kỳ → tạo tác vụ lên lịch.
- File trên máy JC (nhạc mẫu, tiếng gõ, script, logo, ảnh Mira) mới là thứ mất khi cài lại → cần nơi lưu ngoài máy.
- Skill trong kho The Skill đã mua thì tải lại từ tài khoản mua, không chép vào gói.

## Nơi lưu
- **Chính:** thư mục `CLAUDE_BACKUP` trên Google Drive của JC (tìm bằng Drive search theo tên). Chỉ đẩy file nhỏ bằng connector; file lớn nhờ JC kéo zip vào Drive.
- **Phụ:** Project SubAgent và bộ nhớ Claude (trên đám mây).
- **GitHub:** chỉ khi JC yêu cầu, và PHẢI là repo riêng tư (ví dụ `JessieNguyen-sg/jc-claude-backup`). Chưa có thì nhờ JC tạo repo riêng tư rỗng, không tự tạo repo công khai.

## Khi JC nói "sao lưu"
1. Gom vào một thư mục:
   - `agents/`: mỗi subagent một file `.md` đúng định dạng `.claude/agents/<tên>.md` (có frontmatter name, description, tools), đặt theo mã (vd `a04-grace.md`).
   - `skills/`: bản chép SKILL.md các skill tự tạo (maika-code-video, the-jessie-kitchen-global-code, jc-sao-luu-khoi-phuc…).
   - `scripts/`, `assets/` (logo, ảnh Mira gốc, ảnh 6 code dạng jpg, nhạc mẫu mp3, tiếng gõ wav).
   - `memory-notes/`: quy tắc /code, hồ sơ đội A01–A10, giáo án đã duyệt; quyết định, prompt đã duyệt, công thức mặt nhân vật (giữ nguyên văn, không tóm tắt thay bản gốc).
   - `KHOI-PHUC.md`: quy trình khôi phục, sửa lại nếu quy trình đổi.
2. Nén `JC_Claude_Backup_<ngày>.zip`, gửi JC bằng SendUserFile; lưu lên máy JC nếu máy đang liên kết.
3. Lưu lên Drive `CLAUDE_BACKUP` (ghi đè cùng tên, hoặc thêm ngày vào tên nếu cần giữ bản cũ). Đẩy GitHub nếu JC yêu cầu.
4. **Kiểm tra trước khi báo "đã lưu":** tìm lại thư mục, liệt kê file, đếm đủ N mục. Chưa kiểm thì không nói "xong".
5. Báo JC ngắn: đã lưu gì, ở đâu, tổng số mục, còn gì chưa lưu.

## Khi JC nói "khôi phục" (sau khi cài lại máy)
1. Xem skill và bộ nhớ đã tự có lại chưa (cùng tài khoản).
2. Lấy gói sao lưu (Drive, GitHub clone hoặc zip JC đưa).
3. Tạo `.claude/agents`, bỏ các file `agents/*.md` vào; đưa `scripts/`, `assets/` về `Downloads/Nhac JC/`.
4. Đối chiếu `skills/*/SKILL.md` với skill hiện có; thiếu hoặc cũ hơn thì đề xuất lại bằng thẻ LƯU.
5. Gọi thử một subagent và chạy thử một video ngắn để chắc mọi thứ hoạt động.

## Quy tắc
- Không đưa mật khẩu, OTP, token, API key, số thẻ/tài khoản vào gói.
- Repo sao lưu phải riêng tư.
- Không xóa file cũ khi JC chưa bảo.
- Trả lời tiếng Việt ngắn gọn, làm luôn không hỏi lại nhiều.
