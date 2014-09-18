ansible-module-loadbalanced
===========================

Ansible module for enabling/disabling a node in a haproxy backend using socat and the socket api

**TODO:** Add tests using
[docker_pull](https://github.com/modcloth-labs/ansible-module-docker-pull)
as an example.

Example playbook usage:

```yaml
---
- hosts: '{{ server }}'
  gather_facts: true
  user: '{{ ssh_user }}'
  serial: '{{ serial | default(0) }}'
  sudo: true
  vars:
    - loadbalanced_service_lb: "{{ recs_loadbalanced_service_lb }}"
    - loadbalanced_remote_user: "{{ ssh_user | default('ubuntu') }}"
  pre_tasks:
    - name: disable
      loadbalanced:
        action: disable
        server: "{{ hostname | default(ansible_fqdn) }}"
      delegate_to: "{{ loadbalanced_service_lb }}"
      remote_user: "{{ loadbalanced_remote_user }}"
  roles:
    # roles...
  tasks:
    # tasks...
  post_tasks:
    - name: enable
      loadbalanced:
        action: enable
        server: "{{ hostname | default(ansible_fqdn) }}"
      delegate_to: "{{ loadbalanced_service_lb }}"
      remote_user: "{{ loadbalanced_remote_user }}"
```
