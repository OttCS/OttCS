# Upgrading to Nobara 40
**The ISO is taking a bit**

*Credit to LionHeartP in the Nobara/ProtonGE Discord*

Nobara 40 is currently ready to be upgraded to from 39. No new ISOs have been made yet, but all packages are updated and finalized. To upgrade, nothing special is required this time around.

Run the Update System app (or `nobara-sync` in a terminal) to update your 39 installation and bring it in line with some packaging differences (wine-staging) that exist in 40

```
sudo dnf install dnf-plugin-system-upgrade -y
```

This plugin may already be installed, especially if you have previously upgraded from an older Nobara version. (eg. 38 > 39)

```
sudo dnf system-upgrade download --releasever=40 -y
```

At this point, `dnf` will download the appropriate packages from 40 and will check against them for any dependency errors. You must resolve all errors before proceeding. If you're unsure on how to proceed, ask here and for the love of God **never do --allowerasing**

```
sudo dnf system-upgrade reboot
```

This final step will reboot your system and upgrade everything to Nobara 40. Be aware that it may take a while and appear stuck at various points. Don't interrupt, don't be impatient.