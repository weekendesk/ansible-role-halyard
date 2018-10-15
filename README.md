# halyard

Install halyard package.

## Requirements

This role requires Ansible 2.2 or higher,
and platform requirements are listed in the metadata file.

## Role Variables

### Default role variables

``` yaml
# Dependencies management
halyard_use_system_dependencies: True  # Install system packages

# Dedicated user management
halyard_group:
  name: 'halyard'
halyard_user:
  name: 'halyard'
  home: '/var/lib/halyard'

# Paths
halyard_git_dir: '/tmp/halyard-git'

# General
halyard_version: '1.6.0'

# Git settings
halyard_git_repo_url: 'https://github.com/spinnaker/halyard.git'
halyard_git_version: "version-{{ halyard_version }}"

# Install script
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

Weekendesk (https://github.com/weekendesk)

Alexandre Chaussier (for Infopen company)
- http://www.infopen.pro
- a.chaussier [at] infopen.pro
