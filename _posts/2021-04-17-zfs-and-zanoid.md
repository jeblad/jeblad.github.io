---
layout: post
language: en
created: 2021-04-17 13:43:00 (CEST)
modified: 2021-04-24 12:20:00 (CEST)
title: ZFS and zanoid
tagline: a better file system with snapshots
description: How to set up ZFS to get a good security, and a lot better backup strategy, without wasting a fortune.
categories :
  - other
tags :
  - zfs
  - zanoid
  - backup
  - data integrity
  - data retention
  - data safety
  - data security
authors:
  - jeblad
licenses:
  - cc-by-nc-nd-4.0
---

This post is a response to discussions about how I prefer to set up storage space on my development computers, and whether that could be of interest to other users. I prefer to be able to rollback and redo my work in case of problems, which is somewhat tainted of my own experiences. Other users may view things differently.

<!--more-->

{% include opinion.html %}

Several years ago I used [software RAID](https://www.dataplugs.com/en/software-raid-vs-hardware-raid-advantages-disadvantages/) to set up mirrored RAID 1 (mirroring) for my home directory, carefully testing the configuration to check out what was fastest, also against hardware RAID. I found software RAID to be faster than hardware RAID, and larger blocks to be quite much faster than smaller blocks. On top of this I previously put various encrypted file systems.

Usually I have a main disk for the system, and this is separate from the disk for my home. This makes it possible to unplug the home and reinstall the system without having to move the home folder or partition. I feel lot more secure when the home disk is disconnected, instead of constantly trying to track which partitions are safe to reinstall. In addition I have a cold store for backup.

All disks in my new setup use [ZFS](https://wiki.ubuntu.com/ZFS) file system with [zpool](https://wiki.ubuntu.com/ZFS/ZPool) as logical volume manager.

### SSDs and HDD

Both system and home are SSD disks, it does not make sense to use anything else, with 240 GB for the system and a 1 TB for the home. The system disk also has the swap partition. I have a special SSD disk for swap use, but as the durability of ordinary SSDs have increased, I have dropped this. The home disk is a 1 TB disk, it seems sufficient for my use, at least for the moment.

I use an ordinary HDD (spinning disk) for backup, and use a disk that is somewhat bigger than twice the sum of system and home. To keep power down I use a 2.5" disk, and spin it down when not used. The reason for using a HDD is that storage on magnetic platter may survive a lightning strike (an EMP pulse) while that would completely wipe an SSD. Even if the electronics in the HDD is fried to dust it is still possible to regenerate the content from the platter.

Some consideration should be made whether the disks should have upgradeable firmware, as some are supported through the Linux ecosystem while others are not.

### Unencrypted system, encrypted swap

To simplify boot up I have chosen to use an unencrypted disk for system, and this has some consequences for whether swap is encrypted. It is not a given that encrypted swap imply encrypted system, that only holds for full-disk encryption. It is better in my opinion to encrypt the swap partition with a random key, but then there is no way of resuming after hibernation, unless you have a secure storage for the key, that is you have a [TPM module](https://trustedcomputinggroup.org/resource/trusted-platform-module-tpm-summary/) (which I don't). That means you must either run without encrypted swap, or hibernation don't work. I prefer to skip hibernation, as encrypted swap is more important to me.

<p class="note">Newer installs of ZFS on Ubuntu, at least on 20.04.2 LTS seems to create a too small swap partition for hibernation to work properly. Swap must be able to save the complete memory, and my install turned up with partition of only 25% of my memory. That makes hibernation quite risky.</p> 

<p class="note">Using a TPM still demands use of a password or some other token to stop a cold boot attack. The reason is that the TPM module is a token itself, and bound to the computer, and thus can't be used as the sole source for credentials. At the same time you need a single password (or token) for access to the computer.</p>

This follows the scheme where the system storage is assumed to need low-grade protection, while the running system is what needs protection. In my case the system disk needs physical access control, that is a locked enclosure. That also means swap needs protection against tampering, but only after someone has gained physical access. If someone has gained physical access, then the machine can be booted up, but important stuff can't be gleaned from the swap.

### Encrypted home

The home directory is a home pool made by zpool, with an encrypted ZFS file system (a dataset) for each user. These file systems are encrypted with the same password users use for log in. To make this work a small script must be added to [PAM](https://www.redhat.com/sysadmin/pluggable-authentication-modules-pam), all this is described at [Linux homedir encryption ](https://talldanestale.dk/2020/04/06/zfs-and-homedir-encryption/).

<p class="note">Enforcing strong passwords are a must! I've been wondering about using additional tokens, but haven't made up my mind.</p>

When all is up and running there is a homepool that holds a set of file systems, and each one will not be decrypted and mounted before the user logs in. Nothing is set up before the user logs in.

### Regular snapshots

My idea was to make sure the home disk had a high degree of survivability. My own experience over time has shown me that hardware failure is not the real problem, human failure is, and what I need is a way to solve those cases. That has lead me to believe that a working backup is more important than hardware redundancy. If a disk fail, then I much rather have a working backup.

Previously I've been using [Déjà Dup](https://wiki.gnome.org/Apps/DejaDup) to make backups. This is a graphical user interface for the backup program [Duplicity](http://duplicity.nongnu.org/) that itself uses [librsync](https://github.com/librsync/librsync) and writes tar-archives. Because creating those tar-archives is a very slow process, I only takes incremental backups during the night.

After changing to ZFS for the home directories I have decided to do something similar for my backup, and swap out duplicity for for [zrepl](https://zrepl.github.io/) or [zanoid](https://github.com/jimsalterjrs/sanoid/) instead. Those make snapshots of ZFS file systems at regular intervals. The homedir may fail critically, but it can be recreated from snapshots stored at the backup. If homedir is still alive and kicking, then it can be swapped out for a new disk without any problem. Because it is a HDD, it may fail and still be possible to recreate it from the platter. If for some reason it is important to keep the history, then the HDD can be put in a RAID (mirrored), but it could be better to create an off-site copy from time to time.

The zrepl/zanoid snapshot utility is set up to create a new snapshot each hour, and collect them for slightly more than two weeks. Then it will keep one snapshot for each day for two months, and after that one for each week. Because snapshots are small and compact, they takes little space, and as long as the backup disk is somewhat larger than the file systems it copies, it should be sufficient. Exactly how much larger is not clear, it is dependent on the actual content.

This setup is sufficient for my purpose.
