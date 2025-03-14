this is just the start
i'm new to arch linux, to linux overall. 

## Installing Discord from AUR using git clone and makepkg

### Initial Installation
1. First, make sure you have the necessary tools installed:
   ```
   sudo pacman -S --needed git base-devel
   ```

2. Clone the AUR repository:
   ```
   git clone https://aur.archlinux.org/discord_arch_electron.git
   ```

3. Navigate to the cloned directory:
   ```
   cd discord_arch_electron
   ```

4. Build and install the package:
   ```
   makepkg -si
   ```
   The `-si` flags mean:
   - `s`: Install needed dependencies
   - `i`: Install the package after building it

5. After installation completes, you can launch Discord from your application menu or by typing `discord` in the terminal.

### Updating Discord
To update Discord when a new version is available:

1. Navigate to the directory where you cloned the repository:
   ```
   cd discord_arch_electron
   ```

2. Pull the latest changes from the AUR:
   ```
   git pull
   ```

3. Rebuild and reinstall the package:
   ```
   makepkg -si
   ```

This process needs to be done manually whenever you want to check for updates. The package won't automatically update through the regular system updates.

#### Important Notes About Updates:

- **When to update**: Yes, when Discord notifies you about an update within the app, that's a good time to perform these update steps.

- **If you deleted the repository**: If you deleted the original cloned repository, simply clone it again using the same command from step 2 of the installation process.

- **No conflicts**: This update process won't cause conflicts with your existing installation. The `makepkg -si` command will properly replace the old version with the new one.

- **Clean build (if needed)**: If you encounter issues during an update, you can clean the build directory before rebuilding:
  ```
  rm -rf pkg/ src/ *.pkg.tar.zst
  makepkg -si
  ```

- **Configuration preservation**: Your Discord settings, login information, and other user data will be preserved during updates as they're stored in your home directory.

Note: This method is the manual way to install AUR packages. For future reference, you might want to consider using an AUR helper like `yay` or `paru` to simplify the process of both installation and updates. With an AUR helper, you could update all packages (including AUR packages) with a single command.

## Installing and Using Yay (AUR Helper)

Yay is a popular AUR helper that simplifies installing and updating packages from the AUR. Here's how to install it:

### Installing Yay

1. Make sure you have the necessary tools installed:
   ```
   sudo pacman -S --needed git base-devel
   ```

2. Clone the yay repository:
   ```
   git clone https://aur.archlinux.org/yay.git
   ```

3. Navigate to the cloned directory:
   ```
   cd yay
   ```

4. Build and install yay:
   ```
   makepkg -si
   ```

5. Verify the installation:
   ```
   yay --version
   ```

### Installing Visual Studio Code with Yay

Once yay is installed, you can use it to install Visual Studio Code:

1. Install VS Code using yay:
   ```
   yay -S visual-studio-code-bin
   ```
   
   Note: There are several VS Code packages available in the AUR:
   - `visual-studio-code-bin`: Microsoft's official binary release
   - `code`: The open-source version (VS Code OSS)
   - `visual-studio-code-insiders-bin`: The insider/beta version

2. During the installation, yay will:
   - Ask you to confirm the installation
   - Show you the PKGBUILD file (you can review it for security)
   - Download dependencies
   - Build and install the package

3. After installation, you can launch VS Code from your application menu or by typing `code` in the terminal.

### Updating Packages with Yay

To update all packages, including those from the AUR:
```
yay -Syu
```

To update only AUR packages:
```
yay -Sua
```

This is much more convenient than the manual method we used for Discord, as yay handles all the git pulling, building, and installing automatically.