# adhoc

gather facts for the hosts
```shell
ansible all -m setup
```

reboot the hosts in the `atlanta` group. We didn't specify a module because `command` is the default one.
```shell
ansible atlanta -a "/sbin/reboot"
```

print the memory usage
```shell
ansible all -a "free -m"
```

check the reachability of the hosts
```shell
ansible all -m ping
```

copy local file on the control node to the hosts in the `atlanta` group 
```shell
ansible atlanta -m copy -a "src=/etc/hosts dest=/tmp/hosts"
```

same as above but also with additional options
```shell
ansible atlanta -m copy -a "src=/etc/hosts dest=/tmp/hosts mode=600 owner=mdehaan group=mdehaan"
```

install `nginx` package to the hosts in the `webservers` group
```shell
ansible webservers -m apt -a "name=nginx state=present"
```

same as above but with a specific version
```shell
ansible webservers -m apt -a "name=nginx=1.18.0 state=present"
```

make sure `nginx` service is started
```shell
ansible webservers -m service -a "name=nginx state=started"
```