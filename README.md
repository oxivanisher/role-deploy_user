deploy_user
===========

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
| deploy_user_ssh_keys_present | A list of SSH keys to be present for the deployment user | `[]`           |
| deploy_user_ssh_keys_absent  | A list of SSH keys to be absent for the deployment user  | `[]`           |

Example Playbook
----------------

```yaml
- name: SSH Keys
  hosts: servers
  roles:
    - role: oxivanisher.linux_base.ssh_keys
      tags:
        - basic_access
```

License
-------

BSD

Author Information
------------------

This role is part of the [oxivanisher.linux_base](https://galaxy.ansible.com/ui/repo/published/oxivanisher/linux_base/) collection, and the source for that is located on [github](https://github.com/oxivanisher/collection-linux_base).
