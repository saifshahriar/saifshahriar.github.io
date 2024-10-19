+++
title = "Arch Linux Installation Handbook"
author = "Saif Shahriar"
date = "2021-10-19"
category = "example2"
+++
<b>Index</b>
- [Install Arch Linux](#install-arch-linux)
  - [Verify Boot Mode](#verify-boot-mode)
  - [Make sure you have internet](#make-sure-you-have-internet)
  - [Update the system clock](#update-the-system-clock)
  - [Partitioning the disk](#partitioning-the-disk)
  - [Format partitions](#format-partitions)
  - [Mount the file systems](#mount-the-file-systems)
  - [Installation](#installation)
    - [Select the mirrors](#select-the-mirrors)
    - [Install essential packages](#install-essential-packages)
  - [Configure the system](#configure-the-system)
    - [Fstab (contains all the drivers)](#fstab-contains-all-the-drivers)
    - [Chroot](#chroot)
    - [Enable network manager at boot](#enable-network-manager-at-boot)
    - [Install a boot loader (grub)](#install-a-boot-loader-grub) 
  - [Optional](#optional)
    - [User setup](#user-setup)
    - [Timezone](#timezone)
    - [Localization](#localization)
    - [Set users](#set-users)
- [Install blackarch on top of arch linux](#install-blackarch-on-top-of-arch-linux)
  - [You may now install tools from the blackarch repository](#you-may-now-install-tools-from-the-blackarch-repository) 

# Install Arch Linux

## Verify Boot Mode

Check if you have an efi or bios system.
```bash
ls /sys/firmware/efi/efivars
```
<br>

## Make sure you have internet 

To make sure you have internet connection, simply ping to any valid website.
```bash
ping saifshahriar.github.io
```
<br>

## Update the system clock

Use ```timedatectl``` to make sure the system clock is accurate.
```bash
timedatectl set-ntp true
```
To check the status simply type,
```bash
timedatectl status
```
<br>

## Partitioning the disk

Use ```cfdisk``` tool to partition the disks.

  - Make 3 partitions
    - boot 
      - Size:     ```128M```
      - Bootable: ```[  * ]```
      - Name:     ```/dev/sda1```
    - swp
      - Size:     ```1G```
      - Type:     ```Swap/Solaris```
      - Name:     ```/dev/sda2```
    - rooot
      - Size:     Rest of the space
      - Name:     ```/dev/sda3```
<br>

## Format partitions 
```bash
# format boot & root
mkfs.ext4 /dev/sda1
mkfs.ext4 /dev/sda3

# format swp
mkswap /dev/sda2
```
<br>

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
<br>
<br>
<br>

## Installation
### Select the mirrors:
```bash
vim /etc/pacman.d/mirrorlist
```
### Install essential packages
```bash
pacstrap /mnt base base-devel linux linux-firmware vim networkmanager git grub opendoas 
```
<br>

## Configure the system
### Fstab (contains all the drivers)
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```
### Chroot
```bash
arch-chroot /mnt
```
### Enable network manager at boot
```bash
systemctl enable NetworkManager
```
### Install a boot loader (grub)
```bash
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```
<br>

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

# Add another user and passwd
useradd -m saif
passwd saif

# Give user the permission
usermod -aG wheel,audio,video,optical,storage saif
```
- Configure superuser privilege: 
  - Edit the sodoers file. (if you are using doas insted of sudo then see the next point)
```bash
visudo
```
Uncomment the following line 

```diff
## Allow members of group wheel to execute any command
- # %wheel ALL=(ALL:ALL) ALL
+ %wheel ALL=(ALL:ALL) ALL

## Uncomment to allow members of group wheel to execute any command
- # %sudo ALL=(ALL:ALL) ALL
+ %sudo ALL=(ALL:ALL) ALL
```

  - doas configuration:
Create a name `/etc/doas.conf`
```bash
touch /etc/doas.conf
```
Now add these lines to the file.
To permit the user `saif` to execute any command as a root user:
```
permit saif as root
```
To permit any user from the `:wheel` to execute any command as a root user.
```
permit :wheel as root
```
Don't ask for password for some times:
```
permit persist saif as root
```

Now `unmount -R /mnt` remove the installation media and `reboot`
<br>
<br>
<br>

# Install blackarch on top of arch linux

```bash
# Run https://blackarch.org/strap.sh as root and follow the instructions.
curl -O https://blackarch.org/strap.sh

# Verify the SHA1 sum
echo 8bfe5a569ba7d3b055077a4e5ceada94119cccef strap.sh | sha1sum -c

# Set execute bit
chmod +x strap.sh

# Run strap.sh
sudo ./strap.sh
```

Enable multilib:
To enable multilib repository, uncomment the `[multilib]` section in `/etc/pacman.conf`.

```bash
vim /etc/pacman.conf
```
Find
```bash
[multilib]
Include = /etc/pacman.d/mirrorlist
```
and uncomment the section.

Now synchronize the packages and upgrade the system.

```bash
sudo pacman -Syu
```

- <b>Tip:</b> Run ```pacman -Sl multilib``` to list all packages in the multilib repository. 32-bit library package names begin with lib32-.

<br>

## You may now install tools from the blackarch repository.
To list all of the available tools, run
```bash
sudo pacman -Sgg | grep blackarch | cut -d' ' -f2 | sort -u
```
To install all of the tools, run
```bash
sudo pacman -S blackarch
```
To install a category of tools, run
```bash
sudo pacman -S blackarch-<category>
```
To see the blackarch categories, run
```bash
sudo pacman -Sg | grep blackarch
```
- <b>Note</b> - it maybe be necessary to overwrite certain packages when installing blackarch tools. If you experience "failed to commit transaction" errors, use the --needed and --overwrite switches

For example:

```bash
sudo pacman -Syyu --needed blackarch --overwrite='*'
```
