# linux-general
A repo dedicated to linux, install, quirks with hardware or software and notes


## How to Install Linux 

This guide may not be entirely clear, I've installed Linux mutliple times now, so I can find my way around some common issues. This is not a dual boot guide for existing windows systems, though there are great guides online that can guide you through an installation. This guide is more geared towards a fresh install which is what I find myself doing nowadays. 

Wanna know how to do Linux on UEFI boot by following a longer more thorough guide? https://www.rodsbooks.com/linux-uefi/

### Starting with the Hardrives 

You probably have some drives that you're going to install linux on, most will want to do a windows and linux system. In that case there are a couple of concepts to understand 

1) BIOS vs. UEFI 

- TLDR: This is the type of firmware running on top of the motherboard, it really is in charge of how your computer boots. BIOS is older, what the system sometimes calls legacy boot. UEFI is newer and has some advantages over BIOS.

Majaro explains: https://wiki.manjaro.org/index.php/Some_basics_of_MBR_v/s_GPT_and_BIOS_v/s_UEFI

A bigger guide to BIOS vs. UEFI: https://www.happyassassin.net/posts/2014/01/25/uefi-boot-how-does-that-actually-work-then/

2) MBR vs. GPT 

- TLDR: MBR and GPT are partitioning schemes for your harddrives, how your harddrive splits the drive up into different plots of memory. Generally UEFI can access both MBR and GPT but BIOS can only really access MBR.  

Both links above also cover MBR vs. GPT

3) Ext4 vs. NFTS vs. FAT32

- TLDR: These are popular file systems for operating system use. Linux uses Ext4, MTFS is used by Windows and FAT32 is a general purpose format used in different cases. 


### Actually Installing Linux (after preparing drives)

To prepare the harddrives for installation in UEFI mode, you probably should have recognized that your drives need to be partitioned properly

1) Boot a live linux USB - I choose Ubuntu or LinuxMint for simplicity of troubleshooting and a vast amount of Googleable questions (sue me)

  - NOTE you must BOOT your USB in the style that you want to install to drive i.e. if you want a UEFI Linux boot, then boot the USB from UEFI mode in the motherboard, otherwise boot from Legacy/BIOS

2) Use Gparted to delete some of the partitions on the desired drive

  - I remember reading somewhere that a drive cannot be GPT partitioned if 3 or more partitions exist. If so delete the necessary partitions. 

3) Format the necessary drive into GPT. The following commands may help when choosing MBR and GPT for different drives. 

```
    parted - for an all-in-one partition and formatting system
    fdisk - for old MBR-type partition tables (limited to 2TB per partition)
    gdisk - for newer, larger GPT partition tables
```

A good guide on MBR to GPT: https://www.cpqlinux.com/convert-disk-mbr-to-gpt-on-linux/ or https://serverfault.com/questions/963178/how-do-i-convert-my-linux-disk-from-mbr-to-gpt-with-uefi


4) Assuming you've partitioned your drives you can set the file system type 

```
sudo mkfs.ntfs /dev/sda OR sudo mkfs.ext4 /dev/sda
```

5) Okay so the drives are set up properly now onto the installation. If you've converted your desired windows drive to GPT and are happy with the size, go ahead and install Windows on it. The rest of the guide is for linux only. At this point your drive is essentially split into a Windows GPT drive with NTFS file system. And a GPT drive for linux.  

6) What to do with the space we've allocated for linux? Here's the recommendation when you're in the linux installer for Gparted

MAJORITY: Space for actual OS installation and local linux files 
FORMAT: Ext4

SWAPSPACE (OPITIONAL but RECOMMENDED): Which as a rule of thumb can be from half the size of your RAM to double the size of your RAM 
FORMAT: linux-swap/swap

information on swap: https://help.ubuntu.com/community/SwapFaq

EFI (ESP) SYSTEM PARTITION: UEFI needs this to boot the drive; I would recommend 256 MB+
FORMAT: FAT32

7) The installer will also ask you where it should keep the bootloader somewhere (I forget where in the installation) the answer is '/' and ON the harddrive that you are installing the Linux installation to, the WHOLE hardrive not a particular partition. This is where the GRUB menu sits. 


8) Some issues with GRUB and their solutions

GRUB menu dissapears: https://medium.com/@leijerry888/get-grub-menu-back-after-installing-ubuntu-20-04-alongside-windows-dab5de5afc37

Get a more modern GRUB menu: https://linuxmint-user-guide.readthedocs.io/en/latest/grub.html




