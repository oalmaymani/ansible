```sh
ansible-galaxy init /home/ec2-user/roles/apache
```

- Create tasks/main.yml with the following.

```yaml
- name: installing apache
  yum:
    name: httpd
    state: latest

- name: index.html
  copy:
    content: "<h1>Hello DevOps from ansible role</h1>"
    dest: /var/www/html/index.html

- name: restart apache2
  service:
    name: httpd
    state: restarted
    enabled: yes
```

- Create a playbook named "role1.yml".

```yaml
cd /home/ec2-user/working-with-roles/
vi role1.yml
```

```yaml
---
- name: Install and Start apache
  hosts: node1
  become: yes
  roles:
    - apache
```

- Run the command below

```yaml
ansible-playbook role1.yml
```