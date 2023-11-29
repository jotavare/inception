### TOOLS
- [VirtualBox](https://www.virtualbox.org/) `Website`
- [Debian](https://www.debian.org/) `Website`

- - - -

### CREATE A NEW VIRTUAL MACHINE
#### Name and operating system
- **Name:** `Inception`
- **Machine Folder:** `/home/jotavare/VirtualBox VMs`
- **Type:** Linux
- **Version:** Debian (64-bit)

#### Memory size
- [x] `1024 MB` (4-8 GB RAM) or `4096 MB` (16 GB RAM or above)

#### Hard disk
- [ ] Do not add a virtual hard disk
- [x] Create a virtual hard disk now
- [ ] Use an existing virtual hard disk file

#### Hard disk file type
- [x] VDI (VirtualBox Disk Image)
- [ ] VHD (Virtual Hard Disk)
- [ ] VMDK (Virtual Machine Disk)

#### Storage on physical hard disk
- [x] Dynamically allocated
- [ ] Fixed size

#### File location and size
- [x] `8,00 GB`

#### Choose a disk file
- [x] Settings > Storage > Click on `Empty` > Click on disk icon > `Choose a disk file...` > Insert Debian .iso

> [!NOTE]
> You can add more processor cores to the virtual machine if needed. Settings > System > Processor.

- - - -

### INSTALL DEBIAN OS
- `TAB` - move
- `Space` - select
- `Enter` - confirm

#### Debian GNU/Linux installer menu (BIOS mode)
- [ ] `Graphic Install`
- [x] `Install`
- [ ] `Advanced options`
- [ ] `Accessible dark contrast installer menu`
- [ ] `Help`
- [ ] `Install with speech synthesis`

#### Select a language
- [x] `English`

#### Select your location
- [x] `other` > `Europe` > `Portugal`

#### Configure locales
- [x] `United States`

#### Configure the keyboard
- [x] `American English`

#### Configure the network
- [x] Hostname: `Inception`
- [x] Domain name: `<empty>`

#### Set up users and passwords
- [x] Root password: `<password easy to remember>`
- [x] Full name for the new user: `<intra username>`
- [x] Username for your account: `<intra username>`
- [x] Choose a password for the new user: `<password easy to remember>`

#### Configure the clock
- [x] `Lisbon`
- [ ] `Madeira Islands`
- [ ] `Azores`

#### Partition method
- [x] `Guided - use entire disk`
- [ ] `Guided - use entire disk and set up LVM`
- [ ] `Guided - use entire disk and set up encrypted LVM`
- [ ] `Manual`

#### Select disk to partition
- [x] `SCSI3 (0,0,0) (sda) - 8.6 GB ATA VBOX HARDISK`

#### Partition scheme
- [x] `All files in one partition (recommended for new users)`

#### Partition disks
- [x] `Finish partitioning and write changes to disk`
- [x] Write the changes to disks? `Yes`

#### Configure the package manager
- [x] Scan extra installation media? `No`
- [x] `Portugal`
- [x] `deb.debian.org`
- [x] HTTP proxy information (blank for none): `<empty>`

#### Configure popularity-contest
- [x] Participate in the package usage survey? `No`

#### Software selection
- [x] `SSH server`

#### Install the GRUB boot loader
- [x] Install the GRUB boot loader to your primary drive? `Yes`

#### Configuring grub-pc
- [ ] Enter device manually
- [x] `/dev/sda (ata-VBOX_HARDISK_VB2e44d73e-45a0c522)`

#### Finish the installations
- [x] `Continue`

- - - -

### INSTALL NECESSARY SOFTWARE
#### Login to the system
- Start the virtual machine
- Select `Debian GNU/Linux`
- Inception login: `root`
- Password: `<insert the same password from the previous installation>`

#### Update repository list
- `apt update`

#### Install necessary applications
- `apt install -y sudo ufw docker docker-compose make openbox xinit kitty firefox-esr`

#### Check applications
- `startx` > `right click with mouse` > `Applications`
- `Internet` > `Firefox ESR` - Opens Firefox.
- `System` > `kitty` - Opens the terminal.

> [!NOTE]
> If everything opens and appears right you can close with `right click with mouse` > `Exit` > `Exit`
