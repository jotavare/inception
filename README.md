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

- - - -

### PORT FORWARDING
#### Configure SSH
- `nano /etc/ssh/sshd_config`
- If port 22 is being used by the school - `#Port 22` to `Port 42` 
- `#PermitRootLogin prohibit-password` to `PermitRootLogin yes`
- Optional - `#PasswordAuthentication yes` to `PasswordAuthentication yes`
- Save and exit file - `Ctrl` + `X` > `Y` > `Enter`

#### Restart services
- `service ssh restart`
- `service sshd restart`
- `service ssh status`

#### Configure Firewall
| Description           | Command         |
| --------------------- | --------------- |
| Check status          | `ufw status` or `ss -tunlp` |
| Enable ufw            | `ufw enable`    |
| Open port 42 (SSH)    | `ufw allow 42`  |
| Open port 80 (HTTP)   | `ufw allow 80`  |
| Open port 443 (HTTPS) | `ufw allow 443` |
| Close virtual machine | `shutdown now`  |


#### Port forwarding
- Go to our virtual machine `Settings` in VirtualBox;
- `Network` > `Advanced` > `Port Forwarding`;
- Add the same ports allowed in the firewall;

| Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
| ---- | -------- | ------- | --------- | -------- | ---------- |
| `SSH`   | `TCP` | `<empty>` | `42`  | `<empty>`| `42`  |
| `HTTP`  | `TCP` | `<empty>` | `80`  | `<empty>`| `80`  |
| `HTTPS` | `TCP` | `<empty>` | `443` | `<empty>`| `443` |

#### Login with OS terminal
- Open a terminal in your main OS;
- `ssh root@localhost -p 42` or `ssh root@<vm ip address> -p 42`;
- You can check for known ssh hosts with `cat ~/.ssh/known_hosts`;

- - - -

### STORING CONFIGURATION
> [!NOTE]
> Why is the below important? If something goes wrong in the future (believe me that it will), we can always restore a specific snapshot or download our configuration from the cloud.

#### Create snapshot
- Open the VirtualBox;
- `Left Click` on top of the icon of your VM and choose `Snapshots`;
- Click on `Take`;
- Write a name like `Basic Inception Configuration` and a description for future reference;

#### Save on cloud
- Go to the VirtualBox folder and compress the `Inception` folder;
- Also you can use the `Export` function in VirtualBox;
- Upload to the internet, usually 1-2 GB;

#### Open in a different pc
- Find the main folder of VirtualBox;
- Uncompress it inside;
- Open VirtualBox and it should appear everything;

- - - -

### PRE CONFIGURE DOCKER
#### Sudo configuration
- Login to virtual machine through ssh;
- Open the file `nano /etc/sudoers`;
- In `# User privilege specification` add bellow `<intra user> ALL=(ALL:ALL) ALL`;
- Save and exit file `Ctrl` + `X` > `Y` > `Enter`;

#### Add user to docker group
- Add user to groups `sudo usermod -aG docker <intra user>`;
- Check user groups `groups <intra user>`;

#### Test configuration
- Switch user `su <intra user>`;
- Go to the home directory `cd ~/`;
- Test docker `git clone https://github.com/codesshaman/simple_docker_nginx_html.git`;
- Build docker `docker-compose up -d`;
- Open Firefox and browse `172.17.0.1` (localhost) or `<vm ip>` (bridged adapter);
- If it should appear `My html config is work!`;

#### Create project directories and files
- Create .sh file `nano make_inception.sh`;
- Open it and paste the following code:
```bash
#!/bin/bash
mkdir project
mkdir project/srcs
touch project/Makefile
mkdir project/srcs/requirements
touch project/srcs/docker-compose.yml
touch project/srcs/.env
echo "DOMAIN_NAME=<your_nickname>.42.fr" > project/srcs/.env
echo "CERT_=./requirements/tools/<your_nickname>.42.fr.crt" >> project/srcs/.env
echo "KEY_=./requirements/tools/<your_nickname>.42.fr.key" >> project/srcs/.env
echo "DB_NAME=wordpress" >> project/srcs/.env
echo "DB_ROOT=rootpass" >> project/srcs/.env
echo "DB_USER=wpuser" >> project/srcs/.env
echo "DB_PASS=wppass" >> project/srcs/.env
mkdir project/srcs/requirements/bonus
mkdir project/srcs/requirements/mariadb
mkdir project/srcs/requirements/mariadb/conf
touch project/srcs/requirements/mariadb/conf/create_db.sh
mkdir project/srcs/requirements/mariadb/tools
echo "" > project/srcs/requirements/mariadb/tools/.gitkeep
touch project/srcs/requirements/mariadb/Dockerfile
touch project/srcs/requirements/mariadb/.dockerignore
echo ".git" > project/srcs/requirements/mariadb/.dockerignore
echo ".env" >> project/srcs/requirements/mariadb/.dockerignore
mkdir project/srcs/requirements/nginx
mkdir project/srcs/requirements/nginx/conf
touch project/srcs/requirements/nginx/conf/nginx.conf
mkdir project/srcs/requirements/nginx/tools
touch project/srcs/requirements/nginx/Dockerfile
echo ".git" > project/srcs/requirements/mariadb/.dockerignore
echo ".env" >> project/srcs/requirements/mariadb/.dockerignore
mkdir project/srcs/requirements/tools
mkdir project/srcs/requirements/wordpress
mkdir project/srcs/requirements/wordpress/conf
touch project/srcs/requirements/wordpress/conf/wp-config-create.sh
mkdir project/srcs/requirements/wordpress/tools
echo "" > project/srcs/requirements/wordpress/tools/.gitkeep
touch project/srcs/requirements/wordpress/Dockerfile
touch project/srcs/requirements/wordpress/.dockerignore
echo ".git" > project/srcs/requirements/wordpress/.dockerignore
echo ".env" >> project/srcs/requirements/wordpress/.dockerignore
```
- Save and exit file `Ctrl` + `X` > `Y` > `Enter`;
- Give permissions to file `chmod 777 make_inception.sh`;
- Run script to create all necessary folders and files `./make_inception.sh`;

- - - -

### CHANGE DOMAIN AND INSTALL CERTIFICATES
#### Install mkcert
Certainly! Here's your process formatted into a markdown table:

| Step                                      | Command                                         |
|-------------------------------------------|-------------------------------------------------|
| Login to the virtual machine (NAT)        | `ssh root@localhost -p 42`                      |
| Login to the virtual machine (Bridged Adpter) | `ssh root@<vm_ip_address> -p 42`            |
| Update list of repositories               | `sudo apt update -y`                            |
| Install utilities for mkcert              | `sudo apt install -y wget curl libnss3-tools`   |

- Download mkcert binary;
```bash
curl -s https://api.github.com/repos/FiloSottile/mkcert/releases/latest| grep browser_download_url  | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -```
```

| Step                                      | Command                                         |
|-------------------------------------------|-------------------------------------------------|
| Rename the binary                         | `mv mkcert-v*-linux-amd64 mkcert`               |
| Give all permissions                      | `chmod 777 mkcert`                              |
| Move mkcert to bin directory              | `sudo mv mkcert /usr/local/bin/`                |
| Check mkcert version                      | `mkcert --version`                              |
