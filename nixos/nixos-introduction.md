# NixOS - Introduction

1. Linux Distribution based on Nix package manager.
2. Supports declarative reproducible system configurations.
3. "Unbreakable" -> Boot to specific configuration generations, e.g. reproducible.
4. nix-store - No `/lib` & `/usr/lib`. Almost non-existent `/bin` & `/usr/bin`. Symlinks to `/nix/store`.
5. nix-env - Install packages at user level without having to change system state.