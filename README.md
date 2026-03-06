# Mac Setup – Fully Automated macOS Bootstrap with Ansible

This repository provides a fully automated macOS setup using Ansible.
It installs Homebrew, development tools, Rust, Zsh configuration, and preferred applications
in a reproducible and idempotent way.

---

## 1. Requirements

- macOS
- Internet connection
- Xcode Command Line Tools (required once)

If Command Line Tools are not installed, run:

```
sudo touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress && sudo softwareupdate --install --recommended
```

Wait until installation completes before continuing.

Verify installation:

```
xcode-select -p
```

It should return:

/Library/Developer/CommandLineTools

---

## 2. Quick Start (Single Command)

Run this on a fresh macOS machine:

**Main Branch:**

```
git clone https://github.com/suleymenb/mac-setup.git && cd mac-setup && chmod +x bootstrap/bootstrap.sh && ./bootstrap/bootstrap.sh
```

**Dev Branch:**

```
git clone -b dev https://github.com/suleymenb/mac-setup.git && cd mac-setup && chmod +x bootstrap/bootstrap.sh && ./bootstrap/bootstrap.sh
```

This will:

1. Install Homebrew (if missing)
2. Configure PATH
3. Install pipx
4. Install ansible-core
5. Install required Ansible collections
6. Execute the Ansible playbook
7. Configure your macOS environment automatically

---

## 3. What This Setup Configures

### Core Tooling
- Homebrew
- pipx
- ansible-core
- Terraform
- Rust

### Applications
- iTerm2
- Rectangle
- Stats

### CLI Tools
- eza
- vim (vimdiff)
- midnight commander
- du-dust (via cargo)

### Fonts
- JetBrains Mono
- Meslo LG Nerd Font

### Shell Configuration
- Oh My Zsh
- Powerlevel10k theme
- Plugins:
  - git
  - sudo
  - zsh-autosuggestions
  - zsh-syntax-highlighting
- Custom aliases:
  - `rz` - reload zshrc
  - `ls` - eza with icons and grouped directories
  - `ll` - eza long format with all files and icons
- Cargo bin directory added to PATH

### System Customization
- Dark mode enablement
- Finder hidden files visibility
- Brew auto-updates

---

## 4. Project Structure

```
mac-setup/
├── bootstrap/
│   └── bootstrap.sh          # Initial setup script
├── roles/
│   ├── homebrew/
│   │   └── tasks/
│   │       └── main.yml      # Homebrew, casks, and Rust installation
│   ├── zsh/
│   │   └── tasks/
│   │       └── main.yml      # Oh My Zsh, plugins, aliases, and cargo tools
│   └── system/
│       └── tasks/
│           └── main.yml      # macOS system customization
├── playbook.yml              # Main Ansible playbook
├── inventory.ini             # Ansible inventory
├── ansible.cfg               # Ansible configuration
└── README.md                 # This file
```

---

## 5. Updating Your System

To update your configuration:

```
cd ~/mac-setup
git pull
ansible-playbook playbook.yml
```

Or run specific roles with tags:

```
ansible-playbook playbook.yml --tags homebrew
ansible-playbook playbook.yml --tags zsh
ansible-playbook playbook.yml --tags system
```

---

## 6. Design Principles

- **Idempotent configuration** - Safe to run multiple times
- **Reproducible environment** - Same setup every time
- **Infrastructure-as-Code approach** - Everything is version controlled
- **Clean separation of concerns** - Organized by role (homebrew, zsh, system)
- **Version-controlled system setup** - Track all changes in git

This repository serves as a reproducible macOS baseline for development environments.

---

## 7. Customization

You can customize your setup by editing:

- `roles/homebrew/tasks/main.yml` - Add/remove packages and casks
- `roles/zsh/tasks/main.yml` - Modify shell configuration, aliases, and cargo tools
- `roles/system/tasks/main.yml` - Add more macOS system customizations
- `playbook.yml` - Include/exclude roles

---

## License

MIT