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
