# Ubuntu-Init
## Create User As Administrator
adduser example_user<br>
adduser example_user sudo<br>
## Set Auto-Upgrade
[Official Instruction](https://help.ubuntu.com/lts/serverguide/automatic-updates.html.en)<br>
sudo apt install unattended-upgrades<br>
### Config File Path:
/etc/apt/apt.conf.d/50unattended-upgrades<br>
### Enable Automatic Update:
vi /etc/apt/apt.conf.d/20auto-upgrades:<br>
{<br>
APT::Periodic::Update-Package-Lists "1";<br>
APT::Periodic::Download-Upgradeable-Packages "1";<br>
APT::Periodic::AutocleanInterval "7";<br>
APT::Periodic::Unattended-Upgrade "1";<br>
}<br>
## Install Firewall:
[Instruction](https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/)<br>
sudo apt install ufw<br>
sudo ufw default allow outgoing<br>
sudo ufw default deny incoming<br>
### ufw Config File:
/etc/default/ufw<br>
## Secure ssh:
[Instruction](https://www.linode.com/docs/security/securing-your-server/)<br>
### 1. Disable Root Login Over ssh:
sudo vi /etc/ssh/sshd_config<br>
set:<br>
PermitRootLogin no<br>
### 2. disable shh password authentication
sudo vi /etc/ssh/sshd_config<br>
Set:<br>
PasswordAuthentication no<br>
### 3. Listen on Only One Internet Protocol
echo 'AddressFamily inet' | sudo tee -a /etc/ssh/sshd_config<br>
(AddressFamily is not in sshd_config by default)<br>
_AddressFamily inet listen IPv4_ listening on IPv4<br>
_AddressFamily inet6 listen IPv6_ listening on IPv6<br>
### 4. Restart ssh
sudo systemctl restart sshd<br>