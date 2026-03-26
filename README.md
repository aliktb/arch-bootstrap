# arch-bootstrap

Minimal Arch Linux bootstrap using a single meta-package.

This repository defines **the core packages I want on any Arch system**.

Dotfiles and configuration are managed separately using chezmoi.

---

## 🧠 Philosophy

* **Arch** → OS + packages
* **Dotfiles** → configuration (chezmoi)

This repo defines the **packages layer only**.

---

## 📦 Structure

```text
arch-bootstrap/
├── PKGBUILD
└── README.md
```

The `PKGBUILD` is a **meta-package** that installs all required tools via the
`depends=()` array.

No software is compiled — it simply installs packages from Arch repos and AUR.

---

## 🚀 Quick start

### 1. Install base system + paru

```bash
sudo pacman -Syu
sudo pacman -S --needed git base-devel

git clone https://aur.archlinux.org/paru
cd paru
makepkg -si
```

---

### 2. Install bootstrap package

```bash
git clone https://github.com/aliktb/arch-bootstrap
cd arch-bootstrap
paru -U .
```

This installs:

* system base (kernel, bootloader, networking)
* CLI tools (git, neovim, fzf, etc.)
* shell environment (zsh, starship)
* dev tools (docker, fnm, pyenv)

---

### 3. Apply dotfiles

```bash
chezmoi init https://github.com/aliktb/dotfiles.git
chezmoi apply
```

---

## ⚙️ Customisation

Edit the `depends=()` array inside `PKGBUILD`:

```text
PKGBUILD
```

Then reinstall:

```bash
paru -Bi .
```

---

## 💡 Notes

* This is a **meta-package** (no build step)
* All packages come from official repos or AUR
* `paru` handles dependency resolution
* Safe to re-run at any time

---

## 🧩 Example workflow

On a fresh machine:

```bash
# install paru
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/paru.git
cd paru && makepkg -si

# install system + tools
git clone https://github.com/aliktb/arch-bootstrap
cd arch-bootstrap
paru -Bi .

# apply config
chezmoi init https://github.com/aliktb/dotfiles.git
chezmoi apply
```
