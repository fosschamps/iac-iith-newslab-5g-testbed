To setup ethernet interfaces, vlan interfaces, bridge interfaces on the workstation
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e "target_host=nfvsrv1" playbooks/setup_ethernets.yml
```

```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e "target_host=nfvsrv1" playbooks/setup_bridges.yml
```

To download qcow2 image to the host (bare-metal server or workstation)
```
# cd /var/lib/libvirt/images/
$ wget https://cdimage.debian.org/images/cloud/bookworm/20260210-2384/debian-12-generic-amd64-20260210-2384.qcow2
```

To setup Core switch and DNS server LXDs
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"lxds_to_provision": ["natrtr", "coresw", "dnssrv"]}' playbooks/setup_lxds.yml
```

```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' -e 'target_host="natrtr"' playbooks/setup_nat_router_using_linux_kernel.yml
```

```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="coresw"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_core_router_using_linux_kernel.yml
```


```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="dnssrv"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_dns_server_bind9.yml
```


To setup a VM for MAAS region controller in a target
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"vms_to_provision": ["maas-regctrl"]}' playbooks/setup_vms.yml
```

To setup an LXD for MAAS rack controller in a target
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"lxds_to_provision": ["maas-rackctrl"]}' playbooks/setup_lxds.yml
```

To setup MAAS region controller in a given target
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="maas-regctrl"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_maas_regctrl.yml
```

To setup MAAS rack controller in a given target
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host="maas-rackctrl"' -e 'ansible_ssh_common_args="-o ProxyJump=maruthisi@10.9.64.176"' playbooks/setup_maas_rackctrl.yml
```

To setup a test VM which gets IP address from MAAS
```
$ ansible-playbook -i ~/iac-iith-newslab-5g-testbed/inventory/hosts.yml -e 'target_host=nfvsrv1' -e '{"vms_to_provision": ["testvm1"]}' playbooks/setup_vms.yml
```


