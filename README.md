# What?
When applied, this patch modified libinput's `filter-touchpad.c` with a custom touchpad acceleration behaviour, and provides a script that automatically rebuilds libinput with custom values for touchpad acceleration. The configurable values are based on KovaaK's Interaccel (https://github.com/KovaaK/InterAccel) settings.

When built, `libinput.so.13.10.0` is copied into `/usr/lib64/` to replace the old `libinput.so.13.10.0`. Updating `libinput` will revert this patch's changes. On Fedora, you can prevent `libinput` from updating with `echo "excludepkgs=libinput*" | sudo tee -a /etc/dnf/dnf.conf`.

# Prerequisites
Your distribution must be using `/usr/lib64/libinput.so.13.10.0`, as this patch is designed to replace it. The version of libinput this patch is designed for might be outdated by the time you apply it. The `build.sh` script that applies the patch requires Fedora on GNOME, but in principle can be edited to apply to other distributions. `build.sh` should automatically download prerequisite packages when run for the first time.

# Usage

The configurable acceleration values can be adjusted directly in `libinput/src/filter-touchpad.c`. They 
To download and use this patch, run this:

## On Fedora Workstation 44 

```bash
git clone https://gitlab.freedesktop.org/libinput/libinput/
git clone https://github.com/m1ksu/fedora-libinput-custom-touchpad-acceleration
cd libinput
git apply ../fedora-libinput-custom-touchpad-acceleration/custom_touchpad_acceleration.patch
./build.sh
```

In GNOME, replacing `/usr/lib64/libinput.so.13.10.0` should result in instant log-out as gdm crashes. You can choose to not immediately replace the file when running `build.sh`, but you will have to manually replace `/usr/lib64/libinput.so.13.10.0` with `libinput/builddir/libinput.so.13.10.0` to apply the changes.

## On other distributions or desktop environments

To automatically download libinput and this repository, and apply the patch:
```bash
git clone https://gitlab.freedesktop.org/libinput/libinput/
git clone https://github.com/m1ksu/fedora-libinput-custom-touchpad-acceleration
cd libinput
git apply ../fedora-libinput-custom-touchpad-acceleration/custom_touchpad_acceleration.patch
```
You will have to build libinput and replace `/usr/lib64/libinput.so.13.10.0` with `libinput/builddir/libinput.so.13.10.0` yourself. 
https://wayland.freedesktop.org/libinput/doc/latest/building.html
