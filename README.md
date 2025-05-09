deploy_user
===========
[![Ansible Lint](https://github.com/oxivanisher/role-deploy_user/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/oxivanisher/role-deploy_user/actions/workflows/ansible-lint.yml)

This role configures a deployment user to be used for ansible runs.

Notes
-----

* Please be aware, that you might have to run this role initially first interactively on a new target system before all your automation will work.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

| Name                         | Comment                                                  | Default value  |
|------------------------------|----------------------------------------------------------|----------------|
| deploy_user_username         | Username of the deployment user                          | `ansible`      |
| deploy_user_comment          | Comment for the deployment user                          | `Ansible User` |
| deploy_user_groupname        | Name of the deployment user group                        | `ansible`      |
| deploy_user_uid_min          | Min UID of hte deployment user                           | `900`          |
| deploy_user_uid_max          | Max UID of hte deployment user                           | `999`          |
| deploy_user_ssh_keys_present | A list of SSH keys to be present for the deployment user | `[]`           |
| deploy_user_ssh_keys_absent  | A list of SSH keys to be absent for the deployment user  | `[]`           |

## UID Notes
Since on most systems "normal" user accounts start at UID 1000, setting the `deploy_user_uid_max` to lower than 1000 will i.e. hide the deployment user on some GUI login screens automatically which is desired. But since remote login and a user home is still required for Ansible, making the user a `system` type user would not work. For this reason, the defaults will choose a UID between `900` and `999`. [This discussion on stackexchange](https://unix.stackexchange.com/questions/80277/whats-the-difference-between-a-normal-user-and-a-system-user) states, that [CIS](https://www.cisecurity.org/) treats every user below 1000 as systemuser and all those users are required to have `/sbin/nologin` as shell. 🤷 You might have to tweak the UIDs.
If you want the user to get a "normal" UID, just set `deploy_user_uid_min` to `1000` and `deploy_user_uid_max` to `10000` or so.

Example Playbook
----------------

```yaml
- name: Deploy ansible user
  hosts: servers
  roles:
    - role: oxivanisher.linux_base.deploy_user
      tags:
        - basic_access
```

License
-------

BSD

Author Information
------------------

This role is part of the [oxivanisher.linux_base](https://galaxy.ansible.com/ui/repo/published/oxivanisher/linux_base/) collection, and the source for that is located on [github](https://github.com/oxivanisher/collection-linux_base).
