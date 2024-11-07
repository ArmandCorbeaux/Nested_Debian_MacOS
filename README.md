# Nested Debian MacOS

*This is just a repository to store all the manual manupulations that I need to perform currently*
*For others adjustments, I take elements from my "better_bookworm" repository*

**Subject :**
- Collection of manual adjustments to have a fully running Debian VM through my in-development app

**Requirements :**
- MacOS 15+
- M3+ CPU

Nested Virtualization is enable through Apple Virtualization framework

## Installation of Debian
Assisted Partition Manager doesn't run well as there's 2 partitions through Apple Virtualization.

My way is to create :
- a 1st partition of 256MB with EFI label
- a 2nd one as EXT4 with the rest of the empty space, with "discard" and "noatime"
- to have a light VM, install only "ususla utilities"

## Add Cut and Paste function :
```bash
sudo apt update
sudo apt install spice-vdagent
```

## Configure keyboard
```bash
sudo dpkg-reconfigure keyboard-configuration
```
*for the - you have to found the US ANSI layout in a first time*

later tips to come to adjust keyboard settings
*And I hope to find a way to fix ANSI /ISO keyboard conversion*
*Apple Framework considers keyboard only in ANSI configuration*
*but I believe what a swap-key tips could make the job*

## Configure console fonts size
```bash
sudo dpkg-reconfigure console-setup
```
*My choice is "Terminus Font", "16x32" size*
*At this size, the font size is coherent with the Retina resolution of the screen*
*There's a 2x factor*

## Minimal Desktop
```bash
sudo apt install gnome-shell gnome-console nautilus plymouth-themes -y && sudo reboot
```
*Sometimes, VM handles when installing desktop environment*
*The "reboot" command permits to not shutdown unproperly the VM system.*
 

## Adjust boot
*Because we are in a VM, there's no need to wait for Grub boot time."
```bash
sudo plymouth-set-default-theme -R bgrt
```

## Adjust desktop scale
*To match the size of MacOS interface*

```bash
sudo nano /usr/share/glib-2.0/schemas/90_hidpi.gschema.override
```
Add in the empty file:
```bash
[org.gnome.desktop.interface]
scaling-factor=2
```
ctrl+x to save

then :
```bash
sudo glib-compile-schemas /usr/share/glib-2.0/schemas
```

