# Cisco Catalyst Switch Password Recovery

## Overview

Cisco Catalyst switches support password recovery **without erasing the existing configuration**. Unlike routers, Catalyst switches do **not** use a configuration register (`confreg 0x2142`). Instead, the startup configuration is temporarily renamed so the switch boots without loading it.

> **Note:** The VLAN database (`vlan.dat`) is stored separately from the startup configuration and is **not** affected by password recovery.

---

# Step 1 - Enter the Boot Loader

Power cycle the switch.

Hold the **MODE** button while powering on the switch.

Release the MODE button when the boot loader (`switch:`) prompt appears.

---

# Step 2 - Initialize Flash

### Boot Loader (`switch:`)

Initialize the flash file system.

> switch: flash_init

Verify the flash contents.

> switch: dir flash:

---

# Step 3 - Rename the Startup Configuration

Rename the startup configuration so the switch ignores it during boot.

### Boot Loader (`switch:`)

> switch: rename flash:config.text flash:/config.old

Boot the switch.

> switch: boot

---

# Step 4 - Enter Privileged EXEC Mode

After the switch has booted:

### User EXEC (`>`)

> Switch> enable

No password should be required because the startup configuration was ignored.

---

# Step 5 - Restore the Existing Configuration

Restore the saved configuration into RAM.

### Privileged EXEC (`#`)

> Switch# copy flash:config.old running-config

The original configuration is now restored while in Privileged EXEC mode.

---

# Step 6 - Change Passwords

> Switch(config)# enable secret NewPassword

If required, update console and VTY passwords.

Exit configuration mode.

> Switch(config)# end

---

# Step 7 - Restore the Startup Configuration

Rename the configuration file back to its original name.

### Privileged EXEC (`#`)

> Switch# rename flash:config.old flash:config.text

---

# Step 8 - Save the Configuration

### Privileged EXEC (`#`)

> Switch# write memory

or

> Switch# copy running-config startup-config

---

# Step 9 - Reload

### Privileged EXEC (`#`)

> Switch# reload

The switch will now boot normally using the recovered configuration.

---

# Factory Reset

To completely erase the switch configuration:

### Privileged EXEC (`#`)

> Switch# erase startup-config

Delete the VLAN database.

> Switch# delete flash:vlan.dat

Reload the switch.

> Switch# reload

