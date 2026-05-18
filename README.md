This works perfectly on my machine, but your milage may vary. The patch is an impermanent bandaid solution. I do not guarantee the script to work for everyone!

# What?
When applied, this patch modifies libinput's `filter-touchpad.c` with customizable touchpad acceleration behaviour, and provides a script that automatically rebuilds libinput with custom values for touchpad acceleration. The configurable values are based on KovaaK's Interaccel (https://github.com/KovaaK/InterAccel) settings.

When built, `libinput.so.10.13.0` is copied into `/usr/lib64/` to replace the old `libinput.so.10.13.0`. Updating `libinput` should revert this patch's changes. On Fedora, you can prevent `libinput` from updating with `echo "excludepkgs=libinput*" | sudo tee -a /etc/dnf/dnf.conf`.

# Prerequisites
Your distribution must be using `/usr/lib64/libinput.so.10.13.0`, as this patch is designed to replace it. The version of libinput this patch is designed for might be outdated by the time you apply it. The `build.sh` script that applies the patch requires Fedora on GNOME, but in principle can be edited to apply to other distributions. `build.sh` should automatically download prerequisite packages when run for the first time. The installed dependencies are `meson ninja-build cmake gcc gcc-c++ libudev-devel libevdev-devel libwacom-devel glib2-devel mtdev-devel`.

# Usage

After patching, configurable acceleration values can be adjusted directly in `libinput/src/filter-touchpad.c` starting at line 117, or interactively through `build.sh` on Fedora.

## On Fedora Workstation 44 

`build.sh` is a helper script that automates the editing, building, and deployment of the replacement libinput. It will install libinput's dependencies with `dnf install`. 

```bash
git clone https://gitlab.freedesktop.org/libinput/libinput/
git clone https://github.com/m1ksu/fedora-libinput-custom-touchpad-acceleration
cd libinput
git apply ../fedora-libinput-custom-touchpad-acceleration/custom_touchpad_acceleration.patch
./build.sh
```

In GNOME, replacing `/usr/lib64/libinput.so.10.13.0` should result in instant log-out as gdm crashes. You can choose to not immediately replace the file when running `build.sh`, but you will have to manually replace `/usr/lib64/libinput.so.10.13.0` with `libinput/builddir/libinput.so.10.13.0` to apply the changes. In any case, the changes will not apply until you have logged out.

## On other distributions or desktop environments

To automatically download libinput and this repository, and apply the patch to `src/filter-touchpad.c`:
```bash
git clone https://gitlab.freedesktop.org/libinput/libinput/
git clone https://github.com/m1ksu/fedora-libinput-custom-touchpad-acceleration
cd libinput
git apply ../fedora-libinput-custom-touchpad-acceleration/custom_touchpad_acceleration.patch
```
You will have to build libinput and replace `/usr/lib64/libinput.so.10.13.0` with `libinput/builddir/libinput.so.10.13.0` yourself. 
https://wayland.freedesktop.org/libinput/doc/latest/building.html
