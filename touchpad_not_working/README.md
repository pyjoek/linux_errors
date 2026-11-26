# Touchpad Not Working After Suspend

## Possible Cause

Your touchpad may stop working after waking your laptop from suspend or sleep mode.

When your laptop goes to sleep, some hardware components enter a suspended state. When you turn it back on, not all components may resume properly. As a result, the touchpad can remain unresponsive.

## Solution

One possible fix is to adjust the kernel parameters through GRUB.

### 1. Open the GRUB configuration file

```bash
sudo nano /etc/default/grub
```

### 2. Update the kernel parameters

Find the following line:

```bash
GRUB_CMDLINE_LINUX_DEFAULT="..."
```

Add these parameters at the end of the existing string, before the closing quotation mark:

```bash
i8042.nomux=1 i8042.reset i8042.notimeout
```

For example:

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash i8042.nomux=1 i8042.reset i8042.notimeout"
```

Save the file and exit.

### 3. Reload the touchpad module

Run the following commands:

```bash
sudo modprobe -r psmouse
sudo modprobe psmouse
```

### 4. Update GRUB

Apply the configuration changes:

```bash
sudo update-grub
```

### 5. Restart your laptop

```bash
sudo reboot
```

After restarting, test your touchpad and check whether it continues working after suspend and resume.

---

**Note:** This workaround is intended for Linux systems using GRUB and the `psmouse` driver. The `i8042` parameters may not apply to every touchpad or laptop model.
