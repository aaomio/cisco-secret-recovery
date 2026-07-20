# Cisco Wireless LAN Controller (WLC) Password Recovery

## Overview

Unlike Cisco routers and Catalyst switches, **Cisco Wireless LAN Controllers (AireOS) do not support recovering the existing configuration by bypassing the startup configuration**.

If administrator credentials are lost, the standard recovery method is to **factory reset the controller**, after which it must be reconfigured or restored from a backup.

> **Note:** Always maintain regular configuration backups before performing upgrades or major configuration changes.

---

# Factory Reset

## Step 1 - Connect to the Console

Connect to the WLC using the console port.

Console Settings:

* 9600 Baud
* 8 Data Bits
* No Parity
* 1 Stop Bit
* Flow Control: None

---

## Step 2 - Restart the Controller

### User EXEC (`>`)

Restart the controller.

> (Cisco Controller) > reset system

Confirm when prompted.

---

## Step 3 - Enter the Boot Menu

As the controller begins to reboot, **press `Esc` repeatedly** to interrupt the boot process.

The WLC boot menu will appear.

Select:

> **5 - Clear Configuration**

Confirm the prompt to erase the startup configuration.

The controller will reboot with its factory default configuration.

---

## Step 4 - Perform Initial Setup

After the controller restarts, complete the initial configuration wizard.

Typical settings include:

* System Name
* Management IP Address
* Default Gateway
* VLAN ID
* Country Code
* Administrator Username
* Administrator Password
* NTP Server
* Management Interface

---

## Step 5 - Restore Configuration (Optional)

If a configuration backup exists, restore it after completing the initial setup.

---

# Save Configuration

### User EXEC (`>`)

Save the running configuration.

> (Cisco Controller) > save config

---

# Verification

### User EXEC (`>`)

Verify controller information.

> (Cisco Controller) > show sysinfo
