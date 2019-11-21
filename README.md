# openshift hostpath playbook
Playbook for configure hostpath to cassandra and prometheus in openshift.


- Adjust the files below:

```
hosts
```
> [all:vars]
> ansible_become=true
>
> [servers:children]
> prometheus
> cassandra
>
> [prometheus]
> infra01.local
> infra02.local
>
> [cassandra]
> infra03.local



```
vars/vars.yaml
```
