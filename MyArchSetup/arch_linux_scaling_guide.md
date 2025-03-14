# Setting Up 150% Scaling in Arch Linux with GNOME

This guide provides instructions for achieving 150% scaling on a 2K monitor in Arch Linux using GNOME.

## Action List for 150% Scaling with GNOME Tweaks

### 1. Install GNOME Tweaks

```bash
sudo pacman -S gnome-tweaks
```

> **Note:** When launching GNOME Tweaks, you may see an alert that "Extension has moved to GNOME Extensions." This is normal and expected. The Extensions functionality was separated from GNOME Tweaks into its own application, but this doesn't affect the scaling and font settings we need.

### 2. Launch GNOME Tweaks

You can launch it from the application menu or run:

```bash
gnome-tweaks
```

### 3. Adjust Scaling with GNOME Tweaks

1. Open GNOME Tweaks
2. Navigate to the "Fonts" section
3. Look for "Scaling Factor" 
4. Set it to 1.5 (for 150% scaling)
5. Click "Apply"
6. Log out and log back in for changes to take full effect

### 4. Additional Font Adjustments (Optional)

While in the Fonts section of GNOME Tweaks, you can also:
- Increase individual font sizes
- Change font hinting and antialiasing for better readability
- Enable text scaling for specific applications

### 5. Enable Fractional Scaling (Alternative Method)

If you prefer using GNOME's built-in fractional scaling:

```bash
gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"
```

Then:
1. Log out and log back in
2. Open Settings → Displays
3. Look for "Scale" option which should now show fractional options
4. Select 150%

### 6. Make Changes Permanent

The changes made through GNOME Tweaks will persist across reboots. However, if you used the gsettings command for fractional scaling, you may want to add it to your startup applications:

1. Open "Startup Applications"
2. Click "Add"
3. Name: "Enable Fractional Scaling"
4. Command: `gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"`
5. Click "Add"

### 7. Fine-tuning (If Needed)

If some applications still appear too small or too large:
- For GTK applications: Edit ~/.config/gtk-3.0/settings.ini and add:
  ```
  [Settings]
  gtk-font-name = Your Font 11
  ```
- For Qt applications: Install `qt5ct` and set environment variable:
  ```
  echo "export QT_QPA_PLATFORMTHEME=qt5ct" >> ~/.profile
  ```
  Then configure Qt apps using the qt5ct application

### 8. Troubleshooting

If you encounter issues:
- Check if you're using X11 or Wayland: `echo $XDG_SESSION_TYPE`
- Some applications may not scale properly with fractional scaling
- Try logging out and back in after making changes
- If scaling causes performance issues, consider using font scaling only

### 9. Reverting Changes

To revert font scaling in GNOME Tweaks:
1. Open GNOME Tweaks
2. Go to Fonts section
3. Set Scaling Factor back to 1.0

To disable fractional scaling:
```bash
gsettings reset org.gnome.mutter experimental-features
```

## Additional Resources

- [Arch Linux Wiki - HiDPI](https://wiki.archlinux.org/title/HiDPI)
- [GNOME Wiki - Fractional Scaling](https://wiki.gnome.org/Initiatives/FractionalScaling)
- [Arch Linux Forums](https://bbs.archlinux.org/) 

asdfasdf
.
asdfasdf
asdfasdf
sadfasdf
sdfasdf
asdfasdfasdf
asdfasdf
asdfasdf
asdfasdfasdfasdfasdfasdf
asdfasdf
asdfasdf
asasdfasdfasdfasdf
asdfasdf
asdf

dfcasdf
sesesesesesesesesese