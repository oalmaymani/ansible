---
- name: Create users
  hosts: "*"
  tasks:
    - user:
        name: "{{ item }}"
        state: present
      loop:
        - user1
        - user2
        - user3
        - user4
      when: ansible_os_family == "RedHat"

    - user:
        name: "{{ item }}"
        state: present
      loop:
        - user1
        - user2
      when: ansible_os_family == "CentOS"

    - user:
        name: "{{ item }}"
        state: present
      loop:
        - user1
        - user2
      when: ansible_os_family == "Debian" or ansible_distribution_version == "20.04"
