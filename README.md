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

