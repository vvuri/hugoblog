---
categories: ["Linux"]
tags: ["DevOps","Linux","Ansible"]
description: ""
menu: 
    main:
        parent: "DevOps"
date: "2019-01-23"
title: "Первые шаги с Ansible"
---

#### Install
```bash
$ sudo apt-get install python-pip python-yaml python-jinja2 python-paramiko -y
$ sudo pip install ansible
	
$ python --version
	Python 2.7.3
$ ansible --version
	ansible 2.1.1.0
```

Отработка скрипта пишет в: 
``` 
$ sudo less -f /var/log/syslog	
```

Прямой вызов команд:
```bash
$ ansible localhost -m command -a "python --version"
$ ansible localhost -m shell -a "ps -axf | grep firefox"
$ ansible localhost -m shell -a "ps -eo pcpu,user,args | sort -r -k1 | head -n5"
$ ansible host-file-with-ip -m ping
```    

Документация: 
```bash
$ ansible-doc service  
```

Готовые решение [на galaxy](https://galaxy.ansible.com)

Playbook - каждый файл доржен содержать:
- множество hosts
- список tasks

[пример из книги](https://ipfs.io/ipfs/QmTJaLdhUW6jTdXGFoqv7wZe5KguBi5F2u4ihBdrUMVPhw)
```yaml
name: Configure webserver with nginx
hosts: webservers
sudo: True
tasks:
    - name: install nginx
        apt: name=nginx update_cache=yes
    - name: copy nginx config file
        copy: src=files/nginx.conf dest=/etc/nginx/sites-available/default
    - name: enable configuration
        file: >
            dest=/etc/nginx/sites-enabled/default
            src=/etc/nginx/sites-available/default
            state=link
    - name: copy index.html
        template: src=templates/index.html.j2
                dest=/usr/share/nginx/html/index.html mode=0644
    - name: restart nginx
        service: name=nginx state=restarted
```
Разбор:
```
name - комментраий что будет сделано далее, будет напечатано при выполнении
sudo - выполнять ли по рутом
vars - список переменных
tasks - конкретные выполняемые операции - выше их 5:
    name - рекомендуемый для заполнения комментарий, а так же метка для --start-at-task <task name>
    Каждая задача содержит: имя модюля - apt например, и аргумент name=nginx update_cache=yes
    старый вариант синтаксиса:
        - name: install nginx
            action: apt name=nginx update_cache=yes

    apt      - Installs or removes packages using the apt package manager.
    copy     - Copies a file from local machine to the hosts.
    file     - Sets the attribute of a file, symlink, or directory.
    service  - Starts, stops, or restarts a service	  
    template - Generates a file from a template and copies it to the hosts.

    # ansible-playbook -c xxx -i xxx 
    -i host -по умолчанию хосты лежат в /etc/ansible/hosts
```
[Документация по всем модулям](http://docs.ansible.com/ansible/modules_by_category.html)
```bash
$ ansible-doc -l | grep yum
$ ansible-doc yum_repository
```
Консоль 
```bash
root@all (0)[f:5]$ 
   $ ansible-console
```

#### Пример шаг за шагом:
>
```
 site.yml – starting point of our ansible playbook 
 # - name: install and configure webservers 
 # hosts: webservers ```
 # remote_user: ec2-user
 # sudo: yes
 # roles:
 #    - webservers
```

> hosts – carrying hosts information
```
 # [webservers]
 # 10.0.0.156
```    

> roles/ - defining what each type of server has to perform
> webservers/
>> tasks/ - tasks performed on webservers
>>> main.yml
```     
  # This task installs and enables apache on webservers
  # - name: ensure apache is installed
  #   yum: pkg=httpd state=latest
  # - name: ensure apache is running
  #   service: name=httpd state=running enabled=yes
  # - name: copy files to document root
  #   copy: src=cloud.png dest=/var/www/html/cloud.png
  # - name: copy application code to document root
  #   template: src=index.html.j2 dest=/var/www/html/index.html
  #   notify: restart apache			                     
```
> handlers/ - running tasks under particular events
>> main.yml
``` 
  # # This task installs and enables apache on webservers
  # - name: ensure apache is installed
  #   yum: pkg=httpd state=latest
  # - name: ensure apache is running
  #   service: name=httpd state=running enabled=yes
  # - name: copy files to document root
  #   copy: src=cloud.png dest=/var/www/html/cloud.png
  # - name: copy application code to document root
  #   template: src=index.html.j2 dest=/var/www/html/index.html
  #    notify: restart apache			                 
```
> templates/ - configuration files which can reference variables
>> index.html.j2
```
  # <head>
  #     <title>CloudAcademy Ansible Demo</title>
  # </head>
  # <body>
  #     <h1>
  #         Thank you for reading this post. 
  #         My IP Address is {{ ansible_eth0.ipv4.address }}
  #     </h1>
  #     <br/><br/><br/>
  #     <p>
  #         <img src="cloud.png" alt="CloudAcademy Logo"/>
  #     </p>
  # </body>
  # </html>
```
> files/ - files to be copied to webservers
>> cloud.png
```
>>> # image put on server
```

```
# ansible-playbook site.yml -i hosts  
```


