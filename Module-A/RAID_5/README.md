<p align="center">
  <a>
    <img src="../img/raid_5.png" alt="RAID 5" width="160" height="160">
  </a>
  <h1 align="center">RAID 5</h1>
</p>

### Step 1: Installing 'mdadm' and Verify Drives

````
apt install mdadm
````

After the ``mdadm`` package installation, let’s list the four 2GB disks which we have added to our system using ``fdisk`` command.

````
fdisk -l | grep sd
````

Now it’s time to examine the attached four drives for any existing RAID blocks on these drives using the following command.

````
mdadm --examine /dev/sdb /dev/sdc /dev/sdd /dev/sde
````

### Step 2: Partitioning the Disks for RAID

First and foremost, we have to partition the disks (/dev/sdb, /dev/sdc, /dev/sdd and /dev/sde) before adding to a RAID, So let us define the partition using the ``fdisk`` command, before forwarding it to the next steps.

````
fdisk /dev/sdb
fdisk /dev/sdc
fdisk /dev/sdd
fdisk /dev/sde
````

Please follow the below instructions to create a partition on the ``/dev/sdb`` drive.

- Press ``n`` for creating a new partition.

- Then choose ``P`` for the Primary partition. Here we are choosing Primary because there are no partitions defined yet.

- Then choose ``1`` to be the first partition. By default, it will be 1.

- Here for cylinder size, we don’t have to choose the specified size because we need the whole partition for RAID so just Press Enter two times to choose the default full size.

- Next press ``p`` to print the created partition.

- Use ``w`` to write the changes.

Create /dev/sdb Partition

After creating partitions, check for changes in all four drives sdb, sdc, & sdd.

````
mdadm --examine /dev/sdb /dev/sdc /dev/sdd /dev/sde
````

### Step 3: Creating md device ``md0``

````
mdadm --create /dev/md0 --level=5 --raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
````

After creating raid device, check and verify the RAID, devices included, and RAID Level from the ``mdstat`` output.

````
cat /proc/mdstat
````

````
watch -n1 cat /proc/mdstat
````

After the creation of the raid, Verify the raid devices using the following command.

````
mdadm -E /dev/sd[b-e]1
````

Next, verify the RAID array to assume that the devices which we’ve included in the RAID level are running and started to re-sync.

````
mdadm --detail /dev/md0
````

### Step 4: Creating file system for ``md0``

````
mkfs.ext4 /dev/md0
````

Now create a directory under ``/mnt`` then mount the created filesystem under ``/mnt/raid5`` and check the files under mount point, you will see the lost+found directory.

````
mkdir /mnt/raid5
mount /dev/md0 /mnt/raid5/
ls -l /mnt/raid5/
````

### Step 5: Save Raid 5 Configuration

````
mdadm --detail --scan --verbose >> /etc/mdadm.conf
````