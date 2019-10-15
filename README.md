# ansible-docker

Docker installation and configuration.

## Usage

See [defaults/main.yml](defaults/main.yml) to get the list of variables.

Sample `requirements.yml` :

```
- name: docker-ce
  src: git+https://gogs.quadtreeworld.net/ansible/docker-ce.git
  version: v0.3.0
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
