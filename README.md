# Minimal Arch Install

**Verify the Boot Mode**

`ls /sys/firmware/efi/efivars`

**Partition and Format Disks**

`fdisk -l`

`fdisk /dev/sda`

`g`

`p`

**Create EFI Partition**

`n`

`1`

`default`

`+512M`

`t`

`1`

**Create System Partition**

`n`

`2`

`default`

`default`

`p`

`w`

**Format Partitions**

`mkfs.fat -F 32 /dev/sda1`

`mkfs.ext4 /dev/sda2`

**Mount Partitions**

`mount /dev/sda2 /mnt`

`mkdir /mnt/boot`

`mount /dev/sda1 /mnt/boot`

**Install Base Packages**

`pacstrap /mnt base linux linux-firmware ansible git`

**Generate FSTAB**

`genfstab -U /mnt >> /mnt/etc/fstab`

`cat /mnt/etc/fstab`

**Chroot Into System**

`arch-chroot /mnt`

**Set Time Zone**

`ln -sf /usr/share/zoneinfo/Canada/Atlantic /etc/localtime`

`hwclock --systohc`

**Configure Localization**

`nano /etc/locale.gen`

Uncomment en_US.UTF-8 UTF-8 and run...

`locale-gen`
