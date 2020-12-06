V2V Engine - Ansible
====================

This project provides a set of playbooks to execute a migration plan. Some
configuration has to provided to the engine, such as the providers
credentials, the infrastructure mappings and the migration plans.

The default place to store the configuration is `./v2v_config` and this
repository provides examples for each king of file.

TODO: Describe the format of configuration files

Dependencies
------------

This engine has been tested with **Ansible 2.9**. On Red Hat Enterprise Linux 8,
we can install it with the following commands:

```
$ sudo subscription-manager repos --enable=ansible-2.9-for-rhel-8-x86_64-rpms
$ sudo dnf install ansible
```

We also need to install `pyvmomi` library as it is used by VMware modules.
On Red Hat Enterprise Linux 8, it is provided by the Advanced Virtualization
repository. We can install it with the following commands:

```
$ sudo subscription-manager repos --enable=advanced-virt-for-rhel-8-x86_64-rpms
$ sudo dnf module reset virt
$ sudo dnf module enable virt:8.3
$ sudo dnf install python3-pyvmomi
```

Usage
-----

```
ansible-playbook run_migration_plan.yml -i inventory -e 'migration_plan=my_plan'
```

Variables
---------

| Name | Default Value | Decription |
| v2v_config_path | ./v2v_config | Path to the configuration |
| v2v_migration_plan | UNDEF | Name of the migration plan to run |

Migration plan file
-------------------

```yaml
v2v_infrastructure_mapping: mapping1
v2v_vms_in_plan :
  - vm1
  - vm2
v2v_virt_v2v_max_time : 30000
v2v_virt_v2v_refresh_delay : 15
```

Infrastructure mapping file
---------------------------

```yaml
v2v_im_providers : array of hashes {"source": "src_provider", "destination": "dst_provider"}
v2v_im_clusters : array of hashes {"source": "src_cluster", "destination": "dst_cluster"}
v2v_im_networks : array of hashes {"source": "src_network", "destination": "dst_network"}
v2v_im_storages : array of hashes {"source": "src_storage", "destination": "dst_storage"}
v2v_im_transport_method : choices['vddk', 'ssh']
```

