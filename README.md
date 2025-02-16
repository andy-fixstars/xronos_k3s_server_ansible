# Provision k3s server

Provision a host with k3s server.

This role performs the following steps:

- Disables existing k3s service (if any)
- Installs k3s from the official install script
- Configures `k3s-server` systemd service
- Installes kubenetes python module (used by Ansible)

This role is intended for use in prototyping and internal development projects. This role is not intended for production environments, or for any public-facing services.

## Requirements

Provisioning host:

- Ansible 2.15

Remote host:

- Ubuntu 22.04 or 24.04
- EWAOL
- docker or containerd
- git

## Example playbook

```yaml
- hosts: all
  roles:
    - name: xronos_k3s_server_ansible
      role: xronos_k3s_server_ansible
      vars:
        xronos_k3s_server_token: ""   # your secret token here
```

After running, the service `k3s-agent` should be running on the remote host.

## Variables

- `xronos_k3s_server_token`: secret token to use for authenticating k3s agent to the k3s control node. Required.
- `xronos_k3s_server_version`: version identifier of k3s to install. Defaults to empty (latest).
- `xronos_k3s_server_python_module_version`: version of the kubernetes python module to install. Defaults to empty (latest).
- `xronos_k3s_server_cluster_cidr`: Cluster CIDR. Defaults to `10.42.0.0/16`.
- `xronos_k3s_server_cluster_cidr`: Cluster service CIDR. Defaults to `10.43.0.0/16`.
