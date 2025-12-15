# Incident: 2025-12-15 – ARP Table Does Not Show Local IP When Accessing UNC Shared Path

**Customer:** Internal / Client Site
**Reported On:** 2025-12-15

---

## Summary

When attempting to access a shared folder using a UNC path, the client was unable to see the target machine’s IP address in the ARP table (`arp -a`). This caused confusion during network troubleshooting, as the shared folder was intermittently inaccessible.

---

## What Happened

* User attempted to access a shared folder using a UNC path (e.g. `\\PC-NAME\SharedFolder`).
* The connection failed or was inconsistent.
* User ran `arp -a` on the client machine to verify network communication.
* The target PC’s local IP address did **not** appear in the ARP table.
* No firewall error messages were shown.
* Network connection was active, and both machines were on the same LAN.

---

## Fix Applied

1. Verified both client and host PCs were in the **same subnet**.
2. Tested connectivity using:

   * `ping <IP address>`
   * `ping <hostname>`
3. Identified that hostname resolution was failing, so ARP entries were not created.
4. Accessed the shared folder directly using the IP address:

   * `\\192.168.x.x\SharedFolder`
5. Confirmed that the ARP table populated **after** successful IP-based communication.
6. Flushed and refreshed ARP cache:

   * `arp -d *`
   * Re-ran `ping` to regenerate ARP entries
7. Verified File and Printer Sharing was enabled and firewall rules allowed SMB traffic.

---

## Outcome

* Shared folder access was restored using the IP-based UNC path.
* The target machine’s IP address appeared correctly in the ARP table after active communication.
* User understood that ARP entries only appear **after Layer 2 communication occurs**, not simply by opening File Explorer.

---

## Should This Become a KB Article?

**Yes**

---

## Tags

installation, rdp, shared-folder, networking, arp, unc-path

---

If you want, I can:

* Convert this into a **KB version** (more generic, reusable)
* Add **PowerShell / CMD command snippets**
* Standardize this to match **ITIL-style incident logs**
  Just say the word.
