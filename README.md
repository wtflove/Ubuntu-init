#Ubuntu-Init

##Create User As Administrator
adduser example_user<br>
adduser example_user sudo<br>
<br>
##Set Auto-Upgrade
[Official Instruction](https://help.ubuntu.com/lts/serverguide/automatic-updates.html.en)<br>
sudo apt install unattended-upgrades<br>
<br>
###Config File Path: <br>
/etc/apt/apt.conf.d/50unattended-upgrades<br>
<br>
###Enable Automatic Update:<br>
vi /etc/apt/apt.conf.d/20auto-upgrades:<br>
{<br>
APT::Periodic::Update-Package-Lists "1";<br>
APT::Periodic::Download-Upgradeable-Packages "1";<br>
APT::Periodic::AutocleanInterval "7";<br>
APT::Periodic::Unattended-Upgrade "1";<br>
}<br>
<br>
##Install Firewall<br>
[Instruction](https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/)<br>
sudo apt install ufw<br>
sudo ufw default allow outgoing<br>
sudo ufw default deny incoming<br>
<br>
###ufw Config File:<br>
/etc/default/ufw<br>
<br>
##Secure ssh:<br>
[Instruction](https://www.linode.com/docs/security/securing-your-server/)<br>
<br>
### 1. Disable Root Login Over ssh<br>
sudo vi /etc/ssh/sshd_config<br>
set:<br>
PermitRootLogin no<br>
<br>
### 2. disable shh password authentication<br>
sudo vi /etc/ssh/sshd_config<br>
Set:<br>
PasswordAuthentication no<br>
<br>
### 3. Listen on Only One Internet Protocol<br>
echo 'AddressFamily inet' | sudo tee -a /etc/ssh/sshd_config<br>
(AddressFamily is not in sshd_config by default)<br>
_AddressFamily inet listen IPv4_ listening on IPv4<br>
_AddressFamily inet6 listen IPv6_ listening on IPv6<br>


### 4. Restart ssh
sudo systemctl restart sshd<br>