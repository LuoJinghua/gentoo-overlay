# gentoo-overlay
My personal portage overlay

## step by step for enabling libglvnd for nvidia-drivers & xorg-server

* unmask the libglvnd for mesa
```
$ cat /etc/portage/profile/package.use.mask 
media-libs/mesa -libglvnd
```
* enable the libglvnd use globally
```
$ sudo euse -E libglvnd
```

* uninstall the eselect-opengl
```
$ sudo emerge -C eselect-opengl
```

* reinstall mesa, xorg-server and nvidia-drivers
```
$ sudo emerge -v1 mesa xorg-server nvidia-drivers
```

* enable the AllowNVIDIAGPUScreens option for X server
```
$ cat /etc/X11/xorg.conf.d/01-nvidia-offload.conf 
Section "ServerLayout"
    Identifier "layout"
    Option "AllowNVIDIAGPUScreens"
EndSection
```

* reboot
