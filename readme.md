# K3s Ansible Automation

This project provides an Ansible-based automation for deploying and configuring a K3s (Lightweight Kubernetes) cluster. It supports multi-node clusters with dedicated server and agent roles, and configures necessary firewall rules and system services for a secure and functional Kubernetes environment.

## Features

- Automated installation of K3s on server and agent nodes
- Dynamic retrieval and distribution of cluster join tokens
- Firewall configuration using firewalld for required Kubernetes ports and CIDRs
- Systemd service management for K3s and firewalld
- Customizable via group and host variables

## Project Structure

```
k3s/
├── inventory/
│   ├── hosts
│   └── group_vars/
│       ├── all.yml
│       ├── mainserver.yml
│       ├── servers.yml
│       └── agents.yml
├── roles/
│   └── k3s/
│       ├── defaults/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       ├── meta/
│       │   └── main.yml
│       ├── tasks/
│       │   └── main.yml
│       ├── templates/
│       │   ├── k3s.server.service.j2
│       │   └── k3s.agent.service.j2
│       ├── tests/
│       │   ├── inventory
│       │   └── test.yml
│       └── vars/
│           └── main.yml
├── playbook.yml
└── readme.md
```

## Usage

1. **Configure Inventory**

   Edit `inventory/hosts` to define your server and agent nodes. Adjust SSH connection variables as needed.

2. **Set Group Variables**

   Customize `inventory/group_vars/*.yml` for ports, K3s arguments, and other settings.

3. **Run the Playbook**

   ```sh
   ansible-playbook -i inventory/hosts playbook.yml
   ```

   The playbook will:
   - Set up the main server node, initialize the cluster, and retrieve the join token.
   - Configure additional server and agent nodes to join the cluster using the token and server IP.

## Requirements

- Ansible 2.9+
- SSH access to all nodes
- Sudo privileges on target machines

## Customization

- Modify `roles/k3s/templates/` for custom systemd service files.
- Adjust firewall rules and K3s arguments in `group_vars` as needed.

## License

MIT-0

## Author

[InSearchOfName](https://github.com/InSearchOfName)
