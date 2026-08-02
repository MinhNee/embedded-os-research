# QNX OS — Kế hoạch nghiên cứu

## Trạng thái

Đã xác định phạm vi, chưa kết luận kit hoặc BSP cuối cùng. Tài liệu này sẽ được cập nhật khi có kết quả kiểm chứng.

## 1. Các câu hỏi cần trả lời

1. QNX là hệ điều hành gì và thường được dùng trong lĩnh vực nào?
2. Kiến trúc microkernel của QNX khác monolithic kernel Linux ra sao?
3. Những service/process nào tạo thành một hệ thống QNX tối thiểu?
4. QNX SDP, Momentics IDE, toolchain và BSP đảm nhiệm vai trò gì?
5. Các kit nào được BSP chính thức hoặc cộng đồng hỗ trợ?
6. Kit nào có chi phí vừa phải, phổ biến và phù hợp để thực hành?
7. Quy trình build một QNX image gồm các bước nào?
8. Image được nạp, boot và debug bằng cách nào?
9. QNX và Embedded Linux khác nhau về real-time, driver, filesystem, IPC, độ tin cậy và hệ sinh thái như thế nào?

## 2. Kết quả cần tạo

- Bảng các kit/BSP QNX và tiêu chí lựa chọn.
- Sơ đồ kiến trúc QNX microkernel.
- Quy trình build và ý nghĩa từng bước.
- Danh sách thành phần của một QNX boot image.
- Bảng so sánh QNX với Embedded Linux.
- Slide tổng hợp và tài liệu tham khảo.

## 3. Tiêu chí chọn kit

| Tiêu chí | Cách đánh giá |
|---|---|
| BSP | Có BSP tương thích với phiên bản QNX đang sử dụng |
| Khả năng mua | Kit còn bán và có thể mua tại Việt Nam hoặc đặt dễ dàng |
| Chi phí | Phù hợp ngân sách học tập |
| Tài liệu | Có hướng dẫn boot, flash, serial console và driver |
| Cộng đồng | Có ví dụ, diễn đàn hoặc tài liệu thực hành |
| Debug | Có UART/JTAG hoặc cơ chế debug rõ ràng |

## 4. Kế hoạch commit

```text
research: list candidate QNX boards and BSPs
research: document QNX boot image components
research: add QNX build workflow
research: compare QNX and embedded Linux
docs: add QNX presentation
```

