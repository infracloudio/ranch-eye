# Ranch-Eye

## Modification Summary:

Added ability to add the IP of Cadvisor dynamically - specially useful where host networking is not available

## Summary

Simple haproxy (1.6) implementation for exposing rancher's implementation of cadvisor stats to an external endpoint.
Useful for tools such as prometheus to monitor rancher managed hosts.

## Description

This container is designed to run on each of your rancher managed hosts, it forwards requests recieved on port 9104 to port 9344 on the internal loopback address..
Below and included, is a docker compose file to run this up in your environment, they key thing to consider running this is that it requires the container to be running in `HOST` networking mode.

```
ranch-eye:
  ports:
  - 9104:9104/tcp
  labels:
    io.rancher.scheduler.global: 'true'
    io.rancher.container.hostname_override: container_name
  tty: true
  image: rucknar/ranch-eye:latest
  stdin_open: true
  net: host
```

## Further Info

The ranch-eye container can be found on the docker hub [here](https://hub.docker.com/r/infinityworks/ranch-eye/)
The catalog entry is in the community catalog, available [here](https://github.com/rancher/community-catalog)
Additional information can be found on the [guide](https://github.com/infinityworksltd/Guide_Rancher_Monitoring)
