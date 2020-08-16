# notas_windows-OS

-ansible en wsl 
https://www.jeffgeerling.com/blog/2017/using-ansible-through-windows-10s-subsystem-linux

-winget 
https://github.com/microsoft/winget-cli/releases

-virtualbox en wsl 
# virtualbox - agregar a .bashrc
export PATH=$PATH:/mnt/c/Windows/System32
export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"

-vagrant en wsl
# instalación
apt install -y build-essential ruby-full ruby-all-dev libvirt-dev
apt install -y vagrant
vagrant plugin install vagrant-libvirt

-configuración de vagrant en wsl
# agregar a /etc/wsl.conf
[automount]
enabled = true
options = "metadata,umask=22,fmask=11"
# DNS
[network]
generateHosts = true
generateResolvConf = true

-SSH 
# listar OpenSSH
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'
# instalación del cliente
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
# instalación del servidor
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
# inicio del servicio
Start-Service sshd
# creación del servicio y activación al inicio
Set-Service -Name sshd -StartupType 'Automatic'
# chequeo de regla en firewall
Get-NetFirewallRule -Name *ssh*
# si la regla no existe la crea
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort PORT