# Install Ubuntu on Dell XPS

@see https://github.com/rcasero/doc/wiki/Ubuntu-linux-on-Dell-XPS-15-(9560)


## Step 1 - Prepare grub to install ubuntu
To even be able to install Ubuntu some boot options must be given before booting into the installer:

Add this after the `---` on the grub boot line 
nouveau.modeset=0 nvme_load=YES

## Step 2 - Set a custom font for grub to make it readable


sudo grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono24.pf2 \
  --size=24 /usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf


Put this in `/etc/default/grub`

```sh
# More readable font on high dpi screen, generated with
# sudo grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono24.pf2 \
#    --size=24 /usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf
GRUB_FONT=/boot/grub/fonts/DejaVuSansMono24.pf2
```

Activate the grub config:
`sudo update-grub`


## Step 3 - Fix the double click trackpad

@see https://medium.com/@pck/ubuntu-18-04-fix-for-right-click-not-working-touchpad-issues-40037ff249e1

Use the gnome-tweak-tool to set the touchpad click behaviour
In the "Keyboard & Mouse" menu Choose the "Area" emulation.


# Power saving
Install TLP for a better laptop oriented power profile.
@see https://linrunner.de/en/tlp/docs/tlp-configuration.html

```sh
sudo apt install tlp
```

To avoid problems with wifi connectivity, i changed these values in the config file: /etc/default/tlp
```ini
WIFI_PWR_ON_AC=off
WIFI_PWR_ON_BAT=off

RESTORE_DEVICE_STATE_ON_STARTUP=1
```
