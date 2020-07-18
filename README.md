Tutorial: https://blog.entrostat.com/routing-multiple-domains-using-haproxy-http-and-https-ssl/

Require

```
                                        +---------+
                                    +--> | aaa.com |
                                    |    +---------+
                                    |
                                    |    +---------+
                                    +--> | bbb.com |
+-----------+        +--------+     |    +---------+
| main host +------> | haproxy +----+
+-----------+        +--------+     |    +---------+
                                    +--> | ccc.com |
                                         +---------+
```

- Bind port 80 using `mode http`, but bind port 443 use `mode tcp` to avoid the need for certificates on 443 bind -> routing 443 to a host and I expect that host to have the certificate setup
- Need load balancing: add more servers in the `backend` entries like this: `server server3 server3:443`

HAProxy repo
https://github.com/haproxy/haproxy

HAProxy v2.2
http://www.haproxy.org/download/2.2/src/haproxy-2.2.0.tar.gz

Build HAProxy
```
# CentOS 7
yum install gcc openssl-devel readline-devel systemd-devel make pcre-devel

make clean 
make -j $(nproc) TARGET=linux-glibc \
    USE_OPENSSL=1 USE_ZLIB=1 USE_LUA=1 USE_PCRE=1 USE_SYSTEMD=1
```

