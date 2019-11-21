# Openshift hostPath Playbook
Playbook for configure hostpath to cassandra and prometheus in Openshift.


- ###Files:

```
    ├── files
    │   └── hawkular-metrics-schema.yaml
    ├── hosts
    ├── playbook_hostpath.yaml
    ├── tasks
    │   ├── filesystem.yaml
    │   ├── mount.yaml
    │   ├── nodeselector.yaml
    │   ├── partition.yaml
    │   ├── policy.yaml
    │   └── volume.yaml
    └── vars
       └── vars.yaml
```



- ###Adjust the files below:

`vim ./hosts`

    [all:vars]
    ansible_become=true

    [servers:children]
    prometheus
    cassandra

    [prometheus]
    infra01.local
    infra02.local

    [cassandra]
    infra03.local



`vim ./vars/vars.yaml`

    ---
    openshift:
      - name: prometheus
        device: /dev/sdb
        server:
          - infra01.local
          - infra02.local
      - name: cassandra
        device: /dev/sdc
        server:
          - infra03.local


- ###Run:
`ansible-playbook -i hosts playbook_hostpath.yaml -e "app=prometheus"`
or
`ansible-playbook -i hosts playbook_hostpath.yaml -e "app=cassandra"`



- ### Before:
![](https://github.com/leoaaraujo/openshift-hostpath-playbook/blob/master/01.png?raw=true)

- ### After:
![](https://github.com/leoaaraujo/openshift-hostpath-playbook/blob/master/02.png?raw=true)

![](https://github.com/leoaaraujo/openshift-hostpath-playbook/blob/master/03.png?raw=true)

![](https://github.com/leoaaraujo/openshift-hostpath-playbook/blob/master/04.png?raw=true)
