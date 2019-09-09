# raspberry-pi

## Tools
### Hardware
- Raspberry Pi 3 Model B+
- 2.5A Power Supply
- Protective Case
- MicroSD Card (32GB)

### Software
- [Raspbian Buster with desktop and recommended software](https://www.raspberrypi.org/downloads/raspbian/) 

## Setup
1. Plug SD card into laptop
2. Check SD card for contents
  ```
  $ diskutil list
  ...
  /dev/disk3 (external, physical):
     #:                       TYPE NAME                    SIZE       IDENTIFIER
     0:     FDisk_partition_scheme                        *31.9 GB    disk3
     1:             Windows_FAT_32 NO NAME                 31.9 GB    disk3s1
     
  $ SD_DISK_NUM=3 # because the disk number shown above is 3
  ```
  **Note** SD card may already have contents :. to wipe: `sudo diskutil eraseDisk FAT32 MYSD MBRFormat /dev/disk3`

3. Download disk image [Raspbian Buster with desktop and recommended software](https://www.raspberrypi.org/downloads/raspbian/) (This step takes a while due to image size)

4. Unarchive the Raspbian image and set the location
   `RASPBIAN_IMG=~/Downloads/2018-11-13-raspbian-stretch.img`

5. Run
  ```
  $ diskutil unmountDisk /dev/disk$SD_DISK_NUM
  $ sudo dd bs=1m if=$RASPBIAN_IMG of=/dev/rdisk$SD_DISK_NUM
  ```

6. Enable SSH
   ```
   $ df # Find where SD card filesystem is located
   Filesystem           ...             Mounted on

   ...

   /dev/disk3s1                         /Volumes/boot
   
   $ SD_FILES=/Volumes/boot # Location of SD files as defined above
   $ touch $SD_FILES/ssh # enables ssh
   ```
7. Eject the disk `sudo diskutil eject /dev/disk$SD_DISK_NUM`

## Accessing Pi without internet


