# Ansible Role: Selinux

[![Ansible Role](https://img.shields.io/badge/role-blackstar257.selinux-blue.svg)](https://galaxy.ansible.com/blackstar257/selinux/)
[![Build Status](https://travis-ci.org/blackstar257/ansible-selinux.svg?branch=master)](https://travis-ci.org/blackstar257/ansible-selinux)

Configures SELinux.

## Requirements

This role requires Ansible 1.4 or higher.

## Role Variables

| Name            | Default    | Description                                       |
| --------------- | ---------- | ------------------------------------------------- |
| selinux_policy  | targeted   | SELinux policy type (targeted or mls)             |
| selinux_state   | permissive | SELinux state (permissive, enforcing or disabled) |
| selinux_relabel | true       | Auto relabel files upon boot if enabled           |

## Dependencies

None

## Example Playbook

Configure SELinux in permissive mode.

```yaml
- hosts: all
  roles:
    - blackstar257.selinux
```

Disable SELinux

```yaml
- hosts: all
  roles:
    - { role: blackstar257.selinux, selinux_state: disabled }
```

Configure SELinux to use mls policy and enforcing mode

```yaml
- hosts: all
  vars:
    selinux_policy: mls
    selinux_state: enforcing
  roles:
    - blackstar257.selinux
```

## License

BSD

## Author Information

Original Owner Kevin Brebanov
Forked by blackstar257
