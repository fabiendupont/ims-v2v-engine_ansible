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

Some of the tasks require **Ansible 2.5.3+**. On Fedora 28, you can get it
through `updates-testing` repo:

```
yum update ansible --enablerepo=updates-testing
```

You also need to install `pyvmomi` library as it is used by VMware modules.
On Fedora 28, it's as easy as:

```
yum install python2-pyvmomi
```

Usage
-----

```
ansible-playbook run_migration_plan.yml -e 'migration_plan=my_plan'
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

