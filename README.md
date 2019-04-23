# pmm-vagrant-demo
Simple pmm deployment demo

## Vagrant

Start VMs

```
vagrant up server
vargrant up mysql
```

## Configure mysql 

```
$ vagrant ssh mysql
$ sudo su -
# yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
# yum install Percona-Server-server-57
# grep password  /var/log/mysqld.log
# mysql
mysql> set password for root@localhost = PASSWORD('Mynewpass1!');
mysql> GRANT SELECT, PROCESS, SUPER, REPLICATION CLIENT, RELOAD ON *.* TO 'pmm'@' localhost' IDENTIFIED BY 'changeM3!' WITH MAX_USER_CONNECTIONS 10;
mysql> GRANT SELECT, UPDATE, DELETE, DROP ON performance_schema.* TO 'pmm'@'localhost';
# vim /etc/my.cnf # Add QAN config to [mysqld] section

#QAN
log_output='file'
log_slow_rate_type='query'
log_slow_rate_limit=100
long_query_time=0
log_slow_verbosity='full'
log_slow_admin_statements=ON
log_slow_slave_statements=ON
slow_query_log_use_global_control='all'
slow_query_log_always_write_time=1
slow_query_log=ON

# service mysql restart
```


## Ansible

Check inventory file and verify correct ssh settings.
Run playbook to deploy pmm server and client.

```
ansible-playbook -i inventory manage_pmm.yml
```
