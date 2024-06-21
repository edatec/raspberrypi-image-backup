# raspberrypi-image-backup

This is a script for backing up Raspberry Pi operating system, written by leomichalski, the repository link is https://github.com/leomichalski/drone-delivery/tree/0bf5d975d7672ac6221276f42e54ecfa2ecad3b8.

## How to use this script

It need a SD card or a storage device

In the OS with desktop, device maybe auto mount to **/media/**
```sh
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    1 29.1G  0 disk
└─sda1        8:1    1 29.1G  0 part /media/pi/59EB-E8DO
mtdblock0    31:0    0    4M  0 disk
mmcblk0     179:0    0 29.1G  0 disk
├─mmcblk0p1 179:1    0  256M  0 part /boot
└─mmcblk0p2 179:2    0 28.9G  0 part /
```

Now please umount the sda1 from /media/pi/59EB-E8DO
```sh
sudo umount /media
```

**Note: Format storage device is not necessary, the max file size of ext4 is 16 TB, and the max file size of vfat is 4 GB**
**Note: I don't recommend using vfat, becasue the size of OS with desktop maybe over 4GB**
```sh
lsblk

NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    1 29.1G  0 disk
└─sda1        8:1    1 29.1G  0 part
mtdblock0    31:0    0    4M  0 disk
mmcblk0     179:0    0 29.1G  0 disk
├─mmcblk0p1 179:1    0  256M  0 part /boot
└─mmcblk0p2 179:2    0 28.9G  0 part /

# My storage device is sda1

sudo mkfs.ext4 /dev/sda1
```

Then mount sda1 to /mnt or /media directory.

```sh
sudo mount /dev/sda1 /mnt
```

Clone the repository

```sh
git clone https://github.com/edatec/raspberrypi-image-backup
```

Copy image-backup script to the directory where the storage device is mounted

```sh
sudo cp raspberrypi-image-backup/image-backup /mnt
```

Add execute permission to image-backup

```sh
sudo chmod +x /mnt/image-backup
```

## backup

Start backup of Raspberry Pi OS

```sh
sudo /mnt/image-backup
```

First question is 'Image file to create?' 
Input where you want to save the img file, and set the name of the img file

```sh
Image file to create?/mnt/backup.img
```

Second question is 'Initial image file ROOT filesystem size (MB) [1784]?'
Enter to continue

```sh
Initial image file ROOT filesystem size (MB) [1784]?

```

Third question is 'Added space for incremental updates after shrinking (MB) [0]?'
Enter to contine

```sh
Added space for incremental updates after shrinking (MB) [0]?

```

Fourth question is 'Create /mnt/backup.img (y/n)?'
Input 'y'

```sh
Create /mnt/backup.img (y/n)? y
```

Wait for the command to end, and then you will find the img file in /mnt
```sh
ls /mnt/backup.img
```
