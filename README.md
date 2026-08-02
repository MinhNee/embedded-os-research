# Embedded OS Research

Repository lưu trữ kết quả nghiên cứu về quy trình build hệ điều hành nhúng theo yêu cầu của giảng viên. Nội dung được chia theo từng chủ đề; README này là nơi tổng hợp và cập nhật tiến độ chung.

## Mục tiêu

1. Tìm hiểu quy trình build Full Flow cho kit BeagleBone Black, gồm quy trình và ý nghĩa của từng bước.
2. Tìm hiểu hệ điều hành QNX: kiến trúc, kit hỗ trợ, quy trình build, các thành phần, đặc điểm và so sánh với Embedded Linux.
3. Dùng Git và commit thường xuyên để lưu lại tiến trình nghiên cứu.

## Tiến độ

| Hạng mục | Trạng thái | Kết quả hiện có | Việc tiếp theo |
|---|---|---|---|
| Task 1 — BeagleBone Black Full Flow | Đã có bản tổng hợp và slide | [PowerPoint](01-beaglebone-black/slides/BeagleBone_Boot_Build_Flow.pptx), [ghi chú quy trình](01-beaglebone-black/notes/build-flow-summary.md) | Build thử trên Linux host, flash microSD và lưu UART boot log |
| Task 2 — QNX OS | Đã lập kế hoạch | [Phạm vi nghiên cứu](02-qnx-os/notes/research-plan.md) | Chọn kit/BSP phù hợp và bắt đầu tổng hợp tài liệu |

> Trạng thái trong bảng phản ánh kết quả thực tế. Mỗi khi hoàn thành thêm một phần, README sẽ được cập nhật trong cùng commit với tài liệu hoặc kết quả mới.

## Cấu trúc repository

```text
embedded-os-research/
├── README.md
├── 01-beaglebone-black/
│   ├── notes/
│   │   └── build-flow-summary.md
│   └── slides/
│       └── BeagleBone_Boot_Build_Flow.pptx
└── 02-qnx-os/
    └── notes/
        └── research-plan.md
```

## Task 1 — BeagleBone Black Full Flow

Chuỗi boot tổng quát:

```text
Power-on
  → Boot ROM
  → SPL/MLO
  → U-Boot
  → Linux kernel + Device Tree
  → Root filesystem
  → init/PID 1
  → services và ứng dụng
```

Hướng triển khai được chọn:

- Dùng Buildroot tạo baseline đồng bộ gồm toolchain, U-Boot, kernel, DTB, rootfs và `sdcard.img`.
- Sau khi baseline boot thành công, build thủ công U-Boot hoặc kernel để hiểu từng tầng và thay thử từng nhóm artefact.
- Không thay đồng thời nhiều thành phần, nhằm giữ khả năng khoanh vùng lỗi qua UART.

## Task 2 — QNX OS

Các nội dung sẽ nghiên cứu:

- Kiến trúc microkernel và các process hệ thống.
- QNX Software Development Platform, BSP và toolchain.
- Các board/kit được hỗ trợ; đánh giá mức độ phổ biến và chi phí.
- Quy trình build image, boot và debug.
- Các thành phần trong image QNX.
- Đặc điểm real-time, độ tin cậy và cơ chế cô lập lỗi.
- So sánh QNX với Embedded Linux trên kit nhúng.

## Quy ước commit

Sử dụng commit nhỏ, mô tả đúng kết quả vừa hoàn thành:

```text
docs: add BeagleBone Black build-flow slides
docs: update BeagleBone progress and references
research: add QNX supported-board notes
research: compare QNX microkernel with Linux
test: add BeagleBone UART boot log
```

Không gom toàn bộ quá trình nghiên cứu vào một commit duy nhất. Mỗi commit nên chứa một thay đổi có thể đọc và kiểm tra độc lập.

## Nhật ký cập nhật

### 2026-08-02

- Khởi tạo cấu trúc repository theo hai chủ đề nghiên cứu.
- Thêm slide tổng hợp quy trình build Full Flow cho BeagleBone Black.
- Thêm ghi chú quy trình và kế hoạch nghiên cứu QNX.

