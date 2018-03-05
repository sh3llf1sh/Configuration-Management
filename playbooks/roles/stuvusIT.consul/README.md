# consul

This role sets up a simple Consul cluster on a group of Ansible hosts.
There is no ACL configuration or TLS configuration.

You need internet access on the control machine to download Consul.
Consul will be compiled on the control machine instead of the target machine.

**This playbook requires the `linear` strategy!**

## Requirements

An apt- or pacman-based Linux distribution on both the control machine and the targets.
The control machine can also use the yum package manager.
If another distribution is used, the packages for `git`, `go`, and `make` need to be installed on the control machine and `go` needs to be installed on the targets.

## Role Variables

| Name                    | Default/Required   | Description                                                              |
|-------------------------|:------------------:|--------------------------------------------------------------------------|
| `global_cache_dir`      | :heavy_check_mark: | Path where files are downloaded and Consul is built.                     |
| `consul_version`        | `0.7.5`            | Version of Consul to build and run.                                      |
| `consul_data`           | `/var/lib/consul`  | Path where Consul data will be stored.                                   |
| `consul_advertise_addr` |                    | Advertise this address in the cluster.                                   |
| `consul_bind_addr`      |                    | Bind to this address for clustering.                                     |
| `consul_client_addr`    | `127.0.0.1`        | Bind to this address for client requests.                                |
| `consul_group`          | :heavy_check_mark: | Ansible group containing all Consul hosts to cluster. See example below. |

# Example Playbook

```yml
- hosts: consul
  roles:
    - role: consul
      consul_client_addr: 0.0.0.0
      consul_group: "{{ groups['consul'] }}"
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Janne Heß](https://github.com/dasJ)
