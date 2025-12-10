# KB-1002: shared-folder-0x80007005 error

Author:  Yean1277
Created:  10 Dec 2025
Last Updated:  10 Dec 2025
Version: 12.101.242

---

## Summary
Client PC cannot access the host PC’s shared folder. When connecting via \\hostname\sharename, the system shows “Network path not found”, sometimes accompanied by error 0x80070005 / 0x80004005.

## Symptoms
- Client reports they cannot open shared folder from File Explorer.
- Accessing \\<PC-NAME> or \\<HOST-IP> returns an error.
- Sometimes the hostname cannot be resolved, but direct IP might work.
- Common error messages:
  - “Network path not found.”
  - “Windows cannot access \hostname.”
  - Error code: 0x80070005 or 0x80004005
  - Ping works, but shared folder still cannot open.

## Root Cause
- SMB protocol disabled on Windows (common after updates).
- Host PC firewall blocking File and Printer Sharing (SMB-In).
- Network profile set to Public, causing sharing to be restricted.
- Incorrect hostname resolution (NetBIOS not resolving properly).
- Sharing/NTFS permissions not granted to Everyone or the target user.
- Host PC is asleep, hibernated, or network adapter in power saving mode.

## Resolution (Steps)
1. Click the Windows Key and Search “PowerShell” > Run as Administrator
   - Enter the following command and press enter
<code>
Set-SmbClientConfiguration -EnableInsecureGuestLogons $true -Force 
Set-SmbClientConfiguration -RequireSecuritySignature $false -Force 
Set-SmbServerConfiguration -RequireSecuritySignature $false -Force 
</code>

## Extra Notes
- Tips
- Warnings
- Best practices

## Tags
sql, network, windows, shared-folder, smb, 0x80070005, 0x80004005
