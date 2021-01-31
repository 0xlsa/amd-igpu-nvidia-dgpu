GK5NPFO: Tongfang - AMD iGPU and Nvidia dGPU

https://linuxx.info/installing-nvidia-driver-in-debian-10/
https://wiki.debian.org/NVIDIA%20Optimus

# Add contrib non-free
sudo apt -y install nvidia-detect
sudo apt -y install linux-headers-$(uname-r|sed 's/[^-]*-[^-]*-//')
sudo apt -y install nvidia-driver nvidia-xconfig
sudo nvidia-xconfig

/etc/X11/xorg.conf
/usr/share/gdm/greeter/autostart/optimus.desktop
${HOME}/.xsessionrc
