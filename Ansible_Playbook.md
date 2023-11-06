#simple Ansible playbook that installs the Apache web server on a group of remote servers.
\\You can save this playbook in a YAML file, for example, "install_apache.yml".

---
- name: Install Apache Web Server
  hosts: webservers  # Replace 'webservers' with the appropriate group from your inventory

  tasks:
    - name: Update package cache
      become: yes
      apt:
        update_cache: yes  # Use 'yum' for CentOS/Red Hat systems

    - name: Install Apache
      become: yes
      apt:
        name: apache2
        state: present  # Use 'name: httpd' for CentOS/Red Hat systems

    - name: Start Apache Service
      become: yes
      service:
        name: apache2
        state: started  # Use 'name: httpd' for CentOS/Red Hat systems
        enabled: yes

    - name: Enable Apache to start at boot
      become: yes
      service:
        name: apache2
        enabled: yes  # Use 'name: httpd' for CentOS/Red Hat systems
=========================================================================
# Ansible playbook that performs tasks like copying a file, setting file permissions, and restarting a service on remote servers. 

---
- name: File Copy and Service Restart
  hosts: webservers  # Replace 'webservers' with your target host/group

  tasks:
    - name: Copy a configuration file
      copy:
        src: /local/path/to/config.conf
        dest: /remote/path/to/config.conf
        owner: user
        group: group
        mode: 0644

    - name: Ensure a directory exists
      file:
        path: /path/to/your/directory
        state: directory

    - name: Restart Apache service
      service:
        name: apache2  # Use 'name: httpd' for CentOS/Red Hat systems
        state: restarted
===============================================================================
# Download the artifact and unzip

---
- name: playbook to download the jarfile from jfrog and unarchive
  hosts: devops
  become: true
  user: ansible
  tasks:
    - name: create a folder
      file:
        path: /var/deploy
        state: directry
    - name: download the tar
      get_url:
        url: <url of zip file>
        dest: /var/tmp/
    - name: unzip
      command: unzip -o <your zip file>
