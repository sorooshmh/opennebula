**Deploying OpenNebula on 2 Servers in HA mode:**

This playbook install opennebula on 2 servers which are in HA modes.It means one server is in master mode and another in slave mode and follow the master.


**Requirements**

2 servers( centos7) for opennebulas

1 server ( centos7) for kvm machine

1 server ansible machine

Vmware workstation for test scenario


**Before Any Installation:**

You should set hostname for each machines for example one machine openmaster and another openslave.

Set IPs and hostnames on /etc/hosts if you don't have any dns server in your environment.

On each opennebula servers you should set 4 NICs which will bond each other in related playbook.

You need an ansible server that can communicate with the other machines in order to excute the playbooks.


**The setup:**

It contains a bunch of yml files which create structure of ansible provision and you can clone this and create a path in your ansible server and copy opennebula project in your provision directory in ansible server.All playbooks have their own path and being placed in tasks directories.

mkdir -p /home/ansible/provision

git clone https://github.com/sorooshmh/opennebula.git

mv opnenebula/* /home/ansible/provision

**Describe playbooks:**


**bond:**

This playbook use to bond NICs and put them in 2 groups( bond0 and bond1).Put your desired IPs in ansible-playbook command and execute it.

      ansible-playbook bond.yml -i inventory/bond --tags=Add_bond -e '{ "bond0_ip": "192.168.180.11"}' -e '{ "bond1_ip": "192.168.190.11"}' -e '{ "bond0_gw": "192.168.180.1"}' -e '{ "bond1_gw": "192.168.190.1"}'
      

**opennebula:**

This playbook can create 2 opennebula servers at the same time
         ansible-playbook opennebula.yaml -i inventory/opennebula -vv
         
         
**open-ha:**

This playbook can create a HA environment.
          ansible-playbook open-ha.yml -i inventory/open-ha -vv
         
         
**kvm:**

This playbook can create a KVM virtualization and add this host to opennebula.
          ansible-playbook kvm.yml -i inventory/kvm -vv
          
          
**Usage:**

When all playbooks have finished you can connect to gui in web http://your-opennebula-ip:9869/. You can find the webui user/pass in ~oneadmin/.one/one_auth
          
          

        

