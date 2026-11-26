# Toucpad Not Working
Possible reason, still in suspend mode. When you sleep your laptop some parts goes in suspend mode, when you turn it on a selection of them comes back on, the rest stuck there
## Solution
Fix in kernel in the grub
Go to this file
    sudo nano /etc/default/grub
find this line
    GRUB_CMDLINE_LINUX_DEFAULT=...
add this at the end of the string inside before the last '.
    i8042.nomux=1 i8042.reset i8042.notimeout
restart the mod
    sudo modprobe -r psmouse
    sudo modprobe psmouse
