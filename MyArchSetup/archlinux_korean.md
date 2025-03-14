# Enabling Korean Input on Arch Linux

## Problem
I installed noto font ckj in this machine when I installed this arch linux. When I do super space the korean shows in system but actually cannot type in any korean letters. how can I fix this?

## Solution

### 1. Install IBus and Korean Hangul Input Method

```bash
sudo pacman -S ibus ibus-hangul
```

### 2. Configure System Environment Variables

Create a system-wide configuration file to set IBus as the default input method:

```bash
echo -e 'export GTK_IM_MODULE=ibus\nexport QT_IM_MODULE=ibus\nexport XMODIFIERS=@im=ibus' | sudo tee /etc/profile.d/ibus.sh
```

Output:
```
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
```

### 3. Set Up IBus Autostart

Create an autostart entry for IBus daemon:

```bash
mkdir -p ~/.config/autostart
echo -e '[Desktop Entry]\nName=IBus Daemon\nComment=IBus Daemon\nExec=ibus-daemon -drx\nTerminal=false\nType=Application\nCategories=System;Utility;\nStartupNotify=false\nX-GNOME-AutoRestart=false\nX-GNOME-Autostart-Phase=Applications' > ~/.config/autostart/ibus.desktop
```

### 4. Start IBus Daemon for Current Session

```bash
ibus-daemon -drx
```

### 5. Configure IBus Preferences

Open IBus preferences:

```bash
ibus-setup
```

In the IBus Preferences window:
- Go to the "Input Method" tab
- Click "Add" and select "Korean" → "Hangul"
- Click "Add" to add it to your input methods

### 6. Configure GNOME Input Sources

Open GNOME Settings for region and language:

```bash
gnome-control-center region
```

Note: You might see this warning which can be ignored:
```
WARNING: The direct access to `region` is now deprecated. Please, use `system region` instead.
```

In the GNOME Settings window:
- Go to "Region & Language"
- Under "Input Sources", click the "+" button
- Select "Korean" and then "Korean (Hangul)"
- Click "Add"

### 7. Switching Between Input Methods

- Use Super+Space (default in GNOME) to switch between input methods
- Or click the input method indicator in the top bar
- Once Korean input is active, toggle between Hangul and English by pressing the right Alt key

### 8. Restart Your Session

For all changes to take effect properly, log out and log back in.

## Troubleshooting

If you're still having issues:

1. Check if the IBus daemon is running:
   ```bash
   ps aux | grep ibus-daemon
   ```

2. Verify that the Korean language pack is properly installed:
   ```bash
   ibus list-engine | grep hangul
   ```

3. Make sure your keyboard shortcut for switching input methods is properly configured in GNOME Settings.

## Installing Adobe Korean Fonts

To enhance your Korean typing experience with high-quality fonts, you can install Adobe's Korean fonts:

### Adobe Source Han Sans (Sans-serif Korean Font)

```bash
sudo pacman -S adobe-source-han-sans-kr-fonts
```

This package provides Adobe Source Han Sans, a clean sans-serif font designed for Korean text.

### Adobe Source Han Serif (Serif Korean Font)

```bash=
sudo pacman -S adobe-source-han-serif-kr-fonts
```

This package provides Adobe Source Han Serif, an elegant serif font for Korean text.

### Pan-CJK Collection (Complete Set)

If you need comprehensive support for Chinese, Japanese, and Korean:

```bash
sudo pacman -S adobe-source-han-sans-otc-fonts adobe-source-han-serif-otc-fonts
```

These packages contain the complete OpenType/CFF Collection (OTC) fonts that support all CJK languages in a single font file.

### Verifying Font Installation

After installing the fonts, you can verify they're available with:

```bash
fc-list | grep -i "adobe.*korean\|source han.*kr"
```

### Setting Adobe Fonts as Default for Korean Text

To set Adobe Source Han as your default font for Korean text, create or edit `~/.config/fontconfig/fonts.conf`:

```bash
mkdir -p ~/.config/fontconfig
nano ~/.config/fontconfig/fonts.conf
```

Add the following content:

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match>
    <test name="lang" compare="contains">
      <string>ko</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>Source Han Sans K</string>
    </edit>
  </match>
</fontconfig>
```
Save the file and update the font cache:

```bash
fc-cache -fv
```

Log out and log back in for the changes to take effect.