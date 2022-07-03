# Networking with docker

With the following daemon config in `/etc/docker/daemon.json` :

```json
{
    "bip": "192.168.199.1/24",
    "fixed-cidr": "192.168.199.1/25",
    "default-address-pools" : [
        {"base" : "192.168.200.0/23","size" : 28}
    ]
}
```

* `bip` is the IP range for the default `bridge` :

```bash
docker network inspect bridge | jq '.[0].IPAM'
{
  "Driver": "default",
  "Options": null,
  "Config": [
    {
      "Subnet": "192.168.199.0/24",
      "IPRange": "192.168.199.0/25",
      "Gateway": "192.168.199.1"
    }
  ]
}
```

* `fixed-cidr` allows to reserve `192.168.199.[0-127]` for static IP allocation.

* `default-address-pools` provides allowed IP ranges for other networks with the following behavior :

```bash
docker network create net1
docker network create net2
docker network create net3
```

`docker network inspect net1 | jq '.[0].IPAM'` :

```json
{
  "Driver": "default",
  "Options": {},
  "Config": [
    {
      "Subnet": "192.168.200.0/28",
      "Gateway": "192.168.200.1"
    }
  ]
}
```

`docker network inspect net2 | jq '.[0].IPAM'` :

```json
{
  "Driver": "default",
  "Options": {},
  "Config": [
    {
      "Subnet": "192.168.200.16/28",
      "Gateway": "192.168.200.17"
    }
  ]
}
```

`docker network inspect net3 | jq '.[0].IPAM'` :

```json
{
  "Driver": "default",
  "Options": {},
  "Config": [
    {
      "Subnet": "192.168.200.32/28",
      "Gateway": "192.168.200.33"
    }
  ]
}
```

