# HP-MI-1.2-Ubuntu---HP-Mini-Linux-Factory-Restore-Image
HP Mi 1.2 / "Dennis" — Recovered HP Mini Linux Factory Restore Image  This repository documents the recovery and preservation of **HP Mi (Mobile Internet) 1.2**, an HP-customized Ubuntu distribution shipped for some HP Mini netbooks around 2009.  The recovered image is an authentic HP factory restore image, traced through archived HP support pages, original HP restore-creator software, and finally an image URL embedded inside HP's own Linux restore utility.

The image was successfully written to USB and installed on original-period HP Mini hardware.

---

## What was recovered

The recovered factory image identifies itself as:


'DISTRIB_ID="HP Mi (Mobile Internet)"
DISTRIB_RELEASE=1.2
DISTRIB_DESCRIPTION="HP Mi (Mobile Internet)"
Its underlying Ubuntu release is:'
Ubuntu 8.04.2
The installer identifies itself as:
Welcome to the dennis-1-2-20090417-2 installer
The supplied kernel is:
Linux 2.6.24-22-lpia
The image dates internally to approximately April 17, 2009.
This is an LPIA build intended for Intel Atom-era netbooks rather than an ordinary contemporary x86 Ubuntu desktop image.
How it was found
The interesting part of this recovery was not merely locating an old disk image.
The trail began with fragmentary references to HP's old Linux restore utilities for the HP Mini family.
Archived HP support pages exposed two HP SoftPaq-style object IDs:
Windows restore creator:
ob-68017-1

Linux restore creator:
ob-68020-1
Those pages led to the original HP-hosted files:
ImageCreator.msi

liveusb-creator-ubuntu_0.3.3netbook0dennis5_all.deb
Remarkably, the corresponding files were still available from HP's servers in 2026.
The Linux package was then unpacked.
Inside it was:
/etc/liveusb-creator-ubuntu.cfg
That configuration file contained the original factory-image location:
ftp://ftp.hp.com/pub/softlib/software10/COL25940/dennis-stable-install-usb-gm-1.img
Changing the transport from FTP to HTTPS revealed that the original image itself was also still present on HP's servers:
https://ftp.hp.com/pub/softlib/software10/COL25940/dennis-stable-install-usb-gm-1.img
This gave us a provenance chain of:
Archived HP support page
        ↓
HP restore-creator product ID
        ↓
Original HP restore-creator package
        ↓
HP configuration file
        ↓
Original HP factory-image URL
        ↓
Factory image downloaded directly from HP
        ↓
Hash verification
        ↓
Successful install on real HP Mini hardware
That chain is the primary reason I consider this image substantially better authenticated than the many unlabeled or repackaged HP Mini images that occasionally appear in old software archives.
Recovered files and hashes
HP Mi factory image
Filename:
dennis-stable-install-usb-gm-1.img

Size:
1,154,482,176 bytes

SHA-256:
6778E5136F1D954726E0B0A5D4F7C5A2D3B624399CF99A977C13998C8366E43F

MD5:
5B4B213778FADD6347F7C32CAE0FCC02
The MD5 also matched the ETag returned by HP's server when the image was recovered.
HP MIE Restore Image Creator — Windows
Filename:
ImageCreator.msi

Size:
863,744 bytes

SHA-256:
8E4369C18923D05783768641B416E84B0941AD479225D8891B703320F9BB4F7B
HP MIE Restore Image Creator — Linux
Filename:
liveusb-creator-ubuntu_0.3.3netbook0dennis5_all.deb

Size:
830,568 bytes

SHA-256:
5C6884F6008229828C9C792F2285E17F24E5D8F77CD8FDC4A0830AB9A78935E8
The Debian package identifies itself as:
Package: liveusb-creator-ubuntu
Version: 0.3.3netbook0dennis5
Architecture: all
Description: HP MIE Restore Image Creator
Image structure
The restore image is not a conventional partitioned hard-disk image.
It is a bootable FAT32 superfloppy-style image with no normal MBR partition table.
Important files include:
ldlinux.sys
syslinux.cfg
boot.msg
vmlinuz
initrd0.img
rootfs.img
bootfs.img
install.sh
install.cfg
hwcheck.sh
dmid
recovery/
rootfs.img and bootfs.img are SquashFS images.
Some tools such as fdisk may misinterpret bytes in the FAT boot sector as a bogus partition table. blkid correctly identifies the outer image as FAT/VFAT.
The "Dennis" name
The internal build name appears repeatedly throughout the image.
Examples include:
dennis-1-2-20090417-2
dennis-media-samples
dennis-help
/usr/bin/dennis-lock
/etc/X11/xorg.conf.dennis
More than one hundred installed packages contain dennis in their package versioning.
There is also an HP-modified Ubuntu package carrying the maintainer:
Dennis Kaarsemaker <dennis@ubuntu.com>
Further research showed this to be github user @seveas , long time Ubuntu contributor. 
HP customization
This was much more than stock Ubuntu with an HP wallpaper.
The installation contains a heavily customized HP/Canonical netbook environment with its own launcher and dashboard.
The primary interface includes categories such as:
Internet
Media
Utilities
Work
Play
All
Applications visible in the recovered installation include OpenOffice.org Writer, Calc, Impress and Draw, Adobe Reader 8, Mozilla Firefox, Sunbird, gEdit, Nautilus, games, media software, and a number of HP-specific components.
Examples of customized packages and components include:
ume-config-base
ume-config-harbour
hp-tbird-theme
hp-browser-toolbar
hp-browser-tabbar
hpmini.ko
HP rfkill HAL configuration
Elisa media software
Skype 2.0.0.72
Firefox 3.0.8
The original APT configuration points to Canonical repositories created specifically for HP's Mini Linux work:
deb http://hpmini.archive.canonical.com/mie/ hardy main universe multiverse restricted
deb-src http://hpmini.archive.canonical.com/mie/ hardy main universe multiverse restricted

deb http://hpmini.archive.canonical.com/mi/ hardy-hpmini public
deb-src http://hpmini.archive.canonical.com/mi/ hardy-hpmini public
Hardware validation
The recovered factory image was written to USB and booted on an original-period HP Mini.
The installer completed successfully and the resulting system booted into the full HP Mi environment.
The tested machine is from the HP Mini 110 family, using an Intel Atom N270-class platform with 2 GB RAM.
The resulting installation is remarkably responsive on this hardware, particularly compared with attempting to run a modern Linux distribution on the same Atom-era machine.
That performance difference is itself historically interesting: HP Mi represents software designed specifically around the capabilities and limitations of the netbook hardware it shipped beside.
Important model/provenance distinction
The particular HP Mini used during this research originally shipped with Windows XP.
Therefore, I am not claiming that this exact image was the factory recovery image originally supplied with that individual machine.
What is established is that:
- this is an authentic HP-hosted HP Mi 1.2 factory restore image;
- HP distributed it for the HP Mini product family;
- HP's own restore-creator package directly references it;
- its internal software identifies itself as HP Mi 1.2;
- and it successfully operates on compatible HP Mini hardware.
This distinction matters when documenting historical software.
WARNING: the installer is destructive
The original installer was designed as a factory restore mechanism.
It does not behave like a modern interactive Linux installer.
Among other operations, it can:
erase the beginning of the target disk
repartition the internal drive
create filesystems
install the operating system
install GRUB
create the HP recovery environment
The recovery interface itself warns that existing data will be erased.
Do not boot the installer on a machine containing data you want to preserve.
Use spare hardware, a blank disk, or an emulator when examining it.
Hardware check
The installer contains an HP Mini hardware check broadly equivalent to:
/tmp/install/dmid |
    grep 'Product Name:' |
    grep -ie 'HP' -ie 'Compaq' |
    grep -i 'Mini'
This helps explain why the restore environment is able to operate across more than one closely related HP Mini model.
Historical significance
HP's Mini Linux distributions now occupy an awkward part of computing history.
They appeared during the brief netbook boom, when manufacturers were experimenting with purpose-built Linux interfaces for inexpensive Atom-powered computers.
Much of the surrounding infrastructure has disappeared:
old HP support pages
Canonical HP Mini repositories
product documentation
software indexes
FTP-based download paths
Yet, in this case, enough fragments survived to reconstruct the original distribution chain.
The especially unusual part is that the final factory image was not recovered from a random mirror or third-party upload.
It was rediscovered by following metadata from HP's own archived support material into HP's own restore software, which in turn pointed back to an image that was still present on HP's servers roughly seventeen years later.
Preservation goals
The goal of this project is historical preservation and documentation.
Useful future work includes:
- cataloguing every HP-specific package in the image;
- extracting package versions and dependency information;
- reconstructing the original HP/Canonical repository contents where possible;
- documenting the custom HP Mi shell and user interface;
- comparing HP Mi 1.2 with the earlier HP MIE releases;
- identifying other surviving "Dennis" builds;
- mapping supported HP Mini models;
- documenting recovery-partition behavior;
- preserving screenshots and video from original hardware.
Terminology: MIE vs Mi
HP used several closely related names during this period.
Earlier material commonly refers to:
HP MIE
HP Mobile Internet Experience
The recovered April 2009 system identifies itself specifically as:
HP Mi (Mobile Internet) 1.2
The restore utility itself still uses the older HP MIE Restore Image Creator name.
For that reason, documentation around this system may contain both terms.
Original factory image name
The original HP filename is:
dennis-stable-install-usb-gm-1.img
The combination of the dennis codename, stable, and gm strongly suggests this was a production/general-availability build rather than an ordinary development snapshot, although the precise meaning of every component of HP's internal naming convention has not yet been independently documented.
Preservation status
The following have been preserved together with hashes and provenance information:
dennis-stable-install-usb-gm-1.img
ImageCreator.msi
liveusb-creator-ubuntu_0.3.3netbook0dennis5_all.deb
archived HP support-page material
Wayback/CDX metadata
README / provenance notes
SHA256SUMS
MD5SUMS
A separate preservation copy has also been retained read-only.
Credits
HP and Canonical created the original software.
This repository exists only to document and preserve a largely forgotten part of netbook/Linux history.
The rediscovery was performed through software archaeology using archived HP documentation, surviving HP-hosted software packages, package inspection, filesystem analysis, and validation on period hardware.
If you have original HP Mini documentation, HP MIE/Mi restore media, other Dennis builds, screenshots, recovery discs, package repositories, or contemporary documentation from this project, contributions are very welcome.
