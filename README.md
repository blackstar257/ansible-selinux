# Ansible Role: SELinux

[![CI](https://github.com/blackstar257/ansible-selinux/workflows/CI/badge.svg)](https://github.com/blackstar257/ansible-selinux/actions?query=workflow%3ACI)
[![Ansible Role](https://img.shields.io/badge/role-blackstar257.selinux-blue.svg)](https://galaxy.ansible.com/blackstar257/selinux/)
[![Ansible Galaxy Downloads](https://img.shields.io/ansible/role/d/blackstar257/selinux.svg)](https://galaxy.ansible.com/blackstar257/selinux/)

An Ansible role that configures SELinux on RHEL/CentOS/Rocky Linux/AlmaLinux systems.

## Requirements

- Ansible 2.10 or higher
- Target systems must support SELinux (RHEL/CentOS/Rocky/Alma Linux 7, 8, 9)
- `ansible.posix` collection (for the `selinux` module)

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Variable | Default | Description |
|----------|---------|-------------|
| `selinux_policy` | `targeted` | SELinux policy type (`targeted`, `minimum`, `mls`) |
| `selinux_state` | `permissive` | SELinux state (`enforcing`, `permissive`, `disabled`) |
| `selinux_relabel` | `true` | Whether to create `.autorelabel` file for filesystem relabeling on boot |
| `selinux_reboot_required` | `false` | Whether to allow automatic reboots when required for SELinux changes |

### SELinux States

- **enforcing**: SELinux policy is enforced
- **permissive**: SELinux prints warnings instead of enforcing
- **disabled**: SELinux is completely disabled

### SELinux Policies

- **targeted**: Default policy that targets specific processes
- **minimum**: Minimal policy for containers and minimal systems
- **mls**: Multi-Level Security policy for high-security environments

## Dependencies

- `ansible.posix` collection

Install with:
```bash
ansible-galaxy collection install ansible.posix
```

## Example Playbook

### Basic usage (permissive mode)
```yaml
- hosts: all
  become: true
  roles:
    - blackstar257.selinux
```

### Enforce SELinux
```yaml
- hosts: all
  become: true
  vars:
    selinux_state: enforcing
  roles:
    - blackstar257.selinux
```

### Disable SELinux
```yaml
- hosts: all
  become: true
  vars:
    selinux_state: disabled
  roles:
    - blackstar257.selinux
```

### Use MLS policy in enforcing mode
```yaml
- hosts: all
  become: true
  vars:
    selinux_policy: mls
    selinux_state: enforcing
  roles:
    - blackstar257.selinux
```

### Advanced configuration
```yaml
- hosts: all
  become: true
  vars:
    selinux_policy: targeted
    selinux_state: enforcing
    selinux_relabel: true
    selinux_reboot_required: true  # Allow automatic reboot if needed
  roles:
    - blackstar257.selinux
```

## Supported Platforms

- RHEL/CentOS 7
- RHEL/CentOS 8
- RHEL/Rocky Linux/AlmaLinux 9
- Fedora 37+

## Testing

This role is tested using [Molecule](https://molecule.readthedocs.io/) with Docker.

```bash
# Install dependencies
pip install molecule molecule-plugins[docker] docker

# Run tests
molecule test
```

## Important Notes

- **Reboot Requirements**: Changes to SELinux state may require a system reboot to take effect
- **Filesystem Relabeling**: When enabling SELinux or changing policies, filesystem relabeling may be required
- **Performance Impact**: Initial filesystem relabeling can take significant time on large filesystems
- **Security Implications**: Disabling SELinux reduces system security

## License

MIT

## Author Information

This role was originally created by Kevin Brebanov and is now maintained by blackstar257.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests: `molecule test`
5. Submit a pull request

## Changelog

### v2.0.0
- Updated to support Ansible 2.10+
- Added support for Rocky Linux and AlmaLinux
- Migrated from Travis CI to GitHub Actions
- Modernized molecule testing
- Added support for RHEL/CentOS 8 and 9
- Improved error handling and idempotency
- Added comprehensive testing and verification
