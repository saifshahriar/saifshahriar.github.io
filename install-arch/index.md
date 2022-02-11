# Install Arch Linux

## Verify Boot Mode

If you have a uefi or bios 
To check,
```bash
ls /sys/firmware/efi/efivars
```

## Make sure you have internet 

To make sure you have internet connection, simply ping to any valid website.
```bash
ping saifshahriar.github.io
```

## Update the system clock

Use ```timedatectl``` to make sure the system clock is accurate.
```bash
timedatectl set-ntp true
```
To check the status simply type,
```bash
timedatectl status
```


## Partitioning the disk

Use ```cfdisk``` tool to partition the disks.

  - Make 3 partitions
    - boot 
      - Size:     ```128M```
      - Bootable: ```[  * ]```
      - Type:     ```Default/Linux```
      - Name:     ```/dev/sda1```
    - swp
      - Size:     ```1G```
      - Type:     ```Swap/Solaris```
      - Name:     ```/dev/sda2```
    - rooot
      - Size:     Rest of the space
      - Name:     ```/dev/sda3```

## Format partitions 
```bash
# format boot & root
mkfs.ext4 /dev/sda1
mkfs.ext4 /dev/sda3

# format swp
mkswap /dev/sda2
```

## Mount the file systems

  1. Mount `root` first:
    ```bash
    mount /dev/sda3 /mnt
    ```
  2. Boot:
        - Now make a `boot` directory inside `/mnt`:
          ```bash
          mkdir /mnt/boot
          ```
        - Now mount `boot`:
          ```bash
          mount /dev/sda1 /mnt/boot
          ```
  3. Mount `swp`:
   ```bash
   swapon /dev/sda2
   ```
  `lsblk` to check the partition info
   
## Installation
### Select the mirrors:
```bash
vim /etc/pacman.d/mirrorlist
```
Remove everything except Asian server.

```bash
# Related VIM command
<CTRL + SHIFT + V>

Now navigate up/down. That would select all the line that needs to be commented.

<SHIFT + I>

# Now put the <#> in one line.
<SHIFT + 3 (#)>

# Hit escape
<ESC>
```

### Install essential packages
```bash
pacstrap /mnt base base-devel linux linux-firmware vim
```

## Configure the system
### Fstab (contains all the drivers)
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```
### Chroot
```bash
arch-chroot /mnt
```
### Install some package for default and use it
```bash
pacman -Sy
pacman -S networkmanager grub sudo
systemctl enable NetworkManager
```
### Install a boot loader (grub)
```bash
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

## Optional
### User setup
```bash
vim /etc/hostname
```
put `arch` there
### Timezone
```bash
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
hwclock --systohc
```
### Localization
```bash
vim /etc/locale.gen
# Uncomment needed locale

locale-gen
```
Now  go to the `vim /etc/locale.conf` and add the line `LANG=en_US.UTF-8`
### Set users
```bash
# To setup root passwd
passwd 
adduser -m saif
passwd saif
```
