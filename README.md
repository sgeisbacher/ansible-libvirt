Role Name
=========

A role to set up Libvirt with KVM as well as create KVM machines. Forked from https://github.com/hicknhack-software/ansible-libvirt

Role Variables
--------------

### Download state
``` yaml
libvirt_image_url : The url of the image 
```

### For Running a VirtualMachine

``` yaml

libvirt_domain:
  # basic arguments
  groups: [] # names of Ansible nodes/groups used to provision the domain
  name: # name/uuid of the domain (empty means new uuid)
  title: '' # title of the vm
  description: '' # description of the vm
  apt_mirror: ''
  # note: if you do not provide a domain_id each run will create a new vm!

  # default VM configuration
  vm:
    memory: "512MiB" # RAM memory available to the VM
    vcpu: 1 # number of cores designated to the VM
    vcpu_placement: 'static' # options 'auto', 'static', defaults to 'numatune'
    vcpu_cpuset: [] # list of host CPU numbers the VM can run on
    networks: ['default'] # libvirts id of networks this VM is part of
    disk_size: "12G" # use this to change first disk size
    features: ['acpi', 'apic', 'pae'] # vm features available

libvirt_cloud_config_default_user:
  name: 'ubuntu'
  gecos: 'Ubuntu'
  ssh-authorized-keys: ['']
```



Example Playbook
----------------

To set up the host. 

    - hosts: localhost
	  remote_user: root
	  roles:
	    - kireledan.libvirt
	  vars:
	    state: install

To Create a VM

``` yaml
- hosts: localhost
  remote_user: root
  roles:
    - ../ansible-libvirt
  vars:
    state: create
    libvirt_domain:
      groups: ['cluster'] 
      name: 'Testing'
      title: 'Machine1' 
      description: 'test'
    libvirt_image_url: "https://cloud-images.ubuntu.com/trusty/current/trusty-server-cloudimg-amd64-disk1.img"

```


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
