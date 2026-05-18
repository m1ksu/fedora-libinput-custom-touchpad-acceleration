# What?
When applied, this patch provides a script that rebuilds libinput with custom values for touchpad acceleration. The configurable values are based on KovaaK's Interaccel (https://github.com/KovaaK/InterAccel) settings.

When built, `libinput.so.13.10.0` is copied into `/usr/lib64/` to replace the old `libinput.so.13.10.0`. Updating `libinput` will revert this patch's changes. On Fedora, you can prevent `libinput` from updating with `echo "excludepkgs=libinput*" | sudo tee -a /etc/dnf/dnf.conf`.

# Prerequisites
This patch is made for Fedora 44 running GNOME 50. The `build.sh` script that applies the patch requires Fedora, but can be edited to apply to other distributions. `build.sh` should automatically download prerequisite packages.

# Usage

To download and use this patch, run this:

```bash
git clone https://github.com/wayland-tablet/libinput
git clone https://github.com/m1ksu/fedora-libinput-custom-touchpad-acceleration
cd libinput
git apply ../fedora-libinput-custom-touchpad-acceleration/custom_touchpad_acceleration.patch
./build.sh
```
