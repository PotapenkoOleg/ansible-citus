# Check if ETCD works

1. On **server 1**:
   - Run the following command:
     ```
     /opt/etcd/{{ ETCD_VERSION }}/etcdctl --endpoints=http://localhost:{{ ETCD_CLIENT_URLS_PORT }} member list
     ```
     This command should return the list of members in the ETCD cluster.
2. On **server 1**:
   - Run the following command:
     ```
     /opt/etcd/{{ ETCD_VERSION }}/etcdctl --endpoints=http://localhost:{{ ETCD_CLIENT_URLS_PORT }} put greeting "Hello, etcd"
     ```
     This command should return the list of members in the ETCD cluster.
3. On **server 2**:
   - Run the following command:
     ```
     /opt/etcd/{{ ETCD_VERSION }}/etcdctl --endpoints=http://localhost:{{ ETCD_CLIENT_URLS_PORT }} get greeting
     ```
     This command should return the value "Hello, etcd".
4. On **server 3**:
    - Run the following command:
      ```
      /opt/etcd/{{ ETCD_VERSION }}/etcdctl --endpoints=http://localhost:{{ ETCD_CLIENT_URLS_PORT }} get greeting
      ```
      This command should return the value "Hello, etcd".

   
**NOTE:** you can run commands above from **server 1**. Just replace `localhost` with the IP address of the server where you want to run the command.