# mandiant-flare-vm-set-up
Flare VM for malware


## Requirements

These requirements are mandetory to run the Flare-VM smoothly. Network will be disabled to reduce the attack surface of any malware that you might download and analyze. Make sure you cover your basics before you attempt working with malicious files. We'll be using a Windows 11 iso

### Hardware

This runs VMware Workstation plus everything else, so it needs headroom well beyond the guest:

- CPU: 64-bit with hardware virtualization (Intel VT-x / AMD-V) enabled in BIOS/UEFI. 4+ cores recommended so you can give the VM 2 without starving the host.
- RAM: 16 GB minimum in practice. You'll allocate 8 GB to the guest, and you want room left over for the host and possibly a second VM (e.g. REMnux/INetSim for network simulation).
- Disk: 100+ GB free. The VM itself needs ~80–100 GB, and snapshots grow that significantly — each snapshot can add tens of GB.
- Virtualization platform: VMware Workstation (Pro is now free for personal use under Broadcom). Workstation gives you better snapshot handling and performance than VirtualBox.

### Software

- A clean Windows 11 install from the official Microsoft ISO — no other software, fresh state.
- PowerShell 5+ (ships with Windows 11) and .NET 4.5+.
- An internet connection, with Tamper Protection and any anti-malware (Windows Defender) disabled — preferably via Group Policy — and Windows Updates disabled. The installer checks for these but it's smoother to disable them first. GitHub
- Username with no spaces or special characters (the installer fails otherwise).
- Take a clean snapshot after Windows is configured but before running the FLARE-VM installer, so you can roll back if it breaks.

### Using Windows 11

Windows 11 is harder than Windows 10 here because of its hardware gate. In VMware Workstation you need to:

Set the VM firmware to UEFI and add a virtual TPM 2.0 device — Windows 11 won't install without TPM 2.0 and Secure Boot. VMware requires the VM to be encrypted (at least the TPM-relevant files) before you can add a vTPM.
Be aware that Windows 11 24H2 in particular has known install friction with FLARE-VM that the 23H2/Windows 10 paths don't hit, so some guides recommend using an older feature update if you run into installer errors.

Microsoft's baseline for the OS itself is a 2-core 64-bit CPU, 4 GB RAM, and 64 GB storage, but those are far below what you'd actually allocate for analysis work.

### Bypassing Microsoft Account

As soon as you get the Microsoft Account requirement during the installation process follow these instructions:

1. Shift + F10
2. start ms-cxh:localonly​
3. Make a generic account 
