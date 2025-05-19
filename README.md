
## Ansible Ops: SSH-Access-Mgmnt.yml

#### Document on SSH-Access-Mgmnt on newly launched SSDNodes-VM - AlmaLinux9.X 

### Pre-requisites
1. Ansible-Ops: zabbix-ansible-ops-ssdn-236 [209.182.234.346]
2. Renote Host: New launched SSDNodeds VM [209.182.234.xxx]
   

##### Step-1: Launch new VM using ssdones Web Console and Login (SSH) via root credential
###### Note: Password is available in the SSDNodes console
```shell
$ ssh root@209.182.234.xxx
$ root@209.182.234.xxx's password:
```

##### Step-2: Login Zabbix-Ansible-Ops-SSDN-236 [209.182.234.236] with your available username (key-based)
```shell
$ ssh azim@209.182.234.236 -p 3914
```

##### Step-3: Copy id_rsa.pub key of Zabbix-Ansible-Ops-SSDN-236 and pest into /root/.ssh/authorized_keys of newly launched ssdnodes remote VM
```shell
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCPZVCJDflQS7nTKvbKN4IsCkt1fKixNbHm1AfxIwka+w3hQz26tMIGnl7oaLHmA2SFiOCR7CA5emG6z2TIN+JUi/1c63+7kNvgKJfokw/u4DEch/MIgv43pbL3j1Qy2dxIQ2k74Y0mtSjHpLbtImkFjCxPITrTjCopiUGBRBwZH/J6IEdJcDnyw/MWnzH/IR8Eo0UVjZ1wFYAhnvY71kNqB0QdOKvJABkVj341bQz3ukF3Q5uPK0IIa2D+vowjKtLswW5yUm9jZ87DvRmq3w2vvFP2kKZGGj/tNjRl5gP0pV75F+Vn1vMeYBO4Yc+wTn4SKjmdOuc+NtV8RVx3M6d5 root@zabbix-ansible-ops-ssdn-236
```
###### Note: You can verify the access from zabbix-ansible-ops-ssdn-236 to remote VM, please remember to logout after verifying.
```shell
ssh root@209.182.234.xxx
```

##### Step-4: Set IP of remote VM IP into ansible hosts and inventory file
```shell
nano /etc/ansible/hosts
[servers]
209.182.234.xxx ansible_user=root

nano /etc/ansible/inventory
[servers]
209.182.234.xxx ansible_user=root
```

##### Step-5: Now set the username(s) (you want to create into new remote VM) in the ansible playbook: ssh-user-mgmnt.yml 
```shell
nano /etc/ansible/ssh-user-mgmnt/ssh-user-mgmnt.yml
vars:
  user_list:
  apurba
  azim
  imran
  mahrab
  mamun
  mim
  mushfiq
  rashed
  sabaoon
  syuji
  tamoi
  towfiq 
```
###### Note: Assign only those users who need to access the new remote VM.


##### Step-6: You can verify whether the playbook configuration is correct or not.
```shell
ansible-playbook --check ssh-user-mgmnt.yml
```

##### Step-7: Finaly run the playbook and verify your access to the new VM using your username & key
```shell
$ ansible-playbook --i servers ssh-user-mgmnt.yml
$ ssh azim@209.182.234.xxx -p 3914
```
