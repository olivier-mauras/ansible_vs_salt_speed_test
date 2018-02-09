Ansible VS Salt - Speed test
----------------------------
See `outputs.md` for complete outputs of commands.  

#### Table of Contents

* [Apply states](#apply-states)
  * [Ansible](#ansible)
  * [Salt](#salt)
* [Verify states](#verify-states)
  * [Ansible](#ansible-1)
  * [Salt](#salt-1)
* [Verify without package management](#verify-without-package-management)
  * [Ansible](#ansible-2)
  * [Salt](#salt-2)


## Apply states

### Ansible
``` text
# time ansible-playbook -i localhost desktop.yml 

real	0m11.660s
user	0m8.520s
sys	0m1.804s
```

### Salt
``` text
# time salt-call --local state.apply

real	0m4.132s
user	0m3.165s
sys	0m0.603s
```

## Verify states

### Ansible
``` text
# time ansible-playbook -i localhost desktop.yml 

real	0m10.386s
user	0m7.673s
sys	0m1.651s
```

### Salt
``` text
# time salt-call --local state.apply

real	0m2.509s
user	0m2.050s
sys	0m0.401s
```

## Verify without package management

### Ansible
``` text
# time ansible-playbook -i localhost desktop.yml

real	0m6.134s
user	0m4.727s
sys	0m1.213s
```

### Salt
``` text
# time salt-call --local state.apply

real	0m1.896s
user	0m1.519s
sys	0m0.326s
```
