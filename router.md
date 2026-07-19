# Cisco Router Password Recovery (Cisco 1841)

## Step 1 - Enter ROMMON

Power cycle the router and send a **Break** signal during boot.

### ROMMON

> rommon 1 > confreg 0x2142

> rommon 2 > reset

---

## Step 2 - User EXEC Mode

After the router boots, it ignores the startup configuration and enters **User EXEC Mode**.

### User EXEC (`>`)

> Router> enable

---

## Step 3 - Privileged EXEC Mode

Restore the saved startup configuration.

### Privileged EXEC (`#`)

> Router# copy startup-config running-config

The router loads the saved configuration into RAM while in Privileged EXEC mode.

---

## Step 4 - Global Configuration Mode

Enter Global Configuration mode and update the password.

### Global Configuration (`(config)#`)

> Router# configure terminal

> Router(config)# enable secret NewPassword

Restore the configuration register.

> Router(config)# config-register 0x2102

Exit configuration mode.

> Router(config)# end

---

## Step 5 - Save the Configuration

### Privileged EXEC (`#`)

> Router# write memory

or

> Router# copy running-config startup-config

---

## Step 6 - Reload

### Privileged EXEC (`#`)

> Router# reload

The router now boots normally using the recovered configuration.

---

# Verification

### Privileged EXEC (`#`)

Verify the configuration register.

> Router# show version | include register

Expected output:

> Configuration register is 0x2102

Verify access using the new password and confirm the original configuration has been preserved.
