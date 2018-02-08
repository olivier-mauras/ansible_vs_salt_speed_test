# Apply

### Ansible
``` text
# time ansible-playbook -i localhost desktop.yml 
 [WARNING]: Found both group and host with same name: localhost


PLAY [localhost] *******************************************************************************

TASK [Gathering Facts] *************************************************************************
ok: [localhost]

TASK [base : Update package database] **********************************************************
ok: [localhost]

TASK [base : Install base packages] ************************************************************
changed: [localhost] => (item=cronie)
changed: [localhost] => (item=rsyslog)
changed: [localhost] => (item=logrotate)
changed: [localhost] => (item=vim)
ok: [localhost] => (item=sudo)

TASK [base : Remove unneeded ttys] *************************************************************
changed: [localhost] => (item=3)
changed: [localhost] => (item=4)
changed: [localhost] => (item=5)
changed: [localhost] => (item=6)

TASK [base : Add default services] *************************************************************
changed: [localhost] => (item=cronie)
changed: [localhost] => (item=rsyslogd)

TASK [base : Deploy logrotate.conf] ************************************************************
changed: [localhost]

TASK [base : Deploy logrotate.d] ***************************************************************
changed: [localhost] => (item=/root/roles/base/files/logrotate.d/syslog)

TASK [base : Set custom sudoers.d config] ******************************************************
changed: [localhost] => (item=/root/roles/base/files/sudoers.d/users)

PLAY RECAP *************************************************************************************
localhost                  : ok=8    changed=6    unreachable=0    failed=0   


real	0m11.660s
user	0m8.520s
sys	0m1.804s
```

### Salt
``` text
# time salt-call --local state.apply
local:
----------
          ID: base.packages
    Function: pkg.installed
      Result: True
     Comment: 4 targeted packages were installed/updated.
              The following packages were already installed: sudo
     Started: 20:59:31.015288
    Duration: 1726.907 ms
     Changes:
              ----------
              cronie:
                  ----------
                  new:
                      1.5.1_1
                  old:
              jansson:
                  ----------
                  new:
                      2.10_1
                  old:
              libcurl:
                  ----------
                  new:
                      7.58.0_1
                  old:
              libestr:
                  ----------
                  new:
                      0.1.10_1
                  old:
              libfastjson:
                  ----------
                  new:
                      0.99.8_1
                  old:
              libgcrypt:
                  ----------
                  new:
                      1.8.2_1
                  old:
              libgpg-error:
                  ----------
                  new:
                      1.27_1
                  old:
              liblogging:
                  ----------
                  new:
                      1.0.6_1
                  old:
              logrotate:
                  ----------
                  new:
                      3.13.0_1
                  old:
              nghttp2:
                  ----------
                  new:
                      1.29.0_1
                  old:
              rsyslog:
                  ----------
                  new:
                      8.32.0_1
                  old:
              vim:
                  ----------
                  new:
                      8.0.1427_2
                  old:
              vim-common:
                  ----------
                  new:
                      8.0.1427_2
                  old:
              xxd:
                  ----------
                  new:
                      8.0.1427_2
                  old:
----------
          ID: base.services.removed.tty3
    Function: file.absent
        Name: /etc/runit/runsvdir/default/agetty-tty3
      Result: True
     Comment: Removed file /etc/runit/runsvdir/default/agetty-tty3
     Started: 20:59:32.749220
    Duration: 5.906 ms
     Changes:
              ----------
              removed:
                  /etc/runit/runsvdir/default/agetty-tty3
----------
          ID: base.services.removed.tty4
    Function: file.absent
        Name: /etc/runit/runsvdir/default/agetty-tty4
      Result: True
     Comment: Removed file /etc/runit/runsvdir/default/agetty-tty4
     Started: 20:59:32.755311
    Duration: 0.582 ms
     Changes:
              ----------
              removed:
                  /etc/runit/runsvdir/default/agetty-tty4
----------
          ID: base.services.removed.tty5
    Function: file.absent
        Name: /etc/runit/runsvdir/default/agetty-tty5
      Result: True
     Comment: Removed file /etc/runit/runsvdir/default/agetty-tty5
     Started: 20:59:32.756073
    Duration: 0.504 ms
     Changes:
              ----------
              removed:
                  /etc/runit/runsvdir/default/agetty-tty5
----------
          ID: base.services.removed.tty6
    Function: file.absent
        Name: /etc/runit/runsvdir/default/agetty-tty6
      Result: True
     Comment: Removed file /etc/runit/runsvdir/default/agetty-tty6
     Started: 20:59:32.756710
    Duration: 0.544 ms
     Changes:
              ----------
              removed:
                  /etc/runit/runsvdir/default/agetty-tty6
----------
          ID: base.services.enabled.cronie
    Function: file.symlink
        Name: /etc/runit/runsvdir/default/cronie
      Result: True
     Comment: Created new symlink /etc/runit/runsvdir/default/cronie -> /etc/sv/cronie
     Started: 20:59:32.757424
    Duration: 11.497 ms
     Changes:
              ----------
              new:
                  /etc/runit/runsvdir/default/cronie
----------
          ID: base.services.enabled.rsyslogd
    Function: file.symlink
        Name: /etc/runit/runsvdir/default/rsyslogd
      Result: True
     Comment: Created new symlink /etc/runit/runsvdir/default/rsyslogd -> /etc/sv/rsyslogd
     Started: 20:59:32.769098
    Duration: 1.639 ms
     Changes:
              ----------
              new:
                  /etc/runit/runsvdir/default/rsyslogd
----------
          ID: base.logrotate.logrotate.conf
    Function: file.managed
        Name: /etc/logrotate.conf
      Result: True
     Comment: File /etc/logrotate.conf updated
     Started: 20:59:32.770960
    Duration: 32.223 ms
     Changes:
              ----------
              diff:
                  ---
                  +++
                  @@ -1,25 +1,25 @@
                   # See logrotate(8) for details.
                   #
                  -# rotate log files weekly
                  -weekly
                  +# rotate log files daily
                  +daily

                  -# keep 4 weeks worth of backlogs
                  -rotate 4
                  +# keep 10 days worth of backlogs
                  +rotate 10

                   # restrict maximum size of log files
                  -size 512k
                  +#size 20M

                   # create new (empty) log files after rotating old ones
                   create
                  +
                  +# use date as a suffix of the rotated file
                  +dateext

                   # uncomment this if you want your log files compressed
                   compress

                   # Do not rotate logs if they are empty
                   notifempty
                  -
                  -# Do not send emails
                  -nomail

                   # Do not panic if log missing
                   missingok
                  @@ -29,8 +29,17 @@

                   include /etc/logrotate.d

                  +# no packages own wtmp and btmp -- we'll rotate them here
                   /var/log/wtmp {
                       monthly
                       create 0664 root utmp
                  +    minsize 1M
                       rotate 1
                   }
                  +
                  +/var/log/btmp {
                  +    missingok
                  +    monthly
                  +    create 0600 root utmp
                  +    rotate 1
                  +}
              mode:
                  0640
----------
          ID: base.logrotate.logrotate.d
    Function: file.recurse
        Name: /etc/logrotate.d
      Result: True
     Comment: Recursively updated /etc/logrotate.d
     Started: 20:59:32.803418
    Duration: 74.659 ms
     Changes:
              ----------
              /etc/logrotate.d/syslog:
                  ----------
                  diff:
                      New file
                  mode:
                      0640
----------
          ID: base.sudo.sudoers.d
    Function: file.recurse
        Name: /etc/sudoers.d
      Result: True
     Comment: Recursively updated /etc/sudoers.d
     Started: 20:59:32.882775
    Duration: 78.912 ms
     Changes:
              ----------
              /etc/sudoers.d/users:
                  ----------
                  diff:
                      New file
                  mode:
                      0440

Summary for local
-------------
Succeeded: 10 (changed=10)
Failed:     0
-------------
Total states run:     10
Total run time:    1.933 s

real	0m4.132s
user	0m3.165s
sys	0m0.603s
```
