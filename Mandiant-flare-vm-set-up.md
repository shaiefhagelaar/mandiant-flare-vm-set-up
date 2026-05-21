# Mandiant-flare-vm-set-up

Flare VM for malware

# Installation for Windows 10

Go to this repo and follow the instructions.

https://github.com/mandiant/flare-vm

## Requirements

These requirements are mandetory to run the Flare-VM smoothly. Network will be disabled to reduce the attack surface of any malware that you might download and analyze. Make sure you cover your basics before you attempt working with malicious files. We'll be using a Windows 10 (there's a seperate write up for the Windows 11 installation). We do make a distinction between hardware and software requirements to keep the documentation streamlined.

Use best practices when Reverse Engineering and/or analyzing samples of malware. Using an isolated security framework like Flare-VM doesn't give a 100% guarantee that your host machine is safe whilst virtiualizing the guest OS. There's a chance that the malware stays dormant.   

### Caution

These instruction should suffice. I'll add to the documentation on how to do it (21/05/2026).

    - Disable all networking devices on the guest Windows 10/11 guest OS
    - Disable copy/paste functions
    - Take a snapshot after installing the Windows 10/11 guest OS
    - Take another snapshot after removing the Windows anti-virus
    - Take the last snapshot after Flare-VM is done installing
    - Disable networking in the Flare-VM guest




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

## Workaround for Microsoft Account (20/05/2026)

Make sure you do the installation properly. Download the official Windows 10 iso from the MS website.

Issues whilst booting up the iso might occur. Press a any when it prompt you to do so, if you get an error reboot and retry untill you see the Windows logo. No need to follow the wizard. As soon as you get the wizard set-up loaded follow these instructions:

1. Shift + F10
2. start ms-cxh:localonly​
3. Make a generic account

### Source Bypass MS Account

https://www.hexacorn.com/blog/2022/01/16/ms-cxh-and-ms-cxh-full-handlers/

### Source Disabling Network

If you want to disable the network look here: 

When you have your flare-vm set up open look for the Edit virtual machine settings tab and click on it
 
<img width="2557" height="1363" alt="Disable_Network_Flare_VM_0" src="https://github.com/user-attachments/assets/38910807-c272-4721-948f-563e5bc8db2c" />

A window will open with the title 'Virtual Machine Settings'. You'll see a highlighted square bracket with No.1 make sure you click on it. **Side note(best practices): Hide and/or blur out the path files and other sensitve information if you do share screenshots**.

<img width="1119" height="1072" alt="Disable_Network_Flare_VM_1" src="https://github.com/user-attachments/assets/ad0f72d9-3a4e-492a-b39b-fccc6b227f91" />

Now you'll need to navigate to the Network Adapter tab. Make sure to click on it so we can proceed with disabeling the network connection between the host and guest OS.

<img width="1110" height="1065" alt="Disable_Network_Flare_VM_2" src="https://github.com/user-attachments/assets/42df63fe-5718-42b7-ae09-e44ee8aa47f9" />

We'll disable two functions under Device status (uncheck the checkbox under connect at power on) and Network connection (select the Host-Only: A private network shared with the host).

<img width="1114" height="1056" alt="Disable_Network_Flare_VM_3" src="https://github.com/user-attachments/assets/a987cb33-6758-409b-896c-c65882d90ac5" />

Now you should be set to start reverse engineering safely on a guest os that you created yourself. Good luck and keep in mind to use best practices and document your findings.

### Using Windows 11

Windows 11 is harder than Windows 10 here because of its hardware gate. In VMware Workstation you need to:

Set the VM firmware to UEFI and add a virtual TPM 2.0 device — Windows 11 won't install without TPM 2.0 and Secure Boot. VMware requires the VM to be encrypted (at least the TPM-relevant files) before you can add a vTPM.
Be aware that Windows 11 24H2 in particular has known install friction with FLARE-VM that the 23H2/Windows 10 paths don't hit, so some guides recommend using an older feature update if you run into installer errors.

Microsoft's baseline for the OS itself is a 2-core 64-bit CPU, 4 GB RAM, and 64 GB storage, but those are far below what you'd actually allocate for analysis work.

For more information about installing Windows 11 have a look at the Windows-11-installation.md
