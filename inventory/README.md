To setup ethernet interfaces, vlan interfaces, bridge interfaces on the workstation
<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' -e "target_host=nfvsrv1" playbooks/setup_ethernets.yml
```
</pre>

<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' -e "target_host=nfvsrv1" playbooks/setup_bridges.yml
```
</pre>

To download qcow2 image to the host (bare-metal server or workstation)
<pre>
```
# cd /var/lib/libvirt/images/
$ wget https://cdimage.debian.org/images/cloud/bookworm/20260210-2384/debian-12-generic-amd64-20260210-2384.qcow2
```
</pre>

To setup Core switch and DNS server LXDs
<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"lxds_to_provision": ["natrtr", "coresw", "dnssrv"]}' playbooks/setup_lxds.yml
```
</pre>

<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' -e 'target_host="natrtr"' playbooks/setup_nat_router_using_linux_kernel.yml
```
</pre>

<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="corertr"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_core_router_using_linux_kernel.yml
```
</pre>


<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="dnssrv"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_dns_server_bind9.yml
```
</pre>


To setup a VM for MAAS region controller in a target
<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"vms_to_provision": ["maas-regctrl"]}' playbooks/setup_vms.yml
```
</pre>

To setup an LXD for MAAS rack controller in a target
<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"lxds_to_provision": ["maas-rackctrl"]}' playbooks/setup_lxds.yml
```
</pre>

To setup MAAS region controller in a given target
<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="maas-regctrl"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_maas_regctrl.yml
```
</pre>

To setup MAAS rack controller in a given target
<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="maas-rackctrl"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_maas_rackctrl.yml
```
</pre>

To setup a test VM which gets IP address from MAAS
<pre>
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"vms_to_provision": ["testvm1"]}' playbooks/setup_vms.yml
```
</pre>


