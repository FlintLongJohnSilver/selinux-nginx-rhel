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

```bash
$ ls -Z /usr/sbin/nginx
-rwxr-xr-x. root root system_u:object_r:nginx_exec_t:s0 /usr/sbin/nginx
```

Check the audit logs to see if nginx is being denied.

```bash
$ audit2why -al
```

> No output is good. If there are denials, modify the policy as necessary.

## Troubleshooting

### HTML Directories

if you have others directories for your html files you have to put the context **httpd_sys_content_t** in that directory. 
For example:

```bash
$ semanage fcontext -a -t httpd_sys_content_t "/home/www(/.*)?"
$ restorecon -R -v /home/www/
```

### Sockets

If you are working in nginx with sockets..

```bash
upstream test {
    server unix:/var/run/apps/test-file.sock fail_timeout=0;
}
```

then you have to do this:

```bash
$ semanage fcontext -a -t nginx_var_run_t "/var/run/apps(/.*)?"
$ restorecon -R -v /var/run/apps/
```