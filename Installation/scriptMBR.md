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
* Pilih `DOS`
* Jangan lupa rootnya tandai menjadi `bootable`
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
pacstrap /mnt base linux-lts linux-lts-headers linux-firmware vim intel-ucode
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
echo "arch-desktop" >> /etc/hostname
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
pacman -S grub ntfs-3g base-devel networkmanager network-manager-applet wpa_supplicant wireless_tools xdg-utils xdg-user-dirs xf86-video-intel gvfs os-prober mtools dosfstools xf86-input-libinput pipewire pipewire-pulse pipewire-media-session pipewire-alsa pavucontrol git
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
edit doas
```
vim /etc/doas.conf
```
```
permit :wheel
```
```
vim .bashrc
```
```
complete -cf doas
```
```
pacman -S yay xorg <window manager or desktop environment>
```
copy windowsfont
```
mkdir /usr/share/fonts/WindowsFonts
cp /Windows81/Windows/Fonts/* /usr/share/fonts/WindowsFonts/
chmod 644 /usr/share/fonts/WindowsFonts/*
fc-cache -f
```
