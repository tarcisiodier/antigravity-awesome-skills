---
name: address-github-comments
description: Sử dụng khi bạn cần xử lý các bình luận review hoặc issue trên một GitHub Pull Request đang mở bằng cách sử dụng gh CLI.
---

# Xử lý Bình luận GitHub (Address GitHub Comments)

## Tổng quan

Xử lý hiệu quả các bình luận review trên PR hoặc phản hồi issue bằng GitHub CLI (`gh`). Kỹ năng này đảm bảo tất cả phản hồi được giải quyết một cách có hệ thống.

## Điều kiện tiên quyết

Đảm bảo `gh` đã được xác thực (authenticated).

```bash
gh auth status
```

Nếu chưa đăng nhập, hãy chạy `gh auth login`.

## Quy trình làm việc

### 1. Kiểm tra Bình luận

Lấy các bình luận cho PR của nhánh hiện tại.

```bash
gh pr view --comments
```

Hoặc sử dụng một script tùy chỉnh nếu có để liệt kê các luồng (threads).

### 2. Phân loại và Lên kế hoạch

- Liệt kê các bình luận và luồng review.
- Đề xuất cách sửa cho từng cái.
- **Đợi xác nhận của người dùng** về việc nên xử lý bình luận nào trước nếu có quá nhiều.

### 3. Áp dụng các bản sửa lỗi (Fixes)

Thực hiện các thay đổi code cho các bình luận đã chọn.

### 4. Phản hồi các Bình luận

Khi đã sửa xong, hãy phản hồi vào các luồng là đã giải quyết.

```bash
gh pr comment <PR_NUMBER> --body "Addressed in latest commit."
```

## Các sai lầm thường gặp

- **Sửa lỗi mà không hiểu ngữ cảnh**: Luôn đọc code xung quanh một bình luận.
- **Không xác minh xác thực (auth)**: Kiểm tra `gh auth status` trước khi bắt đầu.
