# Ubuntu-init

# create user as administrator

adduser example_user
adduser example_user sudo

# set auto upgrade
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

# install firewall
https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/

sudo apt install ufw
sudo ufw default allow outgoing
sudo ufw default deny incoming

ufw config file:
/etc/default/ufw