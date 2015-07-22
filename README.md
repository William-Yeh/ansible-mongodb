
williamyeh.mongodb for Ansible Galaxy
============


[![Circle CI](https://circleci.com/gh/William-Yeh/ansible-mongodb.svg?style=shield)](https://circleci.com/gh/William-Yeh/ansible-mongodb)


## Summary

Role name in Ansible Galaxy: **[williamyeh.mongodb](https://galaxy.ansible.com/list#/roles/4405)**

This Ansible role has the following features for MongoDB:

 - Install specific version.
 - Handlers for restart/reload/stop events;
 - Bare bone configuration (*real* configuration should be left to user's template files; see **Usage** section below).




## Role Variables

### Mandatory variables

None.




### Optional variables

User-configurable defaults:

```yaml
# MongoDB version; e.g., "3.0.4"
# Will install the default (usually the latest stable) version, if not specified.
mongodb_version


# which components to install?
# possible values:
#  - "mongod"
#  - "mongos"
mongodb_components: [ "mongod" ]


# install mongod as a config server?
mongodb_configsvr: false

# TCP port of config server
mongodb_configsvr_port: 27019



# use `service` command to start/restart mongodb daemon?
mongodb_use_service:  True
```


User-installable configuration files (by Ansible's template system):

```yaml
# mongod conf template to be installed to "/etc/mongod.conf";
# relative to `playbook_dir`
mongodb_mongod_conf

# mongos conf template to be installed to "/etc/mongos.conf";
# relative to `playbook_dir`
mongodb_mongos_conf

```




## Handlers

**mongod**:

- `restart mongod`
- `reload mongod`
- `stop mongod`


**mongos**:

- `restart mongos`
- `reload mongos`
- `stop mongos`




## Usage


### Step 1: add role

Add role name `williamyeh.mongodb` to your playbook file.


### Step 2: add variables

Set vars in your playbook file.

Simple example:

```yaml
---
# file: simple-playbook.yml

- hosts: all

  roles:
    - williamyeh.mongodb

  vars:
    mongodb_version: 3.0.4
```


### Step 3: copy user's config files, if necessary


More practical example:

```yaml
---
# file: complex-playbook.yml

- hosts: all

  roles:
    - williamyeh.mongodb

  vars:
    mongodb_version: 3.0.4

    mongodb_mongod_conf: "templates/mongod.conf.j2"

```


## Dependencies

None.


## License

MIT License. See the [LICENSE file](LICENSE) for details.


## History

Rewritten from my pre-Galaxy version: [server-config-template](https://github.com/William-Yeh/server-config-template).
