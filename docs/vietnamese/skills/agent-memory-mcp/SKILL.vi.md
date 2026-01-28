---
name: agent-memory-mcp
author: Amit Rathiesh
description: Một hệ thống bộ nhớ lai (hybrid) cung cấp khả năng quản lý tri thức bền vững, có thể tìm kiếm cho các AI agents (Kiến trúc, Mẫu, Quyết định).
---

# Kỹ năng Bộ nhớ Agent (Agent Memory Skill)

Kỹ năng này cung cấp một ngân hàng bộ nhớ bền vững, có thể tìm kiếm và tự động đồng bộ hóa với tài liệu dự án. Nó chạy như một máy chủ MCP để cho phép đọc/ghi/tìm kiếm các ký ức dài hạn (long-term memories).

## Điều kiện tiên quyết

- Node.js (v18+)

## Thiết lập

1. **Clone Repository**:
   Clone dự án `agentMemory` vào workspace của agent hoặc một thư mục song song:

   ```bash
   git clone https://github.com/webzler/agentMemory.git .agent/skills/agent-memory
   ```

2. **Cài đặt Dependencies**:

   ```bash
   cd .agent/skills/agent-memory
   npm install
   npm run compile
   ```

3. **Khởi động MCP Server**:
   Sử dụng helper script để kích hoạt ngân hàng bộ nhớ cho dự án hiện tại của bạn:

   ```bash
   npm run start-server <project_id> <absolute_path_to_target_workspace>
   ```

   _Ví dụ cho thư mục hiện tại:_

   ```bash
   npm run start-server my-project $(pwd)
   ```

## Khả năng (Công cụ MCP)

### `memory_search`

Tìm kiếm ký ức theo truy vấn, loại hoặc thẻ.

- **Args**: `query` (string), `type?` (string), `tags?` (string[])
- **Sử dụng**: "Tìm tất cả các mẫu xác thực" -> `memory_search({ query: "authentication", type: "pattern" })`

### `memory_write`

Ghi lại kiến thức mới hoặc quyết định.

- **Args**: `key` (string), `type` (string), `content` (string), `tags?` (string[])
- **Sử dụng**: "Lưu quyết định kiến trúc này" -> `memory_write({ key: "auth-v1", type: "decision", content: "..." })`

### `memory_read`

Truy xuất nội dung ký ức cụ thể theo khóa (key).

- **Args**: `key` (string)
- **Sử dụng**: "Lấy thiết kế xác thực" -> `memory_read({ key: "auth-v1" })`

### `memory_stats`

Xem phân tích về việc sử dụng bộ nhớ.

- **Sử dụng**: "Hiển thị thống kê bộ nhớ" -> `memory_stats({})`

## Dashboard

Kỹ năng này bao gồm một dashboard độc lập để trực quan hóa việc sử dụng bộ nhớ.

```bash
npm run start-dashboard <absolute_path_to_target_workspace>
```

Truy cập tại: `http://localhost:3333`
