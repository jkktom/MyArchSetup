arch linux 

# Docker and MySQL 8.4.4 Setup on Arch Linux

## Action List

### 1. Install Docker
```bash
# Update system packages
sudo pacman -Syu

# Install Docker
sudo pacman -S docker

# Install required dependencies
sudo pacman -S iptables fuse-overlayfs

# Load required kernel modules
sudo modprobe overlay
sudo modprobe br_netfilter
sudo modprobe iptable_nat

# Make kernel modules load at boot
echo "overlay" | sudo tee /etc/modules-load.d/overlay.conf
echo "br_netfilter" | sudo tee /etc/modules-load.d/br_netfilter.conf
echo "iptable_nat" | sudo tee /etc/modules-load.d/iptable_nat.conf

# Start and enable Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add your user to the docker group (to run Docker without sudo)
sudo usermod -aG docker $USER
```
**Note:** After adding yourself to the docker group, you'll need to log out and log back in for the changes to take effect.

### 2. Verify Docker Installation
```bash
# Check Docker version
docker --version

# Verify Docker is working correctly
docker run hello-world
```

### 3. Set Up MySQL 8.4.4 with Docker
```bash
# Create a directory for MySQL data persistence
mkdir -p ~/mysql-data

# Pull MySQL 8.4.4 image
docker pull mysql:8.4.4

# Run MySQL container
docker run --name mysql-container \
  -e MYSQL_ROOT_PASSWORD=your_root_password \
  -e MYSQL_DATABASE=your_database \
  -e MYSQL_USER=your_user \
  -e MYSQL_PASSWORD=your_password \
  -p 3306:3306 \
  -v ~/mysql-data:/var/lib/mysql \
  -d mysql:8.4.4
```

### 4. Verify MySQL Container
```bash
# Check if container is running
docker ps

# Connect to MySQL from terminal
docker exec -it mysql-container mysql -u root -p
```

### 5. Basic MySQL Container Management
```bash
# Stop MySQL container
docker stop mysql-container

# Start MySQL container
docker start mysql-container

# Remove MySQL container (data will be preserved in ~/mysql-data)
docker rm mysql-container
```

### 6. Create Docker Compose File (Optional)
Create a file named `docker-compose.yml`:
```yaml
version: '3'
services:
  mysql:
    image: mysql:8.4.4
    container_name: mysql-container
    environment:
      MYSQL_ROOT_PASSWORD: your_root_password
      MYSQL_DATABASE: your_database
      MYSQL_USER: your_user
      MYSQL_PASSWORD: your_password
    ports:
      - "3306:3306"
    volumes:
      - ~/mysql-data:/var/lib/mysql
    restart: unless-stopped
```

Then run:
```bash
# Install docker-compose if not already installed
sudo pacman -S docker-compose

# Start MySQL with docker-compose
docker-compose up -d
```

### 7. Troubleshooting Docker Startup Issues

If you encounter errors when starting Docker like "failed to mount overlay: no such device" or "can't initialize iptables table `nat'", follow these steps:

```bash
# 1. Install required dependencies
sudo pacman -S iptables iptables-nft fuse-overlayfs

# 2. Load required kernel modules
sudo modprobe overlay
sudo modprobe br_netfilter
sudo modprobe iptable_nat

# 3. Make kernel modules load at boot
echo "overlay" | sudo tee /etc/modules-load.d/overlay.conf
echo "br_netfilter" | sudo tee /etc/modules-load.d/br_netfilter.conf
echo "iptable_nat" | sudo tee /etc/modules-load.d/iptable_nat.conf

# 4. Restart Docker service
sudo systemctl restart docker
```

If you're still having issues, check if your kernel supports these modules:
```bash
# Check if overlay is supported
grep CONFIG_OVERLAY_FS /boot/config-$(uname -r)

# Check if iptables modules are available
find /lib/modules/$(uname -r) -name '*iptable*'
```

### 8. Handling Missing Kernel Modules

If you encounter errors like `modprobe: FATAL: Module overlay not found in directory /lib/modules/...`, your kernel doesn't have the required modules. You have several options:

#### Option 1: Install the linux-lts kernel (recommended)
```bash
# Install the LTS kernel which includes most required modules
sudo pacman -S linux-lts

# Reboot to use the new kernel
sudo reboot
```

After reboot, select the LTS kernel from the boot menu.

#### Option 2: Configure Docker to use alternative storage driver
If you can't change your kernel, you can configure Docker to use an alternative storage driver:

```bash
# Create Docker daemon configuration directory
sudo mkdir -p /etc/docker

# Create daemon.json file with VFS storage driver
sudo tee /etc/docker/daemon.json > /dev/null <<EOF
{
  "storage-driver": "vfs"
}
EOF

# Restart Docker service
sudo systemctl restart docker
```

**Note:** The VFS storage driver is slower than overlay2 but doesn't require the overlay module.

#### Option 3: Use Podman instead of Docker
Podman is a Docker-compatible alternative that can run without root and doesn't require the overlay module:

```bash
# Install Podman
sudo pacman -S podman

# Use Podman commands (similar to Docker)
podman pull mysql:8.4.4
podman run --name mysql-container \
  -e MYSQL_ROOT_PASSWORD=your_root_password \
  -e MYSQL_DATABASE=your_database \
  -e MYSQL_USER=your_user \
  -e MYSQL_PASSWORD=your_password \
  -p 3306:3306 \
  -v ~/mysql-data:/var/lib/mysql \
  -d mysql:8.4.4
```

**Important Notes:**
- Replace `your_root_password`, `your_database`, `your_user`, and `your_password` with your actual values
- The MySQL data will be stored in `~/mysql-data` on your host system
- MySQL will be accessible on port 3306
