# rog-zephyrus-gpu-patches
A group of patches to help with GPU power management on the Zephyrus lineup

How to use
---
Install bbswitch and your choice of a GPU switching assister -- Optimus Manager or Bumblebee

Inside each folder for each package is an install guide on how to build and install them.

Optimus Manager is currently recommended, as it's more up to date. It's compatible with PRIME, and you can use bbswitch with it
to allow the GPU to turn off when you switch into pure 'amd' mode.

Bumblebee is more experimental. It allows the GPU to be turned on and off as you open and close applications that want the GPU.
However, Vulkan is not currently working with it.

I think it could eventually work with some fiddling with this: [primus\_vk](https://github.com/felixdoerre/primus_vk), but as of right now, not possible.

If you wish to turn on/off the GPU manually with bbswitch setup, you can do 

ON:  `sudo tee /proc/acpi/bbswitch<<<ON` 
OFF: `sudo tee /proc/acpi/bbswitch<<<OFF`

Note, you might have to unload nvidia drivers before doing so, as bbswitch will intentionally not do anything if the GPU appears to be in use.
```
modprobe -r nvidia_drm nvidia_modeset nvidia
```
This is where Optimus Manager and Bumblebee come to shine, as they'll automatically unload the drivers before calling to bbswitch.

It's recommended you blacklist these drivers regardless of your solution(/etc/modprobe.d/(whateveryoulike).conf):
```
blacklist nouveau
blacklist nvidiafb
blacklist rivafb
blacklist i2c_nvidia_gpu
```

Optional modprobe.d addition:
```
remove nvidia modprobe -r --ignore-remove nvidia_drm nvidia_modeset nvidia
```
This will make it so when you run just `modprobe -r nvidia` it will automatically remove other dependent modules at the same time.

Active Power Management
---
When using any of the available options, I also recommend setting up some power management options for when the GPU is on, like described [here](https://asus-linux.org/wiki/rog-zephyrus/g14-and-g15/hardware/graphics/#power-management)
(Thanks to ZappeL for these)
