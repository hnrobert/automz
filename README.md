# automz - Oh My Zsh Automated Installer

Automated installer for Zsh + Oh My Zsh + zsh-autosuggestions + zsh-syntax-highlighting + Powerlevel10k using the included `.p10k.zsh` theme.
Supports Ubuntu/Debian (apt) and macOS (Homebrew). If Zsh/Oh My Zsh/themes/plugins are already present, the installer skips those steps.

## What it does

- Installs dependencies (zsh, git, curl, wget, fonts, locales)
- Installs Oh My Zsh (unattended) **with auto-update disabled**
- Installs plugins: zsh-autosuggestions, zsh-syntax-highlighting
- Installs Powerlevel10k theme and copies the provided `.p10k.zsh` to your home
- Updates `~/.zshrc` to use the theme and plugins (also sets `DISABLE_AUTO_UPDATE` and `DISABLE_UPDATE_PROMPT`)
- Switches your default login shell to `zsh`
- Prompts to reboot (skipped automatically inside containers)

## Usage on Ubuntu/Debian - One command install

> Make sure you are connected to the internet where `raw.githubusercontent.com` is reachable.

```bash
# Copy & paste in your bash, Enter, and the installation will run automatically
curl -fsSL https://raw.githubusercontent.com/hnrobert/automz/main/install.sh | bash
```

The script installs needed dependencies (zsh, git, curl, wget). On macOS it uses Homebrew if available (otherwise it will ask you to install the missing tools). If Zsh or Oh My Zsh is already installed, those steps are skipped. You can also run `exec zsh` or open a new terminal session after completion.

You do not need to clone the repo, it will fetch the required `.p10k.zsh` automatically.

## Usage on macOS - One command install

> On macOS, you can run the same one-liner as above. The script will use Homebrew to install missing dependencies. If Homebrew is not installed, it will prompt you to install it first.
>
> Also, make sure you are connected to the internet where `raw.githubusercontent.com` is reachable.

```zsh
# Copy & paste in your zsh, Enter, and the installation will run automatically
curl -fsSL https://raw.githubusercontent.com/hnrobert/automz/main/install.sh | zsh
```

## Test inside a container (Ubuntu 22.04)

The compose file uses upstream `ubuntu:22.04`, creates non-root user `dev`, installs `sudo`, and runs the installer as `dev`. The container then idles.

Start and view logs:

```bash
docker-compose up -d && docker-compose logs -f
```

When the instruction `[SUCCESS] All done.` appears and the container idles, you may attach to zsh as `dev` and start trying it out:

```bash
docker-compose exec --user dev automz-test zsh
```

To stop and clean up:

```bash
docker-compose down
```
