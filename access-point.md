# Cisco Access Point Password Recovery

## Overview

Unlike Cisco routers and Catalyst switches, **Cisco Access Points do not support configuration recovery by temporarily ignoring the startup configuration** (such as `confreg 0x2142` or renaming `config.text`).

If administrative access is lost, the standard recovery procedure is to **factory reset the Access Point** using the **MODE** button during boot.

> **Note:** Existing configuration cannot normally be recovered from an Access Point. Ensure configuration backups are taken regularly.

---

# Factory Reset

## Step 1 - Power Off

Disconnect power from the Access Point.

---

## Step 2 - Hold the MODE Button

Press and hold the **MODE** button.

Reconnect power while continuing to hold the MODE button.

Continue holding the button until the Status LED changes (typically **20–30 seconds**, depending on the model).

Release the MODE button.

> **Important:** Do **not** continue holding the MODE button for too long (approximately 50 seconds or more on many models), as this enters **Image Recovery Mode**, where the AP attempts to download a recovery image via TFTP.

---

## Step 3 - If the AP Stops at the Boot Loader

If the AP enters the boot loader (`ap:`), restart it.

### Boot Loader (`ap:`)

> ap: reset

Confirm the prompt.

> Are you sure you want to reset the system (y/n)? y

The Access Point will reboot using the existing IOS image.

---

## Step 4 - Reconfigure the Access Point

After the factory reset completes, configure the Access Point as required.

### User EXEC (`>`)

> AP> enable

---

### Privileged EXEC (`#`)

Save the new configuration.

> AP# write memory

or

> AP# copy running-config startup-config

