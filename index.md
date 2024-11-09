---
theme: ./tokyo_night.json
---

# Getting Started w/ Nix

Reproducible Package Management with Flakes

---

# Introduction to the Nix Ecosystem

- **Nix**: Functional package manager for reproducible environments
- **NixOS**: Linux distribution based on Nix
- **Nix Language**: Functional language for package and environment configurations

---

# Why Use Nix as a Package Manager?

- **Reproducibility**: Ensures consistency across environments
- **Isolation**: Packages are isolated to prevent conflicts
- **Rollbacks & Versioning**: Enables easy rollbacks and version pinning
- **Cross-Platform**: Runs on Linux, macOS, and other Unix-based systems

---

# Nix Expressions and the Nix Store

- **Nix Expressions**: Declarative files that define packages and environments.
- **The Nix Store**: Located at `/nix/store`, where each package version is isolated by unique paths.

---

# Installing Nix and Enabling Flakes

- Installation Command:

```bash
sh <(curl -L https://nixos.org/nix/install) --daemon
```

- Enable Flakes: Add this to `~/.config/nix/nix.conf`:

```ini
experimental-features = nix-command flakes
```

---

# Basic Nix Commands with Flakes

- **Install a Package**:

```bash
nix profile install nixpkgs#<package>
```

- **Remove a Package**:

```bahs
nix profile remove <index>
```

- **Search Packages**:

```bash
nix search nixpkgs <query>
```

---

# Working w/ Flakes: Structure and Lock Files

- **flake.nix**: Describes dependencies and environments.
- **flake.lock**: Locks dependencies to specific versions.
- **Updating Dependencies**:

```bash
nix flake update
```

---

# Advanced Package Management

- **Layered Profiles**: Install packages in isolated layers.
- **Examples**:

  - **Install**:

  ```bash
  nix profile install nixpkgs#htop
  ```

  - **List**:

  ```bash
  nix profile list
  ```

  - **Remove**:

  ```bash
  nix profile remove <index>
  ```

---

# Setting Up Dev Environments with Flakes

- **Define devShell in `flake.nix`**:

```nix
{
  description = "A development environment w/ figlet";

  inputs.nixpkgs.url = "github:NixOS/nixpkgs";

  outputs = { self, nixpkgs }: {
    devShell.aarch64-darwin.default = nixpkgs.legacyPackages.aarch64-darwin.mkShell {
      buildInputs = [
        nixpkgs.legacyPackages.aarch64-darwin.figlet
      ];
    };
  };
}
```

- **Run**:

```bash
nix develop
```

---

# Case Study: Setting Up a Project with Nix

- Define project dependencies and environment in `flake.nix`.
- Run `nix develop` to create a reproducible dev environment.

---

# Conclusion and Resources for Learning Nix

- **Takeaways**:

  - Nix provides reproducibility and consistency in package management.
  - Flakes offer standardized project structures and version-locking.

- **Resources**:

  - Nix & NixOS
  - Nix Reference Manual
  - NixOS Search Packages

---

# Thanks!
