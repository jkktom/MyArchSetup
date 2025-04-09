# MyArchSetup
curl based installed software list

curl -fsSL https://ollama.com/install.sh | sh
curl -fsSL https://cdn.anythingllm.com/latest/installer.sh | sh

https://github.com/aaddrick/claude-desktop-arch#
# Clone this repository
git clone https://github.com/aaddrick/claude-desktop-arch.git
cd claude-desktop-arch

# Update checksums (needed once, or after PKGBUILD/install script changes)
updpkgsums

# Build and install the package
# This command automatically handles dependencies, builds, and installs
# Use makepkg -sci to automatically clean up build files afterwards
makepkg -si
sudo pacman -R claude-desktop