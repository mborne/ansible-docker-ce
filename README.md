# ansible-docker-ce

## Role Summary

This ansible playbook allows to setup and configure docker-ce. It aims at providing a decent setup for a dev environment :

* Most daemon options are defaulted to fit [docker-bench-for-security](https://github.com/docker/docker-bench-security#docker-bench-for-security) recommendations (see [doc/dbs-uncovered.md](doc/dbs-uncovered.md) for exceptions)
* Log rotate is configured to avoid disk full

## Role Variables

See [defaults/main.yml](defaults/main.yml) to get the list of variables.

## Example Playbooks

Sample `requirements.yml` :

```
- name: mborne.docker_ce
  src: git+https://github.com/mborne/ansible-docker-ce.git
  version: master
```

Sample basic playbook :

```yaml
---
- name: Install docker
  hosts: all
  become: yes
  become_method: sudo
  roles:
    - mborne.docker_ce
```

Sample basic playbook with [userns-remap](https://docs.docker.com/engine/security/userns-remap/) and custom storage location :

```yaml
---
- name: Install docker
  hosts: all
  become: yes
  become_method: sudo
  roles:
    - mborne.docker_ce
  vars:
    docker_data_root: '/mnt/storage/docker'
    docker_userns_remap: 'default'
```

## Troubleshooting

For rasbperries, `aufs-dkms` should be removed to avoid problems :

```bash
sudo apt-get purge aufs-dkms
```

## See also

* [geerlingguy.docker](https://galaxy.ansible.com/geerlingguy/docker)

## License

[MIT](LICENSE)

