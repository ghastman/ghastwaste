# ghastwaste
The Ghastwaste Cluster  

The Players:  
One Jetson Nano  
Eight Raspberry Pi 4  
One tired AMD PC  

Rocky 8.10  
https://rockylinux.org/download  

Note the README for the Pi image  
https://dl.rockylinux.org/pub/sig/8/altarch/aarch64/images/README.txt  

## On nodes  
sudo rootfs-expand  
sudo adduser ghastman   
sudo passwd ghastman  
sudo usermod -aG wheel ghastman   

## Push SSH keys  
scp -rp ~/.ssh raspberrypi-01:~/  
scp -rp ~/.ssh raspberrypi-02:~/  
scp -rp ~/.ssh raspberrypi-03:~/  
scp -rp ~/.ssh raspberrypi-04:~/  
scp -rp ~/.ssh raspberrypi-05:~/  
scp -rp ~/.ssh raspberrypi-06:~/  
scp -rp ~/.ssh raspberrypi-07:~/  
scp -rp ~/.ssh raspberrypi-08:~/  


## Get base updates done
sudo dnf update

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
sh ansible_packages.sh  

### From the deployment dir...  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags hello_world  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags facts_os  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags facts_cpu  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags update  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags cockpit  