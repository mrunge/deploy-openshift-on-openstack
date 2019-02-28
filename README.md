# deploy-openshift-on-openstack
Snippets and doc to deploy openshift on openstack

```
git clone https://github.com/openshift/openshift-ansible
```
Download a keystonerc, create *enough* quota to create resources.

Then 
```
cp -r openshift-ansible/playbooks/openstack/sample-inventory/ inventory
```
You probably want to adjust `inventory/group_vars/all.yml`
Fields to adjust: `openshift_openstack_public_dns_domain` etc.

It is also important to note, that you'll have to make sure, DNS works; this also includes DNS resolution in internal networks. 
I've set up dns updates from the playbooks, `openshift_openstack_use_nsupdate` is the key here. Also don't forget to set the name of the external network name.

```
ansible-playbook --user openshift \
  -i openshift-ansible/playbooks/openstack/inventory.py \
  -i inventory \
  openshift-ansible/playbooks/openstack/openshift-cluster/provision.yml
  ```
  will create vms to deploy openshift on.
  
  The cluster itself is deployed by
  ```
  ansible-playbook --user openshift \
  -i openshift-ansible/playbooks/openstack/inventory.py \
  -i inventory \
  openshift-ansible/playbooks/openstack/openshift-cluster/install.yml
```
