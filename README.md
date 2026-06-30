# potentpi4

![Build Status](https://github.com/OnyxJeff/potentpi4/actions/workflows/build.yml/badge.svg)
![Maintenance](https://img.shields.io/maintenance/yes/2026.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![GitHub release](https://img.shields.io/github/v/release/OnyxJeff/potentpi4)
![Issues](https://img.shields.io/github/issues/OnyxJeff/potentpi4)

**Valkyrie** is the internal playground server for my homelab, hosted on a Raspberry Pi 4.

## 📁 Repo Structure

```text
potentpi4/
├── .github/workflows/      # CI for YAML validation
├── backup_logs/            # Oldest logs from update script
├── dockprom/               # Docker container(s) for Prometheus Node Exporter for RPi
├── images/                 # Images for README files
├── logs/                   # Most recent update script logs
├── scripts/                # Auto-Updater script for RPi (can be associated with cronjob)
├── U6143_ssd1306/          # Python, C code, and script for UCTronics display screen
└── README.md               # You're reading it!
```

---

## 🧰 Services
- Testing docker container configs for RPi's

- Developing documentation on other RPi setups currently in my homelab.
  - This allows me to develop proper documentation for existing RPis without taking down my current services

- Current RPi Services in production
  - Odin
    - **Pi-hole**: Blocks ads, trackers, and telemetry across the network.
    - **Dockprom**: Collects Docker and system metrics for monitoring and analysis.
  - Mimir
    - **Dockprom**: Collects Docker and system metrics for monitoring and analysis.
    - **UniFi Controller**: Manages UniFi network devices and monitors network performance.
  - Loki
    - **Transmission Server**: Manages and downloads torrents with a web interface.
    - **Dockprom**: Collects Docker and system metrics for monitoring and analysis.

---

## 📝 Preparation

  - Install GIT (app used to download this repo onto your device)
  ```bash
  sudo apt install git -y
  ```

  - Download repo
  ```bash
  cd
  git clone https://github.com/OnyxJeff/potentpi4.git
  ```

---

## 🧪 Installing Ansible

- Download Ansible GitHub Repo
```bash
cd ~/potentpi4
git clone https://github.com/OnyxJeff/ansible.git
```

- Create extra `identity` folders
```bash
mkdir ~/potentpi4/ansible/identity/{automation,revoked,users}
```

---

## Generate an SSH Key Pair

```bash
ssh-keygen -t ed25519 -C "ansible-automation"
```
  - Explaination of flags:
    - `-t ed25519` → modern, secure key type (better than RSA)
    - `-C "ansible-automation"` → optional comment so you know which key it is
    - You'll see promtps like:
    `Enter file in which to save the key (/home/<USER>/.ssh/ansible-automation):`
  - Input `/home/<USER>/.ssh/ansible-automation` and press **Enter** to accept the location.
  - When prompted for a passphrase, you can either:
    - Enter one (more secure, but you’ll type it for every run unless you use `ssh-agent`)
    - Leave empty (convenient for automated playbooks)

### Verify your keys
```bash
ls -l ~/.ssh/ansible-automation*
```

  - You should see two files:
    - `ansible-automation` → private key (keep secret!)
    - `ansible-automation.pub` → public key (what you copy to targets)

### Copy created public key to `/ansible/identity/automation/` folder
```bash
cp ~/.ssh/ansible-automation.pub ~/potentpi4/ansible/identity/automation/ansible.pub
```

### Copy user key on host machine to `/ansible/identity/user/` folder
```bash
grep 'OnyxJeff' ~/.ssh/authorized_keys > ~/potentpi4/ansible/identity/users/onyxjeff.pub
```

---

## Install SSHPass on Control Node:
```bash
sudo apt install -y sshpass
```

---

## Please open the `ansible` folder and follow the Ansible `README.md` for this step

---

## Acknowledgements

This project uses or is inspired by the following repositories:

- [U6143_ssd1306](https://github.com/UCTRONICS/U6143_ssd1306) – Provides the C display code used in the systemd service setup.
- [Dockprom](https://github.com/stefanprodan/dockprom) – Used for Docker-based Prometheus monitoring and metrics collection.

---

📬 Maintained By
Jeff M. • [@OnyxJeff](https://www.github.com/onyxjeff)