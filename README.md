# Terminal KDE system information
A CLI tool to display KDE troubleshooting information in the terminal

- Nice visual output without, faster than Systemsettings
- No sudo permissions required (no `dmidecode`)
- Clipboard copying on Wayland and X11 (`xl-copy`, `xsel` or `xclip`)
- Basic dependencies, works on Fedora Kinoite out-of-the-box (no `inxi`, `neofetch`, `fastfetch`,...)
- Add a Packagename to display its version too (if an app causes Trouble)
  - supports `DPKG` (Ubuntu, Debian, Linux Mint, PopOS)
  - `RPM` (Fedora, OpenSuse, RockyLinux, CentOS, RHEL)
  - `Pacman` (Arch), `Pamac` (Manjaro), `Yay` (AUR)
  - `Emerge` (Gentoo)
  - `Flatpak` (Online only currently)
  - `Snap` (yes I did it)
  - `APK` (Alpine)
  - `Nix` (NixOS)


### Example output:
```
/v/h/user ❯❯❯ sysinfo -h

--- System-Info ---

Display KDE Plasma System Information from the Terminal.

Add an Application-name to add its information.
Example:
sysinfo konsole

Clipboard copying on Wayland and X11 supported.

Use -h to show this help

--------------------
/v/h/user ❯❯❯ sysinfo konsole

Specified App: konsole5-part-22.12.3-1.fc38.x86_64
konsole5-22.12.3-1.fc38.x86_64

--- Software ---  
OS: Fedora Linux 38.20230508.0 (Kinoite) 
KDE Plasma: 5.27.4 
KDE Frameworks: 5.105.0 
Qt: 5.15.9 
Kernel: 6.2.14-300.fc38.x86_64 
Compositor: Wayland 
 
--- Hardware --- 
CPU: AMD Ryzen 5 PRO 3500U w/ Radeon Vega Mobile Gfx 
RAM: 13.5 GB 
GPU: AMD Radeon Vega 8 Graphics
Video memory: 2048MB 
 
Copy to clipboard? (y/n) y

🗒 Copied to clipboard!
```

## Install:
```
wget https://raw.githubusercontent.com/trytomakeyouprivate/KDE-sysinfo-CLI/main/sysinfo -P ~/.bin && chmod +x ~/.bin/sysinfo && /usr/bin/bash ~/.bin/sysinfo
```

### To-Do
- offline Flatpak app infos
  - complex problem, needs exact appID, something like
  - `flatpak search $1 | awk 'NR==2 {print $3}' | xargs flatpak info`
  - `flatpak info $(flatpak search $1 | sed -n '2s/[^\t]*\t[^\t]*\t//p')`
- more efficient package manager usage (detection, configfile/ self-modification)
- `-v` Verbose version with more output (but maybe inxi is better here)
  - CPU: used drivers
  - RAM: usable, swap
  - GPU: OpenGL, Vulkan, drivers
