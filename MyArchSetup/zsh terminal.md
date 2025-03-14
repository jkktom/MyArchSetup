# ZSH Installation and Setup on Arch Linux

ZSH (Z Shell) is a powerful shell with improved features over the default Bash shell, including better tab completion, theming support, and plugin capabilities.

## Action List

### 1. Check if ZSH is Already Installed

```bash
# Method 1: Check using pacman
pacman -Qi zsh || echo "ZSH is not installed"

# Method 2: Check if the ZSH binary exists
which zsh || echo "ZSH binary not found"

# Method 3: Check available shells
cat /etc/shells | grep zsh
```

### 2. Install ZSH

```bash
# Update system packages
sudo pacman -Syu

# Install ZSH
sudo pacman -S zsh
```

### 3. Verify ZSH Installation

```bash
# Check ZSH version
zsh --version

# Verify ZSH is in the list of available shells
cat /etc/shells | grep zsh
```

### 4. Make ZSH Your Default Shell

```bash
# Change your default shell to ZSH
chsh -s $(which zsh)
```

**Note:** You'll need to log out and log back in for the shell change to take effect.

### 5. Install Oh My ZSH (Optional but Recommended)

Oh My ZSH is a framework for managing your ZSH configuration with themes and plugins.

```bash
# Install git if not already installed
sudo pacman -S git

# Install Oh My ZSH
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### 6. Configure ZSH

The main ZSH configuration file is `~/.zshrc`. After installing Oh My ZSH, this file will be created automatically.

#### Customize Theme

Edit `~/.zshrc` and change the ZSH_THEME line:

```bash
# Open .zshrc in your preferred editor
nano ~/.zshrc

# Find and modify the theme (popular options: robbyrussell, agnoster, bira, avit)
# ZSH_THEME="robbyrussell"
# Change to:
ZSH_THEME="agnoster"  # or any other theme you prefer
```

#### Install Powerline Fonts (for certain themes)

If you choose a theme like agnoster that requires special fonts:

```bash
# Install powerline fonts
sudo pacman -S powerline-fonts
```

### 7. Install Useful Plugins

Edit `~/.zshrc` and update the plugins line:

```bash
# Default plugins
plugins=(git)

# Enhanced plugins
plugins=(git zsh-autosuggestions zsh-syntax-highlighting docker sudo)
```

Install additional plugins:

```bash
# Install zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# Install zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 8. Apply Changes

```bash
# Source your updated configuration
source ~/.zshrc

# Or simply restart your terminal
```

### 9. Additional Customizations

#### Add Aliases

Edit `~/.zshrc` and add custom aliases:

```bash
# Example aliases
alias zshconfig="nano ~/.zshrc"
alias ohmyzsh="nano ~/.oh-my-zsh"
alias ll="ls -la"
alias update="sudo pacman -Syu"
```

#### Configure History Settings

Edit `~/.zshrc` and add:

```bash
# History configuration
HISTSIZE=10000
SAVEHIST=10000
HISTFILE=~/.zsh_history
setopt appendhistory
setopt sharehistory
setopt incappendhistory
```

### 10. Troubleshooting

#### Fix Font Issues
If you see strange characters in your prompt:
- Make sure powerline fonts are installed
- Configure your terminal to use a powerline-compatible font

#### Reset to Default ZSH
If you want to remove Oh My ZSH:
```bash
uninstall_oh_my_zsh
```

#### Return to Bash
If you want to switch back to Bash:
```bash
chsh -s $(which bash)
```

#### Resolving Pacman Lock File Error

If you encounter this error when installing ZSH:
```
error: failed to init transaction (unable to lock database)
error: could not lock database: File exists
  if you're sure a package manager is not already
  running, you can remove /var/lib/pacman/db.lck
```

Follow these steps to resolve it:

1. **Check if another package manager is running**:
   ```bash
   ps aux | grep pacman
   ```

2. **If no other pacman process is running**, remove the lock file:
   ```bash
   sudo rm /var/lib/pacman/db.lck
   ```

3. **Try installing ZSH again**:
   ```bash
   sudo pacman -S zsh
   ```

4. **If you're still having issues**, try refreshing the package databases:
   ```bash
   sudo pacman -Syy
   sudo pacman -S zsh
   ```

5. **In case of corrupted databases**, you might need to:
   ```bash
   sudo rm -r /var/lib/pacman/sync
   sudo pacman -Syy
   sudo pacman -S zsh
   ``` 