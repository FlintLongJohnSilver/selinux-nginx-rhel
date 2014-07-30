selinux-nginx-rhel
==================

SELinux Nginx policy for RHEL/CentOS.

Modified from http://sourceforge.net/projects/selinuxnginx/

> Tested on CentOS 6.5

## Installation

```bash
$ sudo yum install selinux-policy-devel selinux-policy-targeted
$ git clone https://github.com/jahrmando/selinux-nginx-rhel.git
$ cd selinux-nginx-rhel/nginx
$ make
$ semodule -i nginx.pp
```

Relabel the filesystem

```bash
$ touch /.autorelabel
$ reboot
```

Make sure nginx is running as **_nginx_exec_t_**

```
$ ls -Z /usr/sbin/nginx
-rwxr-xr-x. root root system_u:object_r:nginx_exec_t:s0 /usr/sbin/nginx
```

Check the audit logs to see if nginx is being denied.

```
$ audit2why -al
```

> No output is good. If there are denials, modify the policy as necessary.