# notas_windows-OS

ansible en wsl 
https://www.jeffgeerling.com/blog/2017/using-ansible-through-windows-10s-subsystem-linux

winget 
https://github.com/microsoft/winget-cli/releases

-configuración virtualbox en wsl 
export PATH=$PATH:/mnt/c/Windows/System32
export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"

-vagrant en wsl
apt install -y build-essential ruby-full ruby-all-dev libvirt-dev
apt install -y vagrant
vagrant plugin install vagrant-libvirt

-configuración de vagrant en wsl
[automount]
enabled = true
options = "metadata,umask=22,fmask=11"

-DNS
[network]
generateHosts = true
generateResolvConf = true

-instalación SSH cliente/servidor 
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
Get-NetFirewallRule -Name *ssh*
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort PORT