# dotfiles Configuration

This repository stores my personal **Bash and system configuration files** for backup, portability, and quick setup across systems. It includes configurations for:

* **Bash**: `.bashrc`, `.bash_aliases`
* **Tmux**: `.tmux.conf`
* **Starship prompt**: `~/.starship.toml`
* **Other configs** (optional, tracked as needed)

The goal of this repo is to **centralize all important dotfiles** and make them easy to deploy. Using a **bare Git repository** allows you to keep files in your home directory without extra folder nesting or clutter.

---

## 📝 Prerequisites

Before using this repo, ensure you have:

* Linux or macOS system
* `tmux` installed (for `.tmux.conf`)
* `starship` prompt installed (for `.starship.toml`)
* `git` installed

Optional but useful:

```bash
sudo apt install coreutils
sudo apt install tree
```

---

## ⚡ Setup Steps

### 1️⃣ Clone the repository as a bare repo

```bash
git clone --bare git@github.com:ankushhKapoor/dotfiles $HOME/.dotfiles
```

---

### 2️⃣ Set up alias for managing dotfiles

Add this temporarily or permanently to your `.bashrc`:

```bash
alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
```

Now you can run commands like:

```bash
dotfiles status
dotfiles add <file>
dotfiles commit -m "Message"
```

---

### 3️⃣ Checkout files into home

```bash
dotfiles checkout
```

> ⚠️ If any files already exist, back them up first to avoid conflicts.

---

### 4️⃣ Optional: Symlink files for programs expecting specific paths

**Starship prompt:**

```bash
ln -s ~/.starship.toml ~/.config/starship.toml
```

**Tmux** (only if you want to keep `.tmux/` directory):

```bash
ln -s ~/.tmux.conf ~/.tmux/tmux.conf
```

> If your `.tmux.conf` is already in `$HOME`, the symlink is **not necessary**.

---

### 5️⃣ Verify setup

```bash
dotfiles status
```

* Only the files you explicitly track should appear.
* Everything else in your home directory remains untracked.

---

# Bash Config

## 🔧 Custom Command: `lsx`

Enhanced `ls` command that shows:

* Total size of current or given directory
* Size and creation date of each file/folder
* `/` for directories, `*` for executables
* Error if directory doesn't exist

### ▶️ Usage

```bash
lsx         # List visible files
lsx -a      # Include hidden files
lsx dir/    # List files in a specific directory
```

### 📌 Example

```bash
lsx abcd
```

**Output:**

```text
Total: 1388653749 bytes
README.md                   723 bytes  01-06-2025 20:38
c/                   1073969817 bytes  11-05-2025 17:08
tools/                    22974 bytes  11-05-2025 17:33
```

**If the path is invalid:**

```text
lsx: 'abcd' - No such directory exists
```

