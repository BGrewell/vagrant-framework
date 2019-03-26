# vagrant-framework
Extension on traditional vagrant configuration to make it easier/faster to bring up any number of systems using just YAML configuration files.


## Single System Example

```
# config.d/system.yaml contents
---
name: system-1
enabled: yes
box: ubuntu/xenial64
memory: 1024
cpus: 1
...
```

## Multiple Systems in a Single File Exmaple
```
# config.d/systems.yaml contents
---
-
  name: system-1
  enabled: yes
  box: ubuntu/xenial64
  memory: 1024
  cpus: 1
-
  name: system-2
  enabled: no
  box: ubuntu/xenial64
  memory: 1024
  cpus: 1
-
  name: system-3
  enabled: yes
  box: ubuntu/xenial64
  memory: 1024
  cpus: 1
...
```

## Multiple Systems in Seperate Files Example
```
# config.d/system1.yaml contents
---
name: system-1
enabled: yes
box: ubuntu/xenial64
memory: 1024
cpus: 1
...


# config.d/system2.yaml contents
name: system-2
enabled: yes
box: ubuntu/xenial64
memory: 1024
cpus: 1
...
```
