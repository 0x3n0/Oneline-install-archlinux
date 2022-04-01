# One Liner Installation Archlinux BIOS/DOS

```
echo -e "g\nn\n\n\n+100M\nt\n1\nn\n\n\n+1G\nn\n\n\n\n\nw\nq\n" | fdisk /dev/sda && mkfs.vfat -F32 /dev/sda1 && mkswap /dev/sda2 && mkfs.ext4 /dev/sda3 && swapon /dev/sda2 && mount /dev/sda3 /mnt && mkdir -p /mnt/{boot/} && mount /dev/sda1 /mnt/boot && pacstrap /mnt base base-devel vi && genfstab -p /mnt >> /mnt/etc/fstab && echo -e "echo 3n0 > /etc/hostname && echo '127.0.1.1 3n0.localdomain 3n0' >> /etc/hosts && rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Jakarta /etc/localtime && echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen && echo 'LANG=en_US.UTF-8' > /etc/locale.conf && mkinitcpio -p linux" | arch-chroot /mnt && echo -e "pacman --noconfirm -Syu xorg-server xorg-xinit xorg-server-utils xf86-video-intel xf86-input-synaptics networkmanager chromium git openssh" | arch-chroot /mnt && echo -e "useradd -Nm -g users -G wheel,sys 0x" | arch-chroot /mnt && echo -e "echo ' \n \n' | passwd 0x" | arch-chroot /mnt
```



# Details

## Create partion
```bash
echo -e "g\nn\n\n\n+100M\nt\n1\nn\n\n\n+1G\nn\n\n\n\n\nw\nq\n" | fdisk /dev/sda
```

## Formate partition
```plaintext
mkfs.vfat -F32 /dev/sda1
mkswap /dev/sda2
mkfs.ext4 /dev/sda3
```

## Enable Swap

```plaintext
swapon /dev/sda2
```

## Mount partition
```plaintext
mount /dev/sda3 /mnt
mkdir -p /mnt/{boot/}
mount /dev/sda1 /mnt/boot/efi
```

## Install basic system file
```plaintext
pacstrap /mnt base base-devel
genfstab -p /mnt >> /mnt/etc/fstab
```
```bash
echo -e "echo 3n0 > /etc/hostname" | arch-chroot /mnt
echo -e "echo '127.0.1.1 3n0.localdomain 3n0' >> /etc/hosts" | arch-chroot /mnt
echo -e "rm -f /etc/localtime" | arch-chroot /mnt
echo -e "ln -s /usr/share/zoneinfo/Asia/Jakarta /etc/localtime" | arch-chroot /mnt
echo -e "echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen" | arch-chroot /mnt
echo -e "locale-gen" | arch-chroot /mnt
echo -e "echo 'LANG=en_US.UTF-8' > /etc/locale.conf" | arch-chroot /mnt

echo -e "mkinitcpio -p linux" | arch-chroot /mnt
```

```bash
echo -e "pacman --noconfirm -Syu xorg-server xorg-xinit xorg-server-utils xf86-video-intel xf86-input-synaptics networkmanager chromium git openssh" | arch-chroot /mnt
```

```bash
echo -e "useradd -Nm -g users -G wheel,sys 0x" | arch-chroot /mnt
echo -e "echo ' \n \n' | passwd 0x" | arch-chroot /mnt
```
