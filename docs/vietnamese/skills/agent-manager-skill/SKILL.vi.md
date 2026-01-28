---
name: agent-manager-skill
description: Quản lý nhiều CLI agents cục bộ thông qua các phiên tmux (khởi động/dừng/theo dõi/giao việc) với khả năng lập lịch cron-friendly.
---

# Kỹ năng Quản lý Agent (Agent Manager Skill)

## Khi nào sử dụng

Sử dụng kỹ năng này khi bạn cần:

- Chạy nhiều CLI agents cục bộ song song (các phiên tmux riêng biệt)
- Khởi động/dừng agents và theo dõi logs của chúng
- Giao nhiệm vụ cho agents và giám sát đầu ra
- Lập lịch công việc định kỳ cho agent (cron)

## Điều kiện tiên quyết

Cài đặt `agent-manager-skill` trong workspace của bạn:

```bash
git clone https://github.com/fractalmind-ai/agent-manager-skill.git
```

## Các lệnh phổ biến

```bash
python3 agent-manager/scripts/main.py doctor
python3 agent-manager/scripts/main.py list
python3 agent-manager/scripts/main.py start EMP_0001
python3 agent-manager/scripts/main.py monitor EMP_0001 --follow
python3 agent-manager/scripts/main.py assign EMP_0002 <<'EOF'
Follow teams/fractalmind-ai-maintenance.md Workflow
EOF
```

## Ghi chú

- Yêu cầu `tmux` và `python3`.
- Các Agents được cấu hình trong thư mục `agents/` (xem repo để biết ví dụ).
