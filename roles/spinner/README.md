## Spinner role for migrating between Oss without data movement in Ceph

This is a procedure for migrating an existing ceph cluster daemons between OS distribution without data movement. 
The main purpose for this role is to provide the ability of switching between different linux distributions such as RHEL, Ubuntu, Centos etc without initiating any data movement in ceph. The process will only cause temporary degredation until new OS is installed on the server. 

## installation 
To run this role, you should import it as one of your roles in the ansible roles directory, and point it to your inventory file which contains osds,mgrs,mons,rgws ini sections. 

There are three key variables in this playbook: 

* mighost - represents the migrated host, consider using the ansible_hostname as the playbook filters tasks by it. 
* action - represents weather a removal/addition is needed (in our use case, first removal and then addition). 
* clustername - the default should be 'ceph', if you have configured a different name, use it. 

Spinner role will know by itself which daemons are installed by the inventory file configuration, it is important to feed the right data into that file. In case you want to remove a specific daemon and not the other one, you can limit the execution with --l flag (not supported for collocated configurations). 

To run this playbook, please change the needed variables and then run the following: 
```bash 
ansible-playbook site.yml -i <inventory_file> -b 
```




