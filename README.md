# ansible-docker-ce

Ansible playbook to deploy and configure docker-ce.

## Usage

See [defaults/main.yml](defaults/main.yml) to get the list of variables.

Sample `requirements.yml` :

```
- name: docker-ce
  src: git+https://github.com/mborne/ansible-docker-ce.git
  version: master
```

Sample playbook :

```yaml
---
- name: Install docker
  hosts: all
  become: yes
  become_method: sudo
  roles:
    - docker-ce
```

## Troubleshooting

For rasbperries, `aufs-dkms` should be removed to avoid problems :

```bash
sudo apt-get purge aufs-dkms
```

## License

[MIT](LICENSE)

