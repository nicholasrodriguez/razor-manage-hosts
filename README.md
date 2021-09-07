# Ansible Role: Razor Manage Hosts

An Ansible Role that manages hosts in Puppet Razor on Linux. It provides the following interactive functionality:

* Add a host to Razor for provisioning
* Remove a host from Razor

## Razor Summary

Puppet Razor Server is an Open Source Operating System provisioning tool, details are here:

[https://github.com/puppetlabs/razor-server/wiki]

# Requirements

This Role was built and tested after the following Ansible Galaxy Roles were deployed but could be used for other Razor deployments, ensure the Tasks and Repos exist that the host is being configured with:

* nicholasrodriguez.razor
* nicholasrodriguez.razor_tasks_esxi
* nicholasrodriguez.razor_tasks_centos

The metadata being injected into the host being managed in Razor via this Role aligns with the following personal lab Repo:

[https://github.com/nicholasrodriguez/lab]

Hosts being managed in Razor need to be resolvable by the Ansible Controller, you can use the shortname or FQDN.

# Role Variables

The following vars are all defined per managed host instance. Example values are listed below.

Mode of operation:
```
add_or_delete: add
```

Short hostname of the host being managed in Razor:
```
hostname: lvm01
```

Razor Repo name:
```
repo: "CentOS-8.2-minimal"
```

Razor Task name:
```
task: "centos/8.2"
```

Razor Broker name:
```
broker: "noop"
```

Root password of the host being managed in Razor:
```
root_password: "Password123"
```

1st DNS Server
```
dns1: "1.1.1.1"
```

2nd DNS server
```
dns2": "1.0.0.1"
```

Time Server
```
time1: "ntp.pool.org"
```

Primary Interface IP address
```
ipaddress: "192.168.1.10"
```

Primary Interface Network gateway
```
gateway: "192.168.1.1"
```

Primary Interface Netmask
```
netmask: "255.255.255.0"
```

Primary Interface name:
```
mgmt_nic: "ens33"
```

Administration User name
```
user_name: "Bob"
```

Administration User Password
```
user_password: "Password123!"
```
# Dependencies

None.

# Example Playbook

This role is better suited to being interactive as per the prompts in the example below. The vars could be fed by other methods if preferred.

```
- name: Manage Razor Hosts
  connection: ssh
  gather_facts: true
  hosts: razor
  become: True
  roles:
    - razor_manage_hosts
  vars_prompt:
    - name: add_or_delete
      prompt: "Add or Delete a host in Razor [add/del]?"
      private: no
    - name: hostname
      prompt: "What is the hostname of the server?"
      private: no
```

# License

MIT

# Author Information

- https://github.com/nicholasrodriguez/ (maintainer)
