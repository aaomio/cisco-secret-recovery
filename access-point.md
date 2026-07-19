# Cisco Access Point Password Recovery

## Overview

Unlike Cisco routers and Catalyst switches, **Cisco Access Points do not support configuration recovery by temporarily ignoring the startup configuration** (such as `confreg 0x2142` or renaming `config.text`).

If administrative access is lost, the standard recovery procedure is to **factory reset the Access Point** using the **MODE** button during boot.

> **Note:** Existing configuration cannot normally be recovered from an autonomous Access Point. Ensure configuration backups are taken regularly.

---

# Autonomous Access Point

## Factory Reset

### Step 1 - Power Off

Disconnect power from the Access Point.

---

### Step 2 - Hold the MODE Button

Press and hold the **MODE** button.

Reconnect power while continuing to hold the button.

Continue holding the button until the Status LED changes (approximately 20–30 seconds).

Release the MODE button.

The Access Point will boot with the factory default configuration.

---

### Step 3 - Reconfigure the Access Point

### User EXEC (`>`)

> AP> enable

Configure the Access Point as required.

---

### Privileged EXEC (`#`)

Save the new configuration.

> AP# write memory

or

> AP# copy running-config startup-config

