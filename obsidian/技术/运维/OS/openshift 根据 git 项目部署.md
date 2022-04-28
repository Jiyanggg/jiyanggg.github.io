

```
oc delete all --selector app=ip-pool
```

```
oc new-app git@gitlab.zylliondata.local:idsg/ip-pool.git#dev -n idsg-edge
```