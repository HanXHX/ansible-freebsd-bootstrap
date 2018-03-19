Ansible FreeBSD bootstrap role
==============================

[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-HanXHX.freebsd--bootstrap-blue.svg)](https://galaxy.ansible.com/HanXHX/freebsd-bootstrap) [![Build Status](https://travis-ci.org/HanXHX/ansible-freebsd-bootstrap.svg?branch=master)](https://travis-ci.org/HanXHX/ansible-freebsd-bootstrap)

This role bootstraps FreeBSD server:

- Install and configure ports
- Install minimal packages (vim, htop...)
- Install CPU microcode if needed
- Install and configure NTP daemon [NTP](http://support.ntp.org/)
- Add groups, users with SSH key, sudoers
- Deploy bashrc, vimrc for root
- Configure system: hostname and timezone
- Sysctl tuning

Supported versions

| OS         | Working | Stable (active support) |
| -----------| ------- | ----------------------- |
| FreeBSD 11 | Yes     | Yes                     |
| FreeBSD 12 | Yes     | Yes                     |

Need the same role Debian? [Check this!](https://github.com/HanXHX/ansible-debian-bootstrap)

Requirements
------------

None.

Role Variables
--------------

### Role setup

- `fbs_set_hostname`: if true, change hostname
- `fbs_clean_hosts`: if true, manages `/etc/hosts` file
- `fbs_set_locale`: if true, configure locales
- `fbs_set_timezone`: if true, set timezone
- `fbs_set_ntp`: if true, install and configure OpenNTPd
- `fbs_set_apt`: if true, configure APT repository

### System configuration

- `fbs_hostname`: system hostname
- `fbs_default_locale`: default system locale
- `fbs_locales`: list of installed locales
- `fbs_timezone`: system timezone. If you need a "standard" timezone like UTC, you must use prefix "Etc/" (ex: "Etc/UTC")
- `fbs_sysctl_config`: hash of kernel parameters, see: [default/main.yml](default/main.yml)
- `fbs_use_systemd`: delete systemd if set to false (persistent)
- `fbs_use_dotfiles`: overwrite root dotfiles (bashrc, screenrc, vimrc)

### NTPd

- `fbs_ntp_hosts`: hostnames NTP server list

### Group

- `fbs_groups`: list of group

Each row have few keys:

- `name`: (M) username on system
- `system`: (O) yes/no (default: no)
- `state`: (O) present/absent (default: present)

(M) Mandatory
(O) Optionnal

### User

- `fbs_users`: list of user

Each row have few keys:

- `name`: (M) username on system
- `password`: (O) password with hash format (see [ansible doc](http://docs.ansible.com/ansible/latest/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module))
- `clear_password`: (O) password as clear format (not recommanded)
- `update_password`: (O) always / on\_create
- `shell`: (O) default is /bin/bash
- `comment`: (O) default is an empty string
- `sudo`: (O) boolean (true = can sudo)
- `group`: (O) main group (default is `name` without password)
- `groups`: (O) comma separated list of groups
- `createhome`: (O) yes/no
- `system`: (O) yes/no (default: no)
- `ssh_keys`: (O) ssh public keys list
- `state`: (O) present/absent (default: present)

(M) Mandatory
(O) Optionnal

Notes:

- if `password` is specified, `clear_password` is not used!
- `clear_password` is not idempotent with `update_password` = always (default)

For more information, look [ansible user module doc](http://docs.ansible.com/ansible/latest/user_module.html).

Dependencies
------------

None.

Example Playbook
----------------

See [tests/test.yml](tests/test.yml).

License
-------

GPLv2


Donation
--------

If this code helped you, or if you’ve used them for your projects, feel free to buy me some :beers:

- Bitcoin: `1BQwhBeszzWbUTyK4aUyq3SRg7rBSHcEQn`
- Ethereum: `63abe6b2648fd892816d87a31e3d9d4365a737b5`
- Litecoin: `LeNDw34zQLX84VvhCGADNvHMEgb5QyFXyD`
- Monero: `45wbf7VdQAZS5EWUrPhen7Wo4hy7Pa7c7ZBdaWQSRowtd3CZ5vpVw5nTPphTuqVQrnYZC72FXDYyfP31uJmfSQ6qRXFy3bQ`

No crypto-currency? :star: the project is also a way of saying thank you! :sunglasses:

Author Information
------------------

- Twitter: [@hanxhx_](https://twitter.com/hanxhx_)
