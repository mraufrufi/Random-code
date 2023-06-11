##Let's find out about our hard disks:

```fdisk -l```

The output looks like this:
```
server1:~# fdisk -l
 
 Disk /dev/sda: 21.4 GB, 21474836480 bytes
 255 heads, 63 sectors/track, 2610 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
    Device Boot      Start         End      Blocks   Id  System
 /dev/sda1   *           1          18      144553+  83  Linux
 /dev/sda2              19        2450    19535040   83  Linux
 /dev/sda4            2451        2610     1285200   82  Linux swap / Solaris
 
 Disk /dev/sdb: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Disk /dev/sdb doesn't contain a valid partition table
 
 Disk /dev/sdc: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Disk /dev/sdc doesn't contain a valid partition table
 
 Disk /dev/sdd: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Disk /dev/sdd doesn't contain a valid partition table
 
 Disk /dev/sde: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Disk /dev/sde doesn't contain a valid partition table
 
 Disk /dev/sdf: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Disk /dev/sdf doesn't contain a valid partition table
 ```
There are no partitions yet on /dev/sdb - /dev/sdf. We will create the partitions /dev/sdb1, /dev/sdc1, /dev/sdd1

```


server1:~# fdisk /dev/sdb

The number of cylinders for this disk is set to 10443.
There is nothing wrong with that, but this is larger than 1024,
and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
   (e.g., DOS FDISK, OS/2 FDISK)

Command (m for help): <-- m
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)

Command (m for help): <-- n
Command action
   e   extended
   p   primary partition (1-4)
<-- p
Partition number (1-4): <-- 1
First cylinder (1-10443, default 1): <-- <ENTER>
Using default value 1
Last cylinder or +size or +sizeM or +sizeK (1-10443, default 10443): <-- +25000M

Command (m for help): <-- t
Selected partition 1
Hex code (type L to list codes): <-- L

 0  Empty           1e  Hidden W95 FAT1 80  Old Minix       be  Solaris boot
 1  FAT12           24  NEC DOS         81  Minix / old Lin bf  Solaris
 2  XENIX root      39  Plan 9          82  Linux swap / So c1  DRDOS/sec (FAT-
 3  XENIX usr       3c  PartitionMagic  83  Linux           c4  DRDOS/sec (FAT-
 4  FAT16 <32M      40  Venix 80286     84  OS/2 hidden C:  c6  DRDOS/sec (FAT-
 5  Extended        41  PPC PReP Boot   85  Linux extended  c7  Syrinx
 6  FAT16           42  SFS             86  NTFS volume set da  Non-FS data
 7  HPFS/NTFS       4d  QNX4.x          87  NTFS volume set db  CP/M / CTOS / .
 8  AIX             4e  QNX4.x 2nd part 88  Linux plaintext de  Dell Utility
 9  AIX bootable    4f  QNX4.x 3rd part 8e  Linux LVM       df  BootIt
 a  OS/2 Boot Manag 50  OnTrack DM      93  Amoeba          e1  DOS access
 b  W95 FAT32       51  OnTrack DM6 Aux 94  Amoeba BBT      e3  DOS R/O
 c  W95 FAT32 (LBA) 52  CP/M            9f  BSD/OS          e4  SpeedStor
 e  W95 FAT16 (LBA) 53  OnTrack DM6 Aux a0  IBM Thinkpad hi eb  BeOS fs
 f  W95 Ext'd (LBA) 54  OnTrackDM6      a5  FreeBSD         ee  EFI GPT
10  OPUS            55  EZ-Drive        a6  OpenBSD         ef  EFI (FAT-12/16/
11  Hidden FAT12    56  Golden Bow      a7  NeXTSTEP        f0  Linux/PA-RISC b
12  Compaq diagnost 5c  Priam Edisk     a8  Darwin UFS      f1  SpeedStor
14  Hidden FAT16 <3 61  SpeedStor       a9  NetBSD          f4  SpeedStor
16  Hidden FAT16    63  GNU HURD or Sys ab  Darwin boot     f2  DOS secondary
17  Hidden HPFS/NTF 64  Novell Netware  b7  BSDI fs         fd  Linux raid auto
18  AST SmartSleep  65  Novell Netware  b8  BSDI swap       fe  LANstep
1b  Hidden W95 FAT3 70  DiskSecure Mult bb  Boot Wizard hid ff  BBT
1c  Hidden W95 FAT3 75  PC/IX
Hex code (type L to list codes): <-- 8e
Changed system type of partition 1 to 8e (Linux LVM)

Command (m for help): <-- w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

Now we do the same for the hard disks /dev/sdc - /dev/sde:

```
fdisk /dev/sdc
 fdisk /dev/sdd
 fdisk /dev/sde
 ```
 Then run
 
 ```
 fdisk -l
 ```
 
 again. The output should look like this: Partations are created
 
 
 ```
 server1:~# fdisk -l
 
 Disk /dev/sda: 21.4 GB, 21474836480 bytes
 255 heads, 63 sectors/track, 2610 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Device Boot      Start         End      Blocks   Id  System
 /dev/sda1   *           1          18      144553+  83  Linux
 /dev/sda2              19        2450    19535040   83  Linux
 /dev/sda4            2451        2610     1285200   82  Linux swap / Solaris
 
 Disk /dev/sdb: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes

  Device Boot      Start         End      Blocks   Id  System
  /dev/sdb1               1        3040    24418768+  8e  Linux LVM
 
 Disk /dev/sdc: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Device Boot      Start         End      Blocks   Id  System
 /dev/sdc1               1        3040    24418768+  8e  Linux LVM
 
 Disk /dev/sdd: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
  Device Boot      Start         End      Blocks   Id  System
 /dev/sdd1               1        3040    24418768+  8e  Linux LVM
 
 Disk /dev/sde: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 Device Boot      Start         End      Blocks   Id  System
 /dev/sde1               1        3040    24418768+  8e  Linux LVM
 
 Disk /dev/sdf: 85.8 GB, 85899345920 bytes
 255 heads, 63 sectors/track, 10443 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 
 Disk /dev/sdf doesn't contain a valid partition table
 ```
 Now we prepare our new partitions for LVM:
 
 ```
 pvcreate /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
 ```
 ```
 server1:~# pvcreate /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
   Physical volume "/dev/sdb1" successfully created
   Physical volume "/dev/sdc1" successfully created
   Physical volume "/dev/sdd1" successfully created
   Physical volume "/dev/sde1" successfully created
   ```
   Now run
   ```
   pvdisplay
   ```
   to learn about the current state of your physical volumes:
   ```
   server1:~# pvdisplay
   --- NEW Physical volume ---
   PV Name               /dev/sdb1
   VG Name
   PV Size               23.29 GB
   Allocatable           NO
   PE Size (KByte)       0
   Total PE              0
   Free PE               0
   Allocated PE          0
   PV UUID               G8lu2L-Hij1-NVde-sOKc-OoVI-fadg-Jd1vyU
 
   --- NEW Physical volume ---
   PV Name               /dev/sdc1
   VG Name
   PV Size               23.29 GB
   Allocatable           NO
   PE Size (KByte)       0
   Total PE              0
   Free PE               0
   Allocated PE          0
   PV UUID               40GJyh-IbsI-pzhn-TDRq-PQ3l-3ut0-AVSE4B
 
   --- NEW Physical volume ---
   PV Name               /dev/sdd1
   VG Name
   PV Size               23.29 GB
   Allocatable           NO
   PE Size (KByte)       0
   Total PE              0
   Free PE               0
   Allocated PE          0
   PV UUID               4mU63D-4s26-uL00-r0pO-Q0hP-mvQR-2YJN5B
 
   --- NEW Physical volume ---
   PV Name               /dev/sde1
   VG Name
   PV Size               23.29 GB
   Allocatable           NO
   PE Size (KByte)       0
   Total PE              0
   Free PE               0
   Allocated PE          0
   PV UUID               3upcZc-4eS2-h4r4-iBKK-gZJv-AYt3-EKdRK6
   ```
   Now let's create our volume group fileserver and add /dev/sdb1 - /dev/sde1 to it:
   ```
   vgcreate fileserver /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
   ```
   ```
   server1:~# vgcreate fileserver /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
   Volume group "fileserver" successfully created
   ```
   Let's learn about our volume groups:
   
   ```
   vgdisplay
   ```
   ```
   server1:~# vgdisplay
   --- Volume group ---
   VG Name               fileserver
   System ID
   Format                lvm2
   Metadata Areas        4
   Metadata Sequence No  1
   VG Access             read/write
   VG Status             resizable
   MAX LV                0
   Cur LV                0
   Open LV               0
   Max PV                0
   Cur PV                4
   Act PV                4
   VG Size               93.14 GB
   PE Size               4.00 MB
   Total PE              23844
   Alloc PE / Size       0 / 0
   Free  PE / Size       23844 / 93.14 GB
   VG UUID               3Y1WVF-BLET-QkKs-Qnrs-SZxI-wrNO-dTqhFP
   ```
   
   Another command to learn about our volume groups:
   ```
   vgscan
   ```
   ```
   server1:~# vgscan
   Reading all physical volumes.  This may take a while...
   Found volume group "fileserver" using metadata type lvm2
   ```
   For training purposes let's rename our volumegroup fileserver into data:
   ```
   vgrename fileserver data
   ```
   ```
   server1:~# vgrename fileserver data
   Volume group "fileserver" successfully renamed to "data"
   ```
   
   Next we create our logical volumes share (40GB), backup (5GB), and media (1GB) in the volume group fileserver. Together they use a little less than 50% of the available space (that way we can make use of RAID1 later on):
   
   ```
  lvcreate --name share --size 40G fileserver
  ```
  ```
server1:~# lvcreate --name share  --size 40G fileserver
   Logical volume "share" created
 ```
 ```
lvcreate --name backup --size 5G fileserver
```
```
server1:~# lvcreate --name backup --size  5G fileserver
   Logical volume "backup" created
 ```
 ```
lvcreate --name media --size 1G fileserver
```
```
server1:~# lvcreate --name media  --size  1G fileserver
   Logical volume "media" created
   ```
   Let's get an overview of our logical volumes:
```
lvdisplay
```
```
server1:~# lvdisplay
   --- Logical volume ---
   LV Name                /dev/fileserver/share
   VG Name                fileserver
   LV UUID                280Mup-H9aa-sn0S-AXH3-04cP-V6p9-lfoGgJ
   LV Write Access        read/write
   LV Status              available
   # open                 0
   LV Size                40.00 GB
   Current LE             10240
   Segments               2
   Allocation             inherit
   Read ahead sectors     0
   Block device           253:0
 
   --- Logical volume ---
   LV Name                /dev/fileserver/backup
   VG Name                fileserver
   LV UUID                zZeuKg-Dazh-aZMC-Aa99-KUSt-J6ET-KRe0cD
   LV Write Access        read/write
   LV Status              available
   # open                 0
   LV Size                5.00 GB
   Current LE             1280
   Segments               1
   Allocation             inherit
   Read ahead sectors     0
   Block device           253:1
 
   --- Logical volume ---
   LV Name                /dev/fileserver/media
   VG Name                fileserver
   LV UUID                usfvrv-BC92-3pFH-2NW0-2N3e-6ERQ-4Sj7YS
   LV Write Access        read/write
   LV Status              available
   # open                 0
   LV Size                1.00 GB
   Current LE             256
   Segments               1
   Allocation             inherit
   Read ahead sectors     0
   Block device           253:2
   ```
   
   Until now we have three logical volumes, but we don't have any filesystems in them, and without a filesystem we can't save anything in them. Therefore we create an ext3 filesystem in share, an xfs filesystem in backup, and a reiserfs filesystem in media:
   
   ```
   mkfs.ext3 /dev/fileserver/share
   ```
   ```
   server1:~# mkfs.ext3 /dev/fileserver/share
 mke2fs 1.40-WIP (14-Nov-2006)
 Filesystem label=
 OS type: Linux
 Block size=4096 (log=2)
 Fragment size=4096 (log=2)
 5242880 inodes, 10485760 blocks
 524288 blocks (5.00%) reserved for the super user
 First data block=0
 Maximum filesystem blocks=0
 320 block groups
 32768 blocks per group, 32768 fragments per group
 16384 inodes per group
 Superblock backups stored on blocks:
         32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
         4096000, 7962624
 
 Writing inode tables: done
 Creating journal (32768 blocks): done
 Writing superblocks and filesystem accounting information: done
 
 This filesystem will be automatically checked every 23 mounts or
 180 days, whichever comes first.  Use tune2fs -c or -i to override.
 ```
Repeate the above instruction for all new partations

Now we are ready to mount our logical volumes. I want to mount share in /var/share, backup in /var/backup, and media in /var/media, therefore we must create these directories first:

```
mkdir /var/media /var/backup /var/share
```
You can automount this 
