# CPANEL CENTOS XENSERVER
cpanel_centos_xenserver
## make cpanel at centos inside xenserver
Disable NetworkManager dan menggunakan Network
```bash
systemctl stop NetworkManager.service
systemctl disable NetworkManager.service
systemctl enable network.service
systemctl start network.service
```
## Disable Firewalld (Centos 7)
```bash
iptables-save > ~/firewall.rules
systemctl stop firewalld.service
systemctl disable firewalld.service
```
## Edit SELINUX
```bash
nano /etc/selinux/config
find and edit > SELINUX=disabled
```
Rubah port SSH ke 3322	 	 
## Setting hostname
Update hostname
```bash
hostnamectl set-hostname <NAMA HOSTNAME/SERVER>
cek hostname
```
# hostnamectl status
reboot if needed
# VM Tools
```bASH
Install XenTools, Jika VM Shared Hosting menggunakan VM dari XenServer wajib untuk install xentools, agar informasi management VM dapat di tampilkan di XenCenter
Pilih iso guest-tools.iso dari tab console VM di XenCenter
create direktori /mnt/cdrom untuk mounting iso tersebut
mount iso
```
# mount /dev/cdrom /mnt/cdrom
```bash
install XenTools
cd /mnt/cdrom/Linux
./install.sh
unmount /mnt/cdrom
```
reboot jika perlu
 	 
# ADDITIONAL PACKAGE
1	EPEL-RELEASE
```bash
yum install -y epel-release
``` 	 
2	Additional package
```bash
yum makecache fast
yum -y install git bash-completion bash-completion-extras tmux htop telnet
```
# CHECK-MK AGENT
1	Install check-mk agent
```bash
yum install -y  check-mk-agent xinetd 
systemctl enable xinetd
systemctl start xinetd
```
## check usiing telnet
telnet localhost 6556
# CPANEL
1	Install Cpanel
```bash
cd /home 
curl -o latest -L https://securedownloads.cpanel.net/latest 
sh latest
``` 
2	Config Basic WebHost Manager® Setup
email
IP address , harus sama dengan IP address yang di setting di NIC0
NameServers
3	
Config Server Time
Asia/Jakarta
4	
Config Statistics Software Configuration
Awstat
5	
Config Apache mod_userdir Tweak
Enable mod_userdir Protection
6	
Config cPHulk Brute Force Protection
Disable (jika perlu)
7	
Config PHP open_basedir Tweak
Enable php open_basedir Protection.
8	
Config Edit System Mail Preferences
Forward mail for “nobody” to: root
Forward mail for “cpanel” to: emailserver@jogja.camp
Forward mail for “root” to:  emailserver@jogja.camp
9	
Config DirectoryIndex Priority
Home » Service Configuration » Apache Configuration » DirectoryIndex Priority
underconstruction.html
underconstructions.html
....
10	
Configure Backup
Home » Backup » Backup Configuration
11	
Configure DNS Cluster
Home » Clusters » DNS Cluster
DNS Role : Synchronize Changes
12	
Install Auto SSL Provider Let's Encrypt
# /scripts/install_lets_encrypt_autossl_provider
Home » SSL/TLS » Manage Auto SSL
Tab Providers
Centang Let's Encrypt di Choose an AutoSSL provider
Centang I agree to these terms of service. 
Klik Save
Tab Options
Centang Allow AutoSSL to replace invalid or expiring non-AutoSSL certificates.
Klik Save
CLOUDLINUX
1	
Install CloudLinux
# wget https://repo.cloudlinux.com/cloudlinux/sources/cln/cldeploy
# sh cldeploy -k <CLKEY>
# reboot
2	
Update Key CL
Jika menggunakan template VM yang sudah terinstall CloudLinux sebelumnya, update Key Cloudlinux

## cldetect --update-new-key <CLKEY>
 	 
SOFTACULOUS
1	
Enable ioncube

WHM -> Tweak Settings -> PHP --> "Enable ioncube"
Install Softaculous

# wget -N http://files.softaculous.com/install.sh
# chmod 755 install.sh
# ./install.sh --quick
Configure Softaculous , enable script

WHM -> Plugins -> Softaculous-Instant Installs -> Software -> General Scripts 
 
- WordPress
- Joomla
- Drupal
- phpBB
- SMF
- PrestaShop
- OpenCart
- osCommerce
- Magento
- Laravel
- CodeIgniter
- Moodle
- Open Journal Systems
 	 
PHP Selector
1	
Install php Selector

# yum groupinstall alt-php
 	 
MultiPHP ini
1	
Tambahkan setting PHP disable_functions

WHM -> Software -> MultiPHP INI Editor -> Editor Mode -> Pilih Versi php -> find disable_functions
 
Icon
 disable_function complete
 	 
Easy Apache
1	
Setting default easy apache

WHM -> Softare -> Easy
Pilih, upload template .json dari http://wiki.jcamp.biz/download/attachments/15925355/EA4-mbog.json?api=v2
Sesuaikan/rubah/edit jika perlu.
 

 	 
CageFs
1	
Install CageFS

# yum install cagefs -y
# cagefstcl --init
 	 
Modsec
1	
Dari salt master eksekusi command berikut:

state modsec
salt 'hostname' state.sls modsec
 	 
MODSEC CMC
 	 
1	
Install ModSec Menu

# cd /root
# wget https://download.configserver.com/cmc.tgz
# tar -xf cmc.tgz
# cd cmc
# sh install.sh
 	 
CSF
1	
Install CSF

# wget https://download.configserver.com/csf.tgz
# tar -xvzf csf.tgz 
# cd csf
# sh install.sh 
# perl /usr/local/csf/bin/csftest.pl
# vi /etc/csf/csf.conf
Allow port

3322,4505,4506,6556
deaktifasi testing mode

TESTING = "0"
 	 
LiteSpeed PLUGINS
 	 
1	
Install LSWS CPANEL/WHM Plugin

# cd;
# wget https://www.litespeedtech.com/packages/cpanel/lsws_whm_plugin_install.sh
# sh lsws_whm_plugin_install.sh
 	 
Cloudflare PLUGINS	 	 
1	
Install cloudflare plugins

# wget https://raw.githubusercontent.com/cloudflare/CloudFlare-CPanel/master/cloudflare.install.sh
# chmod +x cloudflare.install.sh
# ./cloudflare.install.sh -k 80d890cf6852c248adeafec556873171 -n 'PT JC Indonesia'
 	 
Sitepad plugins	 	 
1	
Install sitepad plugins

# wget -N http://files.sitepad.com/install.sh
# chmod 755 install.sh
# ./install.sh
