# How to Install Linux 

This guide may not be entirely clear, I've installed Linux mutliple times now, so I can find my way around some common issues. This is not a dual boot guide for existing windows systems, though there are great guides online that can guide you through an installation. This guide is more geared towards a fresh install which is what I find myself doing nowadays. 

## Starting with the Hardrives 

You probably have some drives that you're going to install linux on, most will want to do a windows and linux system. In that case there are a couple of concepts to understand 

1) BIOS vs. UEFI 

- TLDR: This is the type of firmware running on top of the motherboard, it really is in charge of how your computer boots. BIOS is older, what the system sometimes calls legacy boot. UEFI is newer and has some advantages over BIOS.

2) MBR vs. GPT 

- TLDR: MBR and GPT are partitioning schemes for your harddrives, how your harddrive splits the drive up into different plots of memory. Generally UEFI can access both MBR and GPT but BIOS can only really access MBR.  

3) Ext4 vs. NFTS vs. FAT32

- TLDR: These are popular file formats for operating system use. Linux uses Ext4, MTFS is used by Windows and FAT32 is a general purpose format used in different cases. 

