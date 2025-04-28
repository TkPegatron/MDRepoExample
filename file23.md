# Installation process

```shell
### !!! Do the partitioning and cloning
# Bindmount /mnt
sudo mkdir -pv /mnt/mnt
sudo mount --bind /mnt /mnt/mnt
# Create an ssh host key
sudo mkdir -pv /mnt/etc/secrets/initrd/
sudo ssh-keygen -t ed25519 -N "" -f /mnt/etc/secrets/initrd/ssh_host_ed25519_key
# Enable the unstable nix features
sudo nix-env -f '<nixpkgs>' -iA nixUnstable
# Install the new flaked root
sudo nixos-install --impure --root /mnt --flake /mnt/etc/nixos#nixtest
```



```
nix build --no-link ~/.config/nixpkgs#homeConfigurations.eperry.activationPackage --extra-experimental-features "nix-command flakes"
"$(nix path-info ~/.config/nixpkgs#homeConfigurations.eperry.activationPackage --extra-experimental-features "nix-command flakes")"/activate
```


home-manager switch --flake ~/.config/nixpkgs#eperry --extra-experimental-features "nix-command flakes"



networking.nftables.ruleset


https://github.com/samiulbasirfahim/Flakes/tree/main/modules/core
https://github.com/flick0/dotfiles/tree/aurora
https://github.com/zemmsoares/awesome-rices

# Hardened System

- Ephemeral root storage
- Encrypted persistence store
- Persistent home and system config
- ZRAM Swap
- 

```shell
# Mount our tmpfs root to /mnt and create the bind FSH
mount -t tmpfs none /mnt
mkdir -p /mnt/{boot,home,nix,etc/{nixos,ssh,secrets/initrd},var/{lib,log},srv}
# Mount the unencrypted boot partition
mount /dev/vda1 /mnt/boot
# Mount the nix store partition, I opt for LVM on LUKS
mount /dev/vg_nix_persist/lv_nix_persist /mnt/nix
mkdir -p /mnt/nix/persist/{home,etc/{nixos,ssh},secrets/initrd,var/{lib,log},srv}
# Bind mount for system build
mount -o bind /mnt/nix/persist/home /mnt/home
mount -o bind /mnt/nix/persist/var/log /mnt/var/log
mount -o bind /mnt/nix/persist/etc/nixos /mnt/etc/nixos
# Generate keys needed for remote cryptsetup
ssh-keygen -t ed25519 -N "" -f /mnt/nix/persist/etc/secrets/initrd/ssh_host_ed25519_key
#
# If using age secrets, generate the hostkeys and update secrets prior to building
#
ssh-keygen -t ed25519 -N "" -f /mnt/nix/persist/etc/ssh/ssh_host_ed25519_key
ssh-keygen -t rsa -N "" -f /mnt/nix/persist/etc/ssh/ssh_host_rsa_key
nix-shell -p ssh-to-age --run 'cat /mnt/nix/persist/etc/ssh/ssh_host_ed25519_key.pub | ssh-to-age'
#
# Sync your config repository to /mnt/etc/nixos and build using the following commands
#
sudo nix-env -f '<nixpkgs>' -iA nixUnstable
sudo nixos-install --impure --root /mnt --flake /mnt/etc/nixos#nixtest
```




```shell
# Format system partition and mount it
cryptsetup luksFormat /dev/vda2
cryptsetup luksOpen /dev/vda2 nixos-system
mkfs.btrfs -L nixos-system /dev/mapper/nixos-system
mount /dev/mapper/nixos-system /mnt

# Format and mount /boot
mkfs.vfat /dev/vda1
mkdir /mnt/boot
mount /dev/vda1 /mnt/boot/

# Create BTRFS Subvolumes
btrfs sub cr /mnt/nix
btrfs sub cr /mnt/log
btrfs sub cr /mnt/home
btrfs sub cr /mnt/persist

# Remount as tmpfs and create directories
umount /mnt
mount -t tmpfs none /mnt
mkdir -p /mnt/{boot,persist,home,nix,var/{lib,log}}
mkdir -p /mnt/etc/NetworkManager
mkdir -p /mnt/etc/nixos

# Remount BTRFS Subvolumes
mount -o subvol=nix,compress=zstd,noatime /dev/mapper/cryptoroot /mnt/nix
mount -o subvol=log,compress=zstd,noatime /dev/mapper/cryptoroot /mnt/var/log
mount -o subvol=home,compress=zstd,noatime /dev/mapper/cryptoroot /mnt/home
mount -o subvol=persist,compress=zstd,noatime /dev/mapper/cryptoroot /mnt/persist

# Create persistance topology
mkdir -p /mnt/persist/etc/{nixos,NetworkManager}
mkdir -p /mnt/persist/var/lib

# Bind persistent storage
mount -o bind /mnt/persist/etc/NetworkManager /mnt/etc/NetworkManager
mount -o bind /mnt/persist/etc/nixos /mnt/etc/nixos
mount -o bind /mnt/persist/var/lib /mnt/var/lib

# Generate system config
nixos-generate-config --root /mnt
```

```shell
# Install flake
sudo nix-env -f '<nixpkgs>' -iA nixUnstable git
nixos-install --flake git+https://github.com/TkPegatron/NixOS.git#wintermute --no-write-lock-file
```

```shell
# rebuild-switch flake
nixos-rebuild switch --flake git+https://github.com/TkPegatron/NixOS.git --no-write-lock-file
```