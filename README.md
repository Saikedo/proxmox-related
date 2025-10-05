# Proxmox Related Setup

This repository contains notes and scripts related to running Proxmox and related services.

---

## 🚀 Starting Scripts
```bash
sudo apt update
sudo apt upgrade
```

## 🚀 Install Docker

```bash
# Download Docker installation script
curl -fsSL https://get.docker.com -o get-docker.sh

# Run the script with sudo privileges
sudo sh get-docker.sh

# Remove the installer (no longer needed after install)
rm get-docker.sh

sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

## Docker Portainer Agent
```bash
bash <<'SCRIPT'
set -euo pipefail

echo "→ Working in: $PWD"

DOCKER_DIR="./docker"
AGENT_DIR="$DOCKER_DIR/portainer-agent"
mkdir -p "$AGENT_DIR"
echo "✓ Ensured $AGENT_DIR exists"

COMPOSE_FILE="$AGENT_DIR/docker-compose.yml"
if [[ -f "$COMPOSE_FILE" ]]; then
  cp -f "$COMPOSE_FILE" "$COMPOSE_FILE.bak.$(date +%s)"
  echo "ℹ️  Existing docker-compose.yml found. Backed up."
fi

cat > "$COMPOSE_FILE" <<'YAML'
services:
  agent:
    image: portainer/agent:latest
    container_name: portainer-agent
    restart: unless-stopped
    ports:
      - "9001:9001"     # Agent listens here
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /var/lib/docker/volumes:/var/lib/docker/volumes
YAML

echo "✓ Wrote $COMPOSE_FILE"

# Find compose command
if command -v docker >/dev/null 2>&1 && docker compose version >/dev/null 2>&1; then
  COMPOSE_CMD="docker compose"
elif command -v docker-compose >/dev/null 2>&1; then
  COMPOSE_CMD="docker-compose"
else
  echo "❌ Neither 'docker compose' nor 'docker-compose' is available. Please install Docker Compose."
  exit 1  # exits this subshell only; your SSH session stays alive
fi

echo "→ Running: $COMPOSE_CMD up -d"
(
  cd "$AGENT_DIR"
  $COMPOSE_CMD up -d
)

echo "🎉 Done! Portainer Agent should now be running (port 9001)."
SCRIPT
```


## Terminal Setup


```bash
# Install zsh
sudo apt install -y zsh

# Set it as main editor
chsh -s $(which zsh)

# Install Oh-My-Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Install Powerlevel10k Theme
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# Git prompt
git clone https://github.com/olivierverdier/zsh-git-prompt ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/git-prompt

# Autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# Syntax highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# You-should-use
git clone https://github.com/MichaelAquilina/zsh-you-should-use ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/you-should-use

# zsh-bat
git clone https://github.com/fdellwing/zsh-bat.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-bat

# Change theme
sed -i 's/^ZSH_THEME=.*/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc

# Change Plugins
sed -i '/^plugins=/c\plugins=(\
  git \
  yarn \
  xcode \
  git-prompt \
  gitfast \
  zsh-autosuggestions \
  zsh-syntax-highlighting \
  you-should-use \
  zsh-bat \
)' ~/.zshrc


# Reload
source ~/.zshrc
```

To reconfigure styles at any point
```bash
p10k configure
```


## 🚀 Network Share
```bash
sudo apt install cifs-utils
sudo nano /etc/fstab
```

# proceed to add this to remote shares
```bash
# Remote Shares
//10.0.0.100/data /data cifs uid=1000,gid=1000,username=user,password=password,iocharset=utf8 0 0
```
