# Conan Exiles
Conan Exiles dedicated server.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_conan_exiles/blob/main/meta/main.yml)

Players | CPU           | Memory | Disk
--------|---------------|--------|----------------------------------
10      | 2c/2t @3.0Ghz | 8GB    | 6.5GB (excluding mods, DB growth)
35      | 4c/4t @3.1Ghz | 8GB    | 6.5GB (excluding mods, DB growth)
50      | 4c/8t @3.5Ghz | 12GB   | 6.5GB (excluding mods, DB growth)
70      | 4c/8t @4.0Ghz | 12GB   | 6.5GB (excluding mods, DB growth)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_conan_exiles/tree/main/defaults/main)

### Ports
All ports and protocols have been defined for the role.

[defaults/ports.yml](https://github.com/r-pufky/ansible_conan_exiles/blob/main/defaults/main/ports.yml)

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.game](https://github.com/r-pufky/ansible_collection_game) collection.

## Example Playbook
Read defaults documentation.

The following example will get an instance quickly up and running, with the
specified mods automatically downloaded and installed in order. Server will
be created using the steamcmd user from `r_pufky.game.steam`.
``` yaml
- name: 'Conan Exiles server'
  hosts: 'conan.example.com'
  become: true
  roles:
     - 'r_pufky.game.conan_exiles'
  vars:
    conan_exiles_srv_backup_enable: true
    conan_exiles_cfg_mods_list:
      - 2723987721
      - 1641464108
      - 1401061998
      - 1716717492
      - 864199675
      - 2869834350
      - 2859016366
```

Changes updating the configuration only can be done to speed role application:
``` bash
ansible-playbook site.yml --tags conan \
  -e '{"conan_exiles_srv_update_server": false}'
```

Changes updating the server/mods only can be done to speed role application:
``` bash
ansible-playbook site.yml --tags conan \
  -e '{"conan_exiles_srv_update_settings": false}'
```

## Development
Configure [environment](https://github.com/r-pufky/ansible_collection_docs/blob/main/ansible/environment.md)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Release format: **{OS}-{SERVICE}-{ROLE}**

Each type inherits the versioning system used; defaulting to schematic
versioning.

`12.0.0-2.0.3-1.0.0`

* 12.0.0 - Debian 12 (bookworm).
* 2.0.3 - Service/app version.
* 1.0.0 - Role version.

Releases are branched on Debian releases:

* **[13.x.x](https://github.com/r-pufky/ansible_conan_exiles)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_conan_exiles/tree/12.x)**: 12 Bookworm.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_conan_exiles/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
