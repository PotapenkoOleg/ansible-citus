## Installing RPM from official source

Use system-provided packages or install latest RPM from an official source

https://github.com/haproxy/wiki/wiki/Packages
https://www.haproxy.com/downloads

## Blue/Green Deployment

Please check **[sample-blue-green.cfg](sample-blue-green.cfg)** for multi-cluster config 

To switch clusters we need switch ports in the following blocks:
* line **02**: 5000 -> **5100**
* line **06**: 5001 -> **5101**
* line **10**: 5100 -> **5000**
* line **14**: 5101 -> **5001**

```
01 frontend ft_postgresql_17
02 bind    *:5000 # TODO: <-
03 default_backend bk_postgres_17
04 
05 frontend ft_postgresql_readonly_17
06 bind    *:5001 # TODO: <-
07 default_backend bk_postgres_readonly_17
08
09 frontend ft_postgresql_18
10 bind    *:5100 # TODO: <-
11 default_backend bk_postgres_18
12
13 frontend ft_postgresql_readonly_18
14 bind    *:5101 # TODO: <-
15 default_backend bk_postgres_readonly_18
```

Switch back to allow apps connect to old cluster 

## Update config without restarting HAProxy 
* systemd `sudo systemctl reload haproxy`
* docker `docker kill -s HUP <container_name_or_id>`
