- Ansible Playbooks

```
---
- name: Test Connectivity
  hosts: all
  tasks:
   - name: Ping test
     ping:
```

- Ansible module “Copy”

```
---
- name: Copy for linux
  hosts: webservers
  tasks:
   - name: Copy your file to the webservers
     copy:
       src: /home/ec2-user/testfile1
       dest: /home/ec2-user/testfile1

- name: Copy for ubuntu
  hosts: ubuntuservers
  tasks:
   - name: Copy your file to the ubuntuservers
     copy:
       src: /home/ec2-user/testfile1
       dest: /home/ubuntu/testfile1
```


- Ansible module “Package” management

$ ansible-doc yum
$ ansible-doc apt

$ vim pb3.yml

```
---
- name: Apache installation for webservers
  hosts: webservers
  tasks:
   - name: install the latest version of Apache
     yum:
       name: httpd
       state: latest

   - name: start Apache
     shell: "service httpd start"

- name: Apache installation for ubuntuservers
  hosts: ubuntuservers
  tasks:
   - name: install the latest version of Apache
     apt:
       name: apache2
       state: latest
```

- Custom pages

vim pb5.yml

```
---
- name: Apache installation for ubuntuservers
  hosts: ubuntuservers
  tasks:
   - name: installing apache
     apt:
       name: apache2
       state: latest

   - name: index.html
     copy:
       content: "<h1>Hello Ansible</h1>"
       dest: /var/www/html/index.html

   - name: restart apache2
     service:
       name: apache2
       state: restarted
       enabled: yes

- name: Apache wget installation for webservers
  hosts: webservers
  tasks:
    - name: installing httpd and wget
      yum:
        pkg: ['httpd', 'wget']
        state: present
```

Remove Apache and wget from the hosts with pb6.yml.

```
vim pb6.yml

---
- name: Apache wget removal for webservers
  hosts: ubuntuservers
  tasks:
   - name: Uninstalling Apache
     apt:
       name: apache2
       state: absent
       update_cache: yes
   - name: Remove unwanted Apache2 packages
     apt:
       autoremove: yes
       purge: yes

- name: Apache wget removal for ubuntuserver
  hosts: webservers
  tasks:
   - name: removing apache and wget
     yum:
       pkg: ['httpd', 'wget']
       state: absent
```