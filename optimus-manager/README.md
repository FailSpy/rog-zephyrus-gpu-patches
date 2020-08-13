## Optimus Manager

For using Optimus Manager on the Zephyrus, you will need to use a patched version that supports recognizing the iGPU, as the current one only recognizes Intel.

Here, you can find the link for Optimus Manager with support for AMD, made by Kr1ss:
https://github.com/Kr1ss-XD/optimus-manager#branch=amdigpu-compat

If you're on Arch/Manjaro, you can find an AUR package here:
[optimus-manager-amd-git](https://aur.archlinux.org/packages/optimus-manager-amd-git/)

Once set up, just add this to your `/etc/optimus-manager/optimus-manager.conf`:
```
[optimus]
switching=bbswitch
pci_power_control=no
pci_remove=no
pci_reset=no
```
This will have optimus-manager use bbswitch between the different modes. 'amd' mode will turn the dGPU completely off, hybrid/nvidia mode will leave it on and let NVIDIA handle power management (refer to [here](https://asus-linux.org/wiki/rog-zephyrus/g14-and-g15/hardware/graphics/#power-management))
