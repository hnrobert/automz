# hnrobert-omz-installer

Automated installer for Zsh + Oh My Zsh + zsh-autosuggestions + zsh-syntax-highlighting + Powerlevel10k using the included `.p10k.zsh` theme.

## What it does

- Installs dependencies (zsh, git, curl, wget, fonts, locales)
- Installs Oh My Zsh (unattended)
- Installs plugins: zsh-autosuggestions, zsh-syntax-highlighting
- Installs Powerlevel10k theme and copies the provided `.p10k.zsh` to your home
- Updates `~/.zshrc` to use the theme and plugins
- Switches your default login shell to `zsh`
- Prompts to reboot (skipped automatically inside containers)

## Usage on a host (Ubuntu/Debian)

You do not need to clone the repo. Download and run the installer directly; it will fetch the required `.p10k.zsh` automatically.

```bash
curl -fsSL https://raw.githubusercontent.com/hnrobert/hnrobert-omz-installer/main/install.sh -o install.sh
chmod +x install.sh
./install.sh
```

The script installs needed dependencies (git, curl, etc.) if they are missing. When finished, it asks whether to reboot. You can also run `exec zsh` or open a new terminal session.

## Test inside a container (Ubuntu 22.04)

The included compose file starts an Ubuntu 22.04 container, mounts the repo, and runs the installer via entrypoint.

```bash
docker-compose up -d # build flag is harmless with no Dockerfile present
docker-compose exec hnrobert-omz-installer-test zsh
```

To stop and clean up:

```bash
docker-compose down
```

## Font recommendation

For best glyph rendering with Powerlevel10k, install a Nerd Font such as MesloLGS NF:
<https://github.com/romkatv/powerlevel10k#fonts>
