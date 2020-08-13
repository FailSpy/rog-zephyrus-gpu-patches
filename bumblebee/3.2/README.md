# Bumblebee

Building
---
```text
git clone git://github.com/Bumblebee-Project/bumblebee
cd bumblebee
for p in location/to/patches/*.patch; do patch -Np1 -i "$p"; done 

autoreconf -fi

./configure CONF_DRIVER_MODULE_NVIDIA=nvidia \
CONF_LDPATH_NVIDIA=/usr/lib/nvidia:/usr/lib32/nvidia:/usr/lib:/usr/lib32 \
CONF_MODPATH_NVIDIA=/usr/lib/nvidia/xorg/,/usr/lib/xorg/modules \
--prefix=/usr \
--sbindir=/usr/bin \
--with-udev-rules=/usr/lib/udev/rules.d/ \
--sysconfdir=/etc \
--without-pidfile

make
sudo make install

sudo cp scripts/bumblebeed.service /usr/lib/systemd/system/bumblebeed.service
sudo systemctl daemon-reload
```
Please note, the last 2 lines will install a SystemD service 'bumblebeed.service'
Bumblebee includes other init scripts in its repo if you use something else.

You can then enable the service to have it start up each time with: `systemctl enable bumblebeed`

Be sure to blacklist modules as well in one of your /etc/modprobe.d conf files, as bumblebee will load it when it needs them:
```
blacklist nvidia
blacklist nvidia_drm
blacklist nvidia_modeset
blacklist nouveau
```
This line can also be helpful to have it so when bumblebee unloads 'nvidia', it unloads the whole bunch:

`remove nvidia modprobe -r --ignore-remove nvidia_drm nvidia_modeset nvidia`
