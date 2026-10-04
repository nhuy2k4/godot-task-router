# Godot Task Router

Bộ quy tắc phân loại task và bàn giao giữa Antigravity (thiết kế/điều phối) và Codex (triển khai/kiểm thử) cho project Godot.

## Cài đặt nhanh

1. Giải nén thư mục `Godot_Task_Router` vào thư mục gốc project Godot, cùng cấp với `project.godot`.
2. Gộp nội dung `AGENTS.md` trong gói vào `AGENTS.md` hiện có ở root (nếu chưa có thì dùng nguyên file).
3. Giữ nguyên `.agents/skills/godot-task-router/` trong project. Thư mục `.agents/skills` là vị trí skill project của Antigravity; Codex có thể dùng skill được phát hiện trong môi trường hỗ trợ Agent Skills.
4. Mở lại workspace/IDE nếu skill chưa xuất hiện. Có thể yêu cầu rõ `/godot-task-router` hoặc “Đọc skill godot-task-router trước khi làm”.

## Cấu trúc

- `AGENTS.md`: nhắc agent áp dụng quy trình phân loại trước khi xử lý task trong project.
- `.agents/skills/godot-task-router/SKILL.md`: quy trình chính và luật ACCEPT / DEFER.
- `references/`: rubric độ phức tạp, vai trò, handoff, và ví dụ.
- `TASK_HANDOFF_TEMPLATE.md`: mẫu để chuyển kết quả giữa hai ứng dụng.

## Cách hoạt động

- Codex nhận task: việc code rõ phạm vi thường ACCEPT; kiến trúc, feature lõi, hoặc rủi ro cao thì DEFER TO ANTIGRAVITY.
- Antigravity nhận task: kiến trúc, phân tích, chia feature, nghiên cứu, review thì ACCEPT; việc implement đã có spec thì DEFER TO CODEX.
- Feature lớn: Antigravity viết spec → người dùng chuyển handoff sang Codex → Codex implement/test → người dùng chuyển lại Antigravity review.

Skill hướng dẫn agent phân loại và tạo handoff; nó không tự gọi tài khoản hoặc gửi task giữa hai ứng dụng. Agent vẫn có thể không tuân thủ prompt tuyệt đối, nên hãy kiểm tra phần ROUTING DECISION ở đầu phản hồi trước khi cho phép sửa project.
