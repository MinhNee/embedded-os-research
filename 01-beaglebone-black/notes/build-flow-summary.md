# BeagleBone Black — Build Full Flow

## 1. Mục tiêu

Tạo một hệ thống Linux nhúng hoàn chỉnh cho BeagleBone Black từ các thành phần có thể kiểm soát và tái lập được.

## 2. Chuỗi build

```text
Buildroot configuration
  → cross-compilation toolchain
  → U-Boot SPL/MLO + U-Boot proper
  → Linux zImage + Device Tree
  → BusyBox/packages + root filesystem
  → boot.vfat + rootfs.ext4
  → sdcard.img
```

## 3. Chuỗi boot và ý nghĩa

| Giai đoạn | Artefact | Ý nghĩa |
|---|---|---|
| Boot ROM | Mã cố định trong AM335x | Đọc boot pins, chọn nguồn boot và tìm SPL |
| SPL | `MLO` | Chạy trong SRAM, khởi tạo tối thiểu clock/DDR/MMC và tải U-Boot |
| U-Boot | `u-boot.img` | Nhận diện board, tải kernel/DTB, tạo bootargs và chuyển quyền cho kernel |
| Linux kernel | `zImage` | Khởi tạo MMU, scheduler, driver và mount root filesystem |
| Device Tree | `am335x-boneblack.dtb` | Mô tả phần cứng cụ thể để kernel probe đúng driver |
| Root filesystem | `rootfs.ext4` | Chứa thư viện, shell, cấu hình, init, service và ứng dụng |
| Disk image | `sdcard.img` | Chứa partition table, boot partition và rootfs để ghi lên toàn bộ microSD |

## 4. Baseline bằng Buildroot

```bash
make beaglebone_defconfig
make menuconfig        # tùy chọn
make -j"$(nproc)"
```

Các file bàn giao nằm trong `output/images/`. Ghi `sdcard.img` vào toàn bộ thiết bị thẻ nhớ, không ghi vào một partition như `/dev/sdX1`.

## 5. Cách học từng tầng

1. Boot thành công bằng image Buildroot nguyên bản.
2. Build thủ công U-Boot và chỉ thay `MLO` cùng `u-boot.img`.
3. Build thủ công kernel, DTB và modules; thay cả nhóm đồng bộ.
4. Giữ rootfs của Buildroot cho tới khi bootloader và kernel đã ổn định.
5. Sau cùng mới thử dựng BusyBox/rootfs thủ công.

## 6. Kiểm tra sau khi boot

```bash
uname -a
cat /proc/device-tree/model
cat /proc/cmdline
mount
lsblk
ip addr
dmesg
lsmod
```

UART0 cần được theo dõi từ lúc power-on để xác định checkpoint cuối cùng mà hệ thống đi qua.

## 7. Lỗi thường gặp

- Trộn `MLO`, U-Boot, kernel và DTB từ các phiên bản khác nhau.
- Dùng sai cross-compiler hoặc sai ABI.
- Kernel module không khớp kernel release/vermagic.
- MMC hoặc ext4 được cấu hình dạng module dù cần để mount rootfs.
- Hard-code sai `/dev/mmcblkXpY`; nên ưu tiên PARTUUID khi đóng gói sản phẩm.
- Flash nhầm thiết bị hoặc ghi vào partition thay vì toàn bộ disk.
- Không giữ nút BOOT/S2 trong lúc power-on nên board vẫn boot Debian từ eMMC.

## 8. Tài liệu tham khảo

- [BeagleBone Black documentation](https://docs.beagleboard.org/boards/beaglebone/black/)
- [Buildroot manual](https://buildroot.org/downloads/manual/manual.html)
- [Buildroot BeagleBone defconfig](https://gitlab.com/buildroot.org/buildroot/-/raw/master/configs/beaglebone_defconfig)
- [U-Boot AM335x documentation](https://docs.u-boot.org/en/latest/board/ti/am335x_evm.html)
- [Linux kernel documentation](https://docs.kernel.org/)
- [BeagleBone Black Rev C overview](https://pivietnam.com.vn/beaglebone-black-rev-c-pivietnam-com-vn.html)

