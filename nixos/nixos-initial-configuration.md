# NixOS - Initial Configuration

After partitioning and mounting a system configuration can be generated.

## Generate

- Generate Default Configuration:

  `nixos-generate-config --root /mnt`

- Show Configuration Files:

  `ls /mnt/etc/nixos`

## configuration.nix

### General

- Everything starting with a hash in this file is a comment.
- Arguments on how to evaluate config:

  `{ config, pkgs, ... }:`

- Pull in other files used within the configuration:

  `import = [./hardware-configuration.ini];`

- To prevent code duplication you can type options instead of this:
    ```
    boot.loader.grub.enable = true;
    boot.loader.grub.version = 2;
    ```
    
    like this:

    ```
    boot.loader.grub = {
        enable = true;
        version = 2;
    };
    ```

### Boot

- UEFI - Used for large boot drives and dual booting with Windows
- Default UEFI setup:

    ```
    boot.loader.systemd-boot.enable = true;
    boot.loader.efi.canTouchEfiVariables = true;
    ```

### Networking

- Uncomment and change to correct hostname:
  `networking.hostName = "wednesday";`
- To use networkmanager:
  `networking.networkmanager.enable = true;`
- Extra's:
  - To have a fixed IP:
  ```
  networking = {
    hostname = "wednesday";
    networkmanager.enable = true;
    interfaces = {
      enp0s5 = {
        #useDHCP = true;
        ipv4.addresses = [ { # Not compatible with networkmanager
          address = "192.168.0.50";
          prefixLength = 24;
        } ];
      };
    };
    defaultGateway = "192.168.0.1";
    nameservers = [ "1.1.1.1" ];
  };
  ```

### Internationalization

Where am I? How do I work?

- Set Timezone:
  `time.timeZone = "Europe/Amsterdam";`
- Locale:
  ```
  i18n.defaultLocale = "en_US.UTF-8";
  console = {
    font = "Lat2-Terminus16";
  };
  services.xserver.layout = "us";
  ```
  
### Display Managers/Desktop Environments/Window Managers

- Default:
  ```
  services.xserver.enable = true;
  ```

- Customized:
  ```
  services = {
    xserver = {
      enable = true;
      displayManager = {
        lightdm.enable = true;
        defaultSession = "none+bspwm";
      };
      desktopManager.xfce.enable = true;
      windowManager.bspwm.enable = true;
    };
  };
  ```

### Hardware

### Users

### Packages

### StateVersion

# hardware-configuration.nix