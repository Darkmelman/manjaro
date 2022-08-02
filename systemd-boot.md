# Manjaro Systemd-boot

# mountpoint aendern
lsblk 
nvme0n1p1 ist die Boot Partition

sudo su
umount /boot/efi
rmdir /boot/efi
mkdir -p /tmp/bootdir
cp -r /boot/* /tmp/bootdir
rm -rf /boot/*
mount /dev/nvme0n1p1 /boot
cp -r /tmp/bootdir/* /boot/
rm -rf /tmp/bootdir
exit

# /etc/fstab aendern von /boot/efi # nach /boot

vi /etc/fstab

# systemd-boot installieren
sudo bootctl install

# check entries
efibootmgr -v

# systemd-boot-manager
sudo pacman-Sy systemd-boot-manager

# config bei Bedarf
vi /etc/sdboot-manager.conf

# Generieren:
sudo sdboot-manage gen

# Kontrolle:
ls -al /boot/loader/entries

#Removing grub
sudo pacman -Rn grub-btrfs grub-theme-manjaro

sudo pacman -Rn grub

# keyfile entfernen:
vi /etc/mkinitcpio.conf

#FILES=“/crypto_keyfile.bin“

# initramfs neu generieren:
mkinitcpio -P

# key aus luks Slot loeschen:

cryptsetup luksDump /dev/nvme0n1p2

# Slots testen:
cryptsetup luksOpen - - test-passphrase - -key-slot 0 /dev/nvme0n1p2 && echo correct

# der Slot mit dem Key gibt folgendes zurück: (unbedingt richtige Passphrase nutzen!)
No lex. available with this passphrase

# Kill Slot:
cryptsetup luksKillSlot /dev/nvme0n1p2 1

# Danach noch mal mit luksDump prüfen bei Bedarf.

# Anzeige Bootmenu
vi /boot/loader/loader.conf

# einkommentieren der Timeout-Zeile #
Timeout 3

# Yubikey:

# libfido2 ueber PacketManager installieren
suche nach libfido2


# Swapfile vergroessern auf 16384:
Pfad /swap/swapfile

# Das Acasis Case funktioniert nicht:
# Thunderbolt Support für Plasma installieren:

plasma-thunderbolt


# Wenn man beim Start zweimal die Passphrase eingeben muss:

Prüfen ob /etc/mkinitcpio.conf

FILES=(/crypto_keyfile.bin)

enthält.


cryptsetup luksAddKey /dev/mvme0n1p2 /crypto_keyfile.bin

cryptsetup luksAddKey /dev/mvme0n1p3 /crypto_keyfile.bin

mkinitcpio -P

Danach sollte nur einmal nach der Passphrase gefragt werden



