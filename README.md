# halyard

[![Build Status](https://img.shields.io/travis/infOpen/ansible-role-halyard/master.svg?label=travis_master)](https://travis-ci.org/infOpen/ansible-role-halyard)
[![Build Status](https://img.shields.io/travis/infOpen/ansible-role-halyard/develop.svg?label=travis_develop)](https://travis-ci.org/infOpen/ansible-role-halyard)
[![Updates](https://pyup.io/repos/github/infOpen/ansible-role-halyard/shield.svg)](https://pyup.io/repos/github/infOpen/ansible-role-halyard/)
[![Python 3](https://pyup.io/repos/github/infOpen/ansible-role-halyard/python-3-shield.svg)](https://pyup.io/repos/github/infOpen/ansible-role-halyard/)
[![Ansible Role](https://img.shields.io/ansible/role/25377.svg)](https://galaxy.ansible.com/infOpen/halyard/)

Install halyard package.

## Requirements

This role requires Ansible 2.2 or higher,
and platform requirements are listed in the metadata file.

## Testing

This role use [Molecule](https://github.com/metacloud/molecule/) to run tests.

Local and Travis tests run tests on Docker by default.
See molecule documentation to use other backend.

Currently, tests are done on:
- Ubuntu Xenial

and use:
- Ansible 2.2.x
- Ansible 2.3.x
- Ansible 2.4.x
- Ansible 2.5.x

### Running tests

#### Using Docker driver

```
$ tox
```

## Role Variables

### Default role variables

``` yaml
# Dependencies management
halyard_system_dependencies: "{{ _halyard_system_dependencies }}"
halyard_use_system_dependencies: True  # Install system packages

# Dedicated user management
halyard_group:
  name: 'halyard'
halyard_user:
  name: 'halyard'
  home: '/var/lib/halyard'

# Paths
halyard_dirs:
  src:
    path: '/opt/halyard-git'

# General
halyard_version: '0.34.0'

# Git settings
halyard_git_repo_url: 'https://github.com/spinnaker/halyard.git'
halyard_git_version: "v{{ halyard_version }}"

# Install script
halyard_install_script: "{{ _halyard_install_script }}"
halyard_install_command_options: >
  --user {{ halyard_user.name }}
  --version {{ halyard_version }}
  -y
halyard_install_term: 'vt100'  # Ensure a TERM is defined due to tput usage
```

## Dependencies

`curl`, `git` and `openjdk-8-jre` are required:

- Setting `halyard_use_system_dependencies` to `True`(default) will install them.
- Ansible roles can also be used.

## Example Playbook

``` yaml
- hosts: servers
  roles:
    # System dependencies - only required if `halyard_use_system_dependencies` is set to `False`
    - { role: infOpen.curl }
    - { role: infOpen.git }
    - { role: infOpen.openjdk-jre }
    # Halyard role
    - { role: infOpen.halyard }
```

## License

MIT

## Author Information

Alexandre Chaussier (for Infopen company)
- http://www.infopen.pro
- a.chaussier [at] infopen.pro
