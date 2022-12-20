## 1. enter MK container in shell, create a file (for ex /root/docker.sh) with following entries :

```
update-ca-certificates --fresh
openssl s_client -showcerts -verify 5 -connect ghcr.io:443 < /dev/null 2>/dev/null | openssl x509 -outform PEM | tee ~/ghcr.io.crt
cp ~/ghcr.io.crt /usr/local/share/ca-certificates/
update-ca-certificates
```

## 2. Execute it once, or add the execution safely along with docker start (/etc/init.d/docker)

```
...
case "$1" in
        start)
                # <add-following-line>
                /root/./docker.sh
                # </add-following-line>
                check_init
                fail_unless_root
                cgroupfs_mount
                ..
```
