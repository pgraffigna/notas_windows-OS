# notas_windows-OS

ansible en wsl 
[jeff geerlings blog](https://www.jeffgeerling.com/blog/2017/using-ansible-through-windows-10s-subsystem-linux)

winget [winget-github](https://github.com/microsoft/winget-cli/releases)

## configuración virtualbox en wsl 
```console
 export PATH=$PATH:/mnt/c/Windows/System32
 export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
 export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
```
## vagrant en wsl
```console
 apt install -y build-essential ruby-full ruby-all-dev libvirt-dev
 apt install -y vagrant
 vagrant plugin install vagrant-libvirt
```
## configuración de vagrant en wsl
```console
[automount]
enabled = true
options = "metadata,umask=22,fmask=11"
```
## DNS
```console
[network]
generateHosts = true
generateResolvConf = true
```
## instalación SSH cliente/servidor en windows 10
```console
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'
Add-WindowsCapability -Online -Name OpenSSH.Client
Add-WindowsCapability -Online -Name OpenSSH.Server
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
Get-NetFirewallRule -Name *ssh*
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort PORT
```
