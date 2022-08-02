# VMWare Workstation unter Manjaro:

## Installieren von VMware Workstation über AUR:

Add/Remove Software aufrufen, dort in den Einstellungen unter „Third-Party“ AUR aktivieren.

### Danach Suche nach vmware-workstation
### Aktuell am 2.08.2022: 16.2.4-1

## Kernel installieren über GUI und dann Neustart mit neuem Kernel.

### Kernel herausfinden:

mhwd-kernel –li

### Passende Kernel-Header installieren:

sudo pacman –Syu linux519-headers dkms

## Module herunterladen, erstellen und installieren:

wget https://github.com/mkubecek/vmware-host-modules/archive/workstation-16.2.4.tar.gz

tar -xzf workstation-16.2.4.tar.gz

cd vmware-host-modules-workstation-16.2.4

make

sudo make install


Reboot!
