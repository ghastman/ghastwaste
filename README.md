# ghastwaste
The Ghastwaste Cluster  

The Players:  
One Jetson Nano  
Eight Raspberry Pi 4  
Four tired AMD PC  
One WSL2 PC

Rocky 8.10  
https://rockylinux.org/download  

Note the README for the Pi image  
https://dl.rockylinux.org/pub/sig/8/altarch/aarch64/images/README.txt  

## On nodes  
sudo rootfs-expand  
sudo adduser ghastman   
sudo passwd ghastman  
sudo usermod -aG wheel ghastman   

## On Widows 11 Install Rocky 10 in WSL2  
https://learn.microsoft.com/en-us/windows/wsl/install  
wsl --install  
wsl --update  
wsl --install --from-file C:\Users\ghast\Downloads\Rocky-10-WSL-Base.latest.x86_64.wsl --name rocky-10  

## Update /etc/hosts in WSL2
Add entries to /etc/wsl.conf to disable autogeneration of /etc/hosts by WSL2.  
[network]  
generateHosts = false  

Add local network machines to /etc/hosts  

## Push SSH keys  
scp -rp ~/.ssh a10-9700e:~/  
scp -rp ~/.ssh jetson-nano:~/  
scp -rp ~/.ssh raspberry-pi4b-01:~/  
scp -rp ~/.ssh raspberry-pi4b-02:~/      
scp -rp ~/.ssh raspberry-pi4b-03:~/      
scp -rp ~/.ssh raspberry-pi4b-04:~/  
scp -rp ~/.ssh raspberry-pi4b-05:~/  
scp -rp ~/.ssh raspberry-pi4b-06:~/  
scp -rp ~/.ssh raspberry-pi4b-07:~/  
scp -rp ~/.ssh raspberry-pi4b-08:~/  
scp -rp ~/.ssh phenom-925:~/  	
scp -rp ~/.ssh phenom-965:~/  	
scp -rp ~/.ssh ryzen-5-2600:~/  

## Get base updates done
sudo dnf update

## Add EPEL Repo for Rocky
https://wiki.rockylinux.org/rocky/repo/  

sudo dnf config-manager --set-enabled crb  
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-10.noarch.rpm  

## Get git working  
sudo dnf install git  
git config --global user.name "My Name"  
git config --global user.email "myemail@example.com"  
git config --global init.defaultBranch main  
git config --global credential.helper store  

## Clone this repo locally  
mkdir ~/Workspace  
git clone https://github.com/ghastman/ghastwaste.git ~/Workspace/ghastman/ghastwaste  

## Ansible  
sudo dnf install ansible-collection-ansible-posix.noarch ansible-collection-community-general.noarch ansible-test.noarch ansible-core.noarch  

### From the deployment dir...  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags hello_world  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags facts_os  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags facts_cpu  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags facts_memory  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags test_speed_disk  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags test_speed_internet  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags test_speed_cpu  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags update  

## Oneshot cleanups
ansible-playbook -i inventories/staging/hosts.yaml remove_cockpit.yaml  