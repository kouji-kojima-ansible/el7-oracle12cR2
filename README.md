# EC2 CentOS7, RHEL7 に Oracle 12c R2 を インストールするロール (Role of setting Oracle 12c R2)


Install role
------------

```
ansible-galaxy install kouji-kojima-ansible.el7-oracle12cR2 --force
```


Dependencies
------------

kouji-kojima-ansible.el7-desktop


Process details
---------------




Example site.yml
----------------

```
cat << EOF > site.yml
- hosts: servers
  remote_user: ec2-user
  become: yes
  vars:
    proxy_host: proxy.xxxxxxxxx.co.jp
    proxy_port: port_no
    no_proxys: xxxxx.co.jp,yyyy.co.jp
    ca_url: https://xxxxxxxx.co.jp/xxx.ca(*1)
    ca_sha256: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    swap_file_path: path
  roles:
    - { role: kouji-kojima-ansible.el7-oracle12cR2 }
EOF
```


Example Hosts
-------------

```
# localhostの場合(In case of localhost)
cat << EOF > localhost
[servers]
localhost ansible_connection=local
EOF

# ステージング環境の場合(In case of staging environment)
cat << EOF > staging
[servers]
HostName or IP
HostName or IP

[all:vars]
ansible_ssh_user=ec2-user
EOF
```


Execute Playbook
-----------------

実行例(Normal execution)

```
# ローカルの場合(In case of localhost)
ansible-playbook -i localhost site.yml --private-key=/path/key.pem

# ステージング環境の場合(In case of staging environment)
ansible-playbook -i staging site.yml --private-key=/path/key.pem
```


License
-------

[Apache License Version 2.0](https://github.com/kouji-kojima-ansible/el7-oracle12cR2/blob/master/LICENSE)


Author Information
------------------

Kouji Kojima
