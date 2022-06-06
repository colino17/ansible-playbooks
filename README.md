# ansible-playbooks

`pacman -S gnome-shell gnome-shell-extensions nautilus file-roller gnome-terminal gnome-tweak-tool gnome-remote-desktop gnome-control-center xdg-user-dirs gdm`

```
/etc/fstab
----------
192.168.0.17:/Storage   /Storage  nfs  _netdev,noauto,x-systemd.automount,x-systemd.mount-timeout=10,timeo=14,x-systemd.idle-timeout=1min 0 0
```


# Minimal Arch Install

## Verify the Boot Mode:
`ls /sys/firmware/efi/efivars`

## Partition and Format Disks:
`fdisk -l`
`fdisk /dev/sda`
`g`
`p`

### Create EFI Partition:
`n`
`1`
`default`
`+512M`
`t`
`1`

### Create System Partition:
`n`
`2`
`default`
`default`
`p`
`w`

### Format Partitions:
`mkfs.fat -F 32 /dev/sda1`
`mkfs.ext4 /dev/sda2`

## Mount Partitions:
`mount /dev/sda2 /mnt`
`mkdir /mnt/boot`
`mount /dev/sda1 /mnt/boot`

## Install Base Packages:
`pacstrap /mnt base linux linux-firmware ansible git`

## Generate FSTAB:

`genfstab -U /mnt >> /mnt/etc/fstab`

`cat /mnt/etc/fstab`

## Chroot into system:

`arch-chroot /mnt`
