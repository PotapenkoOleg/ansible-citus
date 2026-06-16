Docs available [here](https://learn.microsoft.com/en-us/postgresql/citus/multi-node-fedora-centos-rhel?view=citus-14)

Install in the following order:
1. **[install-etcd.yml](etcd/install-etcd.yml)** Skip this if reusing existing ETCD for Blue-Green deployment. Cluster name must be different eg constellation_v17 vs constellation_v18)
2. **[install-haproxy.yml](haproxy/install-haproxy.yml)** Skip this if reusing existing HAPROXY for Blue-Green deployment. Add Ports for new cluster instead. Change them to previous version ports to cwitch to new cluster)
3. **[install-postgres.yml](postgres/install-postgres.yml)** Change default port to avoid conflicts with previous version
4. **[install-patroni.yml](patroni/install-patroni.yml)** 