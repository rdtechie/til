# NixOS - Getting Started

## NixOS Website

- [NixOS](https://nixos.org)
- [NixOS Manual](https://nixos.org/manual/nixos/stable/) 
- [NixOS ISO - Intell/AMD - GNOME - Stable](https://channels.nixos.org/nixos-22.05/latest-nixos-gnome-x86_64-linux.iso)
- [NixOS ISO - Intell/AMD - GNOME - Unstable](https://channels.nixos.org/nixos-unstable/latest-nixos-gnome-x86_64-linux.iso)
- [NixOS ISO - ARM - Minimal - Stable](https://releases.nixos.org/nixos/22.05-aarch64/nixos-22.05.4345.6649e08812f/nixos-minimal-22.05.4345.6649e08812f-aarch64-linux.iso)

## Initial Boot

- Boot from ISO
  `sudo su`
- Change password:
  `passwd`

## Partitioning

Partitioning for UEFI
```shell
parted /dev/nvme0n1 -- mklabel gpt
parted /dev/nvme0n1 -- mkpart primary 512MiB -8GiB
parted /dev/nvme0n1 -- mkpart primary linux-swap -8GiB 100%
parted /dev/nvme0n1 -- mkpart ESP fat32 1MiB 512MiB
parted /dev/nvme0n1 -- set 3 esp on
mkfs.ext4 -L nixos /dev/nvme0n1p1
mkswap -L swap /dev/nvme0n1p2
mkfs.fat -F 32 -n boot /dev/nvme0n1p3
```

## Mounting
```shell
mount /dev/disk/by-label/nixos /mnt
mkdir -p /mnt/boot
mount /dev/disk/by-label/boot /mnt/boot
swapon /dev/nvme0n1p2
```

## Validate
```shell
lsblk -f
```