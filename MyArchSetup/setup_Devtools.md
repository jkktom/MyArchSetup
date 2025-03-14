i'm on arch linux GNOME yay

Required Tools:
- IntelliJ IDEA Ultimate
- Eclipse Temurin™ Latest Releases

Action List:
1. Install yay (if not already installed):
   ```bash
   sudo pacman -S --needed git base-devel
   git clone https://aur.archlinux.org/yay.git
   cd yay
   makepkg -si
   ```

2. Install IntelliJ IDEA Ultimate:
   ```bash
   yay -S intellij-idea-ultimate-edition
   ```

3. Install Eclipse Temurin (OpenJDKL):
   ```bash
   yay -S temurin-jdk
   ```

4. Verify installations:
   ```bash
   # Check Java version
   java -version
   
   # IntelliJ can be launched from the applications menu or terminal:
   intellij-idea-ultimate-edition
   ```


Notes:
- IntelliJ IDEA Ultimate requires a license
- Temurin JDK will be set as the default Java runtime
- Both applications will be available in the GNOME applications menu


