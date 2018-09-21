# Ubuntu-init

## create user as administrator


adduser example_user

adduser example_user sudo


## set auto upgrade
https://help.ubuntu.com/lts/serverguide/automatic-updates.html.en

sudo apt install unattended-upgrades


config file:
/etc/apt/apt.conf.d/50unattended-upgrades


enable automatic update:

vi /etc/apt/apt.conf.d/20auto-upgrades:

{

APT::Periodic::Update-Package-Lists "1";

APT::Periodic::Download-Upgradeable-Packages "1";

APT::Periodic::AutocleanInterval "7";

APT::Periodic::Unattended-Upgrade "1";

}

## install firewall
https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/

sudo apt install ufw

sudo ufw default allow outgoing

sudo ufw default deny incoming


ufw config file:

/etc/default/ufw

## secure ssh
https://www.linode.com/docs/security/securing-your-server/

### 1. disable root login over ssh

sudo vi /etc/ssh/sshd_config

PermitRootLogin no

### 2. disable shh password authentication

sudo vi /etc/ssh/sshd_config

PasswordAuthentication no

### 3. listen on only one internet protocol

-AddressFamily inet listen ipv4

-AddressFamily inet6 listen ipv6

-AddressFamily is not in sshd_config by default

	echo 'AddressFamily inet' | sudo tee -a /etc/ssh/sshd_config

### 4. restart ssh

sudo systemctl restart sshd