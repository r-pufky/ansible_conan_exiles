# Conan Exiles
Conan Exiles dedicated server.

## [Requirements][i]
Requires [r_pufky.game][g] galaxy-ng collection. See
[reference documentation][h] for troubleshooting and config variables.
Additional source documentation for [dedicated servers][l] and
[linux and wine][m] installs.

  Players | CPU           | Memory | Disk
 ---------|---------------|--------|------
  10      | 2c/2t @3.0Ghz | 8GB    | 6.5GB (excluding mods, DB growth)
  35      | 4c/4t @3.1Ghz | 8GB    | 6.5GB (excluding mods, DB growth)
  50      | 4c/8t @3.5Ghz | 12GB   | 6.5GB (excluding mods, DB growth)
  70      | 4c/8t @4.0Ghz | 12GB   | 6.5GB (excluding mods, DB growth)

> Tasks [potentially touching Network Mounted Filesystems][o] will be run as
> the task user and fallback to the service user. Manage these locations
> externally if these fail.

## Role Variables
Detailed variable use documented in defaults. See usage for role operation.

* [defaults][j] - User configurable options.

* [ports][k] - Ports are **not** managed (defined for external use).

## Usage

### Feature Flags
Tasks are gated by feature flags and executed in the following order.

  Step | Flag                    | Notes
 ------|-------------------------|-------
  1    | conan_exiles_flg_update | Update server on launch or if already installed.
  2    | conan_exiles_flg_config | Set configuration files.
  3    | conan_exiles_flg_backup | Enable local scheduled backup.

### Example Playbooks
**All** required server configuration files will be generated on start if they
do not exist. [Example configurations][n] have been included in the role:

* **templates/default** - vanilla server configuration deploy.
* **templates/siptah** - Isle of Siptah enabled with minimal configuration.

#### Default Server

``` yaml
- name: 'Vanilla server with daily backups enabled and mods auto configured.'
  ansible.builtin.include_role:
     name: 'r_pufky.game.conan_exiles'
  vars:
    conan_exiles_flg_backup: true
    conan_exiles_cfg_backup_mods: true
    conan_exiles_cfg_mods:
      - 2723987721
      - 1641464108
      - 1401061998
      - 1716717492
      - 864199675
      - 2869834350
      - 2859016366
```

#### Custom Server
Configuration files will be interpreted as templates, allowing for vault use of
server configuration files. Files in this directory will be sync'ed to the
server. See [examples in files][n].

``` yaml
- name: 'Deploy a Siptah server with custom game settings.'
  ansible.builtin.include_role:
     name: 'r_pufky.game.conan_exiles'
  vars:
    conan_exiles_cfg_d: 'host_vars/conan.example.com/config'
    conan_exiles_cfg_mods:
      - 2723987721
      - 1641464108
      - 1401061998
      - 1716717492
      - 864199675
      - 2869834350
      - 2859016366
```

## Development
Configure [environment][a].

``` bash
# Run all tests.
molecule test --all
```

Testing variables:

  Variable            | Type | Description
 ---------------------|------|-------------
  molecule_flg_inject | bool | Disable **get_url** to inject files locally.

### [Releases][b]

  Release | Debian | Ansible | Notes
 ---------|--------|---------|-------
  2.x.x   | 13     | 2.20    | Ansible 2.20, feature flags, and semantic versioning.
  1.x.x   | 12     | 2.11    | Migration from private repository.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License][c] | [direct link][f]

## Author Information
PGP: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9][d] | [github gist][e]

[a]: https://r-pufky.github.io/ansible_docs
[b]: https://semver.org/spec/v2.0.0
[c]: https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0
[d]: https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9
[e]: https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22

[f]: https://github.com/r-pufky/ansible_conan_exiles/blob/main/LICENSE
[g]: https://github.com/r-pufky/ansible_collection_game
[h]: https://r-pufky.github.io/docs/game/conan_exiles
[i]: https://github.com/r-pufky/ansible_conan_exiles/blob/main/meta/main.yml
[j]: https://github.com/r-pufky/ansible_conan_exiles/tree/main/defaults/main/main.yml
[k]: https://github.com/r-pufky/ansible_conan_exiles/blob/main/defaults/main/ports.yml
[l]: https://www.conanexiles.com/dedicated-servers/
[m]: https://conanexiles.fandom.com/wiki/Dedicated_Server_Setup:_Linux_and_Wine
[n]: https://github.com/r-pufky/ansible_conan_exiles/tree/main/files
[o]: https://r-pufky.github.io/ansible_docs/best_practice/patterns/#network-mounts