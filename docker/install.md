1. install

```
curl -sSL get.docker.com | bash
```

2. uninstall

```
sudo apt-get purge docker-ce docker-ce-cli containerd.io
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

3. configuare

```
# vim /etc/docker/daemon.json

{
    "ipv6": false,
    "log-level": "",
    "log-driver": "json-file",
    "log-opts": {
      "max-size": "20m",
      "max-file": "3"
    }
}
```

4. start

```
systemctl daemon-reload
systemctl restart docker
```

5. compose file

```
# nano docker-compose.yml

version: '3.8'

services:
  swag:
    container_name: swag
    image: lscr.io/linuxserver/swag:latest
    restart: unless-stopped
    ports:
      - 443:443
      - 80:80 #optional
    volumes:
      - /data/config:/config
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    # logging:
    #   driver: "none"  # close logging
    #   driver: "json-file"
    #   options:
    #     max-size: "100m"
    #     max-size: "3"

# networks:
#   default:
#     external: true
#     name: swag_proxy # docker network create swag_proxy
```

Ref

[https://docs.docker.com/reference/cli/dockerd/#daemon-configuration-file](https://)

