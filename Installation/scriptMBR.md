cek internet
```
ip a
```
connect wifi
```
iwctl
```
```
station connect "Redmi 5A"
```
`Ctrl + D` untuk keluar

cek partisi
```
lsblk
```
buat partisi
```
cfdisk
```
* Pilih `DOS` jika `MBR` (Pilih `GPT` jika `UEFI`)
* Write
format partisi
```
mkfs.ext4 /dev/sda1
```
mount partisi root
```
mount /dev/sda1 /mnt
```
install kernel
```
pacstrap /mnt base linux linux-firmware vim intel-ucode
```
generate fstab
```
genfstab -U /mnt >> /mnt/etc/fstab
```
cek
```
cat /etc/fstab
```
root
```
arch-chroot /mnt
```
setting timezone
```
ln -sf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
```
terapkan
```
hwclock --systohc
```
edit file
```
vim /etc/locale.gen
```
uncomment `en_US.UTF-8 UTF-8`

run
```
locale-gen
echo "LANG=en_US.UTF-8" >> /etc/locale.conf
echo "KEYMAP=us" >> /etc/vconsole.conf
echo "arch" >> /etc/hostname
```
```
vim /etc/hosts
```
edit
```
127.0.0.1 localhost
::1       localhost
127.0.1.1 arch.localdomain  arch
```
set password `root`
```
passwd
```
install package
```
pacman -S grub ntfs-3g base-devel linux-headers networkmanager network-manager-applet wpa_supplicant xdg-utils xdg-user-dirs pulseaudio alsa-utils pavucontrol wireless_tools os-prober mtools dosfstools
```
install grub
```
grub-install --target=i368-pc /dev/sda
```
```
grub-mkconfig -o /boot/grub/grub.cfg
```
enable network manager
```
systemctl enable NetworkManager
```
```
exit
```
lepas
```
umount -a
```
reboot
```
reboot
```
login

buat user
```
useradd -aG wheel malik
```
```
passwd malik
```
edit sudo
```
EDITOR=vim visudo
```
```
pacman -S xf86-video-intel xorg git
```
copy windowsfont
```
mkdir /usr/share/fonts/WindowsFonts
cp /Windows81/Windows/Fonts/* /usr/share/fonts/WindowsFonts/
chmod 644 /usr/share/fonts/WindowsFonts/*
fc-cache -f
```
