## GK5NPFO: Tongfang - AMD iGPU and Nvidia dGPU

https://wiki.debian.org/NVIDIA%20Optimus?action=show&redirect=NvidiaGraphicsDrivers%2FOptimus

https://linuxx.info/installing-nvidia-driver-in-debian-10/

https://wiki.debian.org/NVIDIA%20Optimus

---

**From contrib non-free**

```bash
sudo apt -y install nvidia-detect
sudo apt -y install linux-headers-$(uname-r|sed 's/[^-]_-[^-]_-//')
sudo apt -y install nvidia-driver nvidia-xconfig
sudo nvidia-xconfig
```

---

**Config files**

<details>
  <summary><strong>${HOME}/.xsessionrc</strong></summary>

```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
xrandr --dpi 96
```

</details>

<details>
  <summary><strong>/etc/X11/xorg.conf</strong></summary>

```config
Section "ServerLayout"
    Identifier "SuperLayout
    Screen 0 "dGPUScreen"
    Inactive "iGPU"
EndSection

# iGPU

Section "Device"
Identifier "iGPU"
Driver "modesetting"
VendorName "AMD GPU"

# BusID "PCI:5:0:0"

EndSection

Section "Screen"
Identifier "iGPUScreen"
Device "iGPU"
EndSection
#################

# dGPU

Section "Device"
Identifier "dGPU"
Driver "nvidia"
VendorName "NVIDIA Corporation"
BusID "PCI:1:0:0"
EndSection

Section "Screen"
Identifier "dGPUScreen"
Device "dGPU"
Option "AllowEmptyInitialConfiguration" # Fix Horizontal Lines Tearing Bug, slower rendering though
Option "metamodes" "nvidia-auto-select +0+0 {ForceCompositionPipeline=On, ForceFullCompositionPipeline=On}"
EndSection
#################

```

</details>

<details>
  <summary><strong>/usr/share/gdm/greeter/autostart/optimus.desktop</strong></summary>

```config
[Desktop Entry]
Type=Application
Name=Optimus
Exec=sh -c "xrandr --setprovideroutputsource modesetting NVIDIA-0; xrandr --auto"
NoDisplay=true
X-GNOME-Autostart-Phase=DisplayServer
```

</details>

---
