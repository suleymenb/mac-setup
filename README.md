# Mac Setup – Fully Automated macOS Bootstrap with Ansible

This repository provides a fully automated macOS setup using Ansible.
It installs Homebrew, Ansible, Zsh configuration, and preferred applications
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

```
git clone https://github.com/suleymenb/mac-setup.git && cd mac-setup && chmod +x bootstrap/bootstrap.sh && ./bootstrap/bootstrap.sh
```

This will:

1. Install Homebrew (if missing)
2. Configure PATH
3. Install pipx
4. Install ansible-core
5. Install required Ansible collections
6. Execute the Ansible playbook
7. Configure your macOS environment automatically

## What This Setup Configures

Core Tooling:
- Homebrew
- pipx
- ansible-core
- Terraform

Applications:
- iTerm2
- Rectangle
- Stats

CLI Tools:
- eza

Fonts:
- JetBrains Mono

Shell Configuration:
- Oh My Zsh
- Powerlevel10k theme
- Plugins:
  - git
  - sudo
  - zsh-autosuggestions
  - zsh-syntax-highlighting
- Custom aliases

---

## Updating Your System

To update your configuration:

```
cd ~/mac-setup
git pull
ansible-playbook playbook.yml
```

---

## Design Principles

- Idempotent configuration
- Reproducible environment
- Infrastructure-as-Code approach
- Clean separation between bootstrap and configuration
- Version-controlled system setup

This repository serves as a reproducible macOS baseline for development environments.

---

TO DO
- [ ] Add
    - [x] vimdiff
    - [x] du-dust (`cargo install du-dust`)
    - [x] midnight commander
