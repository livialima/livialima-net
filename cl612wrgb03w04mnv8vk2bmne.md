## How to turn an old PC into a NAS server

Do you have an old computer laying around your house and want to give it a purpose? Why not use it for storage? This is a tutorial on how to install FreeNAS and share a drive with Windows.

%[https://youtu.be/M7JOb0R84EU]

Step 1 : Check your hardware resources
--------------------------------------

On Windows:

1.  Click the Start button and choose Settings (it's the gear-shaped icon above the power icon).
2.  Click "System."
3.  Click "About."

Step 2 : Find a distro that suits you
-------------------------------------

1.  Go to [DistroWatch](https://distrowatch.com)
2.  Click "Search"
3.  On Distribution category, select "NAS"
4.  On Status, select "Active"
5.  Click "Submit Query"

You will receive a list with the currently active distributions that are focused on NAS, such as FreeNAS, EasyNAS, OpenMediaVault. Take your time to know the hardware requirements and features for each distro, and compare to your old computer resources. The more you have to use, the easier it is to choose.

Step 3 : Create a bootable flash drive
--------------------------------------

Once you have the ISO image downloaded, you need to create a bootable drive to proceed for installation. There are several options in this realm: Rufus, UNetbootin, ImageWriter... the list goes on.

My personal favorite is `dd`, a staple in Linux distros everywhere (`/dev/sdb` being the USB drive):

```
sudo dd if=distro.iso of=/dev/sdb
```

Step 4 : Installation
---------------------

My pick was [FreeNAS](https://www.ixsystems.com/documentation/freenas/11.3-U4/freenas.html) but the installation process is pretty much the same for the other NAS distros.

On installer menu:

1.  Press Enter to select the default option, "Install/Upgrade"
2.  A minimum of 8 GiB of RAM is required and the installer will present a warning message if less than 8 GiB is detected. **However**, for domestic sharing with very low volume of requests, or no RAID, 8GiB is good but not necessary.
3.  Use the arrow keys to highlight the destination SSD, hard drive, USB stick, or virtual disk. If you only have one hard drive, please get at least an USB stick for the system. Drives selected at this stage **cannot be used for data later**. Press the spacebar to select and press Enter.
4.  Set the root password.
5.  Choose UEFI or BIOS booting, depending on how old your computer is. Most UEFI systems can also boot in BIOS mode if CSM (Compatibility Support Module) is enabled in the UEFI setup screens.
6.  Installation complete! Press Enter to return to Installer Menu and press Enter on "Reboot System".

Step 5 : Create a shared volume
-------------------------------

First access the WebGUI by typing the server IP address (provided at the end of installation) on a browser, and login with root.

1.  Go to Storage ➞ Pools and click ADD. Select Create new pool and click CREATE POOL
2.  Enter a name for the pool in the Name field
3.  From the Available Disks section, select disks to add to the pool.
4.  After selecting disks, click the **right arrow** to add them to the Data VDevs section.
5.  Click CREATE. A dialog shows a reminder that all disk contents will be erased. Click Confirm, then CREATE POOL to create the pool.
6.  Click Sharing ➞ Windows (SMB Shares), then ADD.
7.  Select path of the pool created.
8.  Enable Allow Guest Access.
9.  Press SAVE.
10.  When prompted to enable SMB service, click "Enable SMB"

Creating a regular user is a good idea to avoid using root to access the volume remotely.

Step 6 : Access the volume
--------------------------

On Windows:

1.  Open File Explorer.
2.  Select Map network drive.
3.  Select the Drive Letter that you want from the Drive list.
4.  Enter the path to the storage in the Folder field.
```
\\\\nas-server-ip-address
```

6.  Select the Connect using different credentials option.
7.  You can select the Reconnect at logon check box to automatically reconnect to the storage.
8.  Click the Finish to complete the mapping process. When you are prompted for credentials,

*   Enter the NAS user name in the user name field.
*   Enter the NAS password in the password field.
*   Click OK

Done! Enjoy your new NAS. :)