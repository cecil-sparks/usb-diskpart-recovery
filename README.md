# Troubleshooting & Restoring a Corrupted USB Flash Drive via Windows DiskPart

## Problem Statement
A USB flash drive malfunctioned and mounted in Windows as multiple fragmented partitions, making it unusable for standard file transfers or bootable media creation. Standard GUI formatting tools were unable to merge the partitions and restore the drive's full native capacity.

## Objective
Use the Windows command-line disk partitioning utility (`diskpart`) with elevated privileges to wipe the partition table, rebuild a single primary partition, format the volume to exFAT, and restore full storage accessibility.

## Tools & Environment
* **OS:** Windows 10 / Windows 11
* **Utility:** Command Prompt (Administrator) & `diskpart.exe`
* **File System:** exFAT (chosen for cross-platform compatibility and support for files larger than 4 GB)

## Step-by-Step Resolution

### 1. Launch Elevated Command Prompt & DiskPart
Opened Command Prompt as Administrator and initialized the disk management utility:
```cmd
diskpart
```

### 2. Identify and Select Target Disk
Enumerated all connected physical drives (`list disk`) and verified the target USB drive by storage capacity to prevent accidental data loss on the primary OS drive. Selected the target flash drive (`Disk 1`):
```cmd
select disk 1
```

### 3. Wipe Partition Table & Existing Volumes
Removed all existing partition and volume formatting from the drive:
```cmd
clean
```

### 4. Create Primary Partition & Format Volume
Allocated the full unallocated space into a single primary partition and performed a quick format using the exFAT file system:
```cmd
create partition primary
format fs=exfat quick
```

### 5. Assign Drive Letter & Exit
Mounted the newly formatted volume to Windows File Explorer by assigning an available drive letter, then exited the utility:
```cmd
assign
exit
```

## Outcome & Verification
* Confirmed in Windows File Explorer under **This PC** that the flash drive mounted cleanly as a single healthy volume with its full native storage capacity restored.

## Skills Demonstrated
* Windows Command-Line Interface (CLI) Administration
* Storage & Partition Management (`diskpart`)
* File System Configuration (exFAT)
* Hardware & Removable Media Troubleshooting
