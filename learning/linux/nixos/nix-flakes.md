# 🌟 Nix Flakes Tutorial

## Introduction

- **What are Flakes?**
  - Experimental Nix feature for reproducible environments
  - Enforces standardized project structure
  - Uses `flake.lock` for dependency pinning
  - Works with Nix commands: `nix run`, `nix build`, `nix develop`

---

## Getting Started

### Enable Flakes

```bash
# For NixOS
nix.settings.experimental-features = [ "nix-command" "flakes" ];

# For Home Manager
home.file.".config/nix/nix.conf".text = ''
  experimental-features = nix-command flakes
'';

# Manual config
echo "experimental-features = nix-command flakes" >> /etc/nix/nix.conf
```

### Initialize Flake

```bash
mkdir my-flake && cd my-flake
nix flake init
```

### Flake Structure

#### Basic `flake.nix`

```nix
{
  description = "My first flake";
  
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs";
  };

  outputs = { self, nixpkgs }:
    let
      pkgs = nixpkgs.legacyPackages.x86_64-linux;
    in {
      packages.x86_64-linux.default = pkgs.hello;
      devShells.x86_64-linux.default = pkgs.mkShell { /* ... */ };
    };
}
```

### Key Concepts

#### Outputs & Commands

| Command          | Looks For                        |
| ---------------- | -------------------------------- |
| `nix run`        | `packages.<system>.default`      |
| `nix build`      | `packages.<system>.default`      |
| `nix develop`    | `devShells.<system>.default`     |
| `nixos-rebuild`  | `nixosConfigurations.<hostname>` |
| **Home Manager** | homeConfigurations.<username>    |

#### Inputs

- Add dependencies in `inputs` section
- Example with multiple nixpkgs versions:

```nix
inputs = {
  nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
  nixpkgs-stable.url = "github:NixOS/nixpkgs/release-23.05";
};
```
### Advanced Usage

#### Development Shell 

```nix
devShells.x86_64-linux.default = pkgs.mkShell {
  buildInputs = [ pkgs.neovim pkgs.nodejs ];
};
```

**Run with:** `nix develop`

#### System Configuration

```nix
nixosConfigurations.nixos = nixpkgs.lib.nixosSystem {
  system = "x86_64-linux";
  modules = [ ./configuration.nix ];
};
```

**Rebuild with:** `nixos-rebuild switch --flake .#nixos`

### Lock File Magic 

- Auto-generated `flake.lock` pins versions
- Update dependencies: `nix flake update`
- Check versions: `nix flake metadata`

### Common Pitfalls 

> [!WARNING] 
> **GIT TRACKING**
> - All files must be staged in Git
> - Untracked files won't be detected
     
> [!WARNING] 
> **PURE EVALUATION**
> - No network access during evaluation
> - All dependencies must be declared in `flake.nix`

## Summary

- Flakes bring reproducibility to Nix
- Centralized dependency management
- Works across all Nix use cases (packages, shells, systems)
- `flake.lock` ensures consistent environments
     

## Resources

- [Nix Flakes Wiki](https://nixos.wiki/wiki/Flakes)
- `man flake`
- `nix flake --help`
     

#nix #flakes #tutorial #reproducibility #devops 
     


