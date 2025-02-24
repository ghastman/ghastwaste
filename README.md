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

scp -rp ~/.ssh raspberrypi-01:~/  
scp -rp ~/.ssh raspberrypi-02:~/  
scp -rp ~/.ssh raspberrypi-03:~/  
scp -rp ~/.ssh raspberrypi-04:~/  
scp -rp ~/.ssh raspberrypi-05:~/  
scp -rp ~/.ssh raspberrypi-06:~/  
scp -rp ~/.ssh raspberrypi-07:~/  
scp -rp ~/.ssh raspberrypi-08:~/  

## Ansible  
sh ansible_packages.sh  

### From the deployment dir...  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags hello_world  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags facts_os  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags facts_cpu  
ansible-playbook -i inventories/staging/hosts.yaml common.yaml  --tags update  
