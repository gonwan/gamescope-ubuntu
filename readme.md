# gamescope-ubuntu
Ubuntu 24.04 does not come up with gamescope. The most recent version is 3.14.24, that depends on wayland 1.22. Futher versions bumped wayland to 1.23.

### Dependencies
```
# sudo apt-get install libpipewire-0.3-dev libx11-dev libwayland-dev libvulkan-dev wayland-protocols libx11-xcb-dev libglm-dev libxdamage-dev libxcomposite-dev libxcursor-dev libxxf86vm-dev libxtst-dev libxres-dev libxmu-dev libdrm-dev libeis-dev libxkbcommon-dev libcap-dev libsdl2-dev libstb-dev libavif-dev libpixman-1-dev libseat-dev libinput-dev libxcb-composite0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-res0-dev glslang-tools libdisplay-info-dev
```

### Build
- Checkout gamescope
```
# git clone https://github.com/ValveSoftware/gamescope.git
# cd gamescope
# git checkout 3.14.24
# git submodule update --init
```
- Apply patches and build, see [1](https://github.com/ValveSoftware/gamescope/pull/1335), [2](https://github.com/ValveSoftware/gamescope/commit/ff4536106e80f285983acb562e43233ddb4e7571) for patch details.
```
# cd ..
# git clone https://github.com/gonwan/gamescope-ubuntu.git
# cp -r gamescope-ubuntu/debian gamescope/
# cd gamescope
# QUILT_PATCHES=debian/patches quilt push -a
# fakeroot debian/rules binary
```

### Install and run
```
# cd ..
# sudo gdebi gamescope_3.14.24-1_amd64.deb
# gamescope vkcube
```

### Steam launch options
```
# gamescope --mangoapp -w 1920 -h 1200 -W 2880 -H 1800 -f -F fsr -- %command%
# eval $( echo "gamescope --mangoapp -w 1920 -h 1200 -W 2880 -H 1800 -f -F fsr -- %command%" | sed -E "s#launcher/dowser#binaries/ck3#g" )
```
