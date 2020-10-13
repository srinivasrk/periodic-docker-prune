## The problem
When running docker, periodicaly updating service images, each worker node starts to hold stale versions of old images, taking disk space.

Common solution is to run `docker prune` via cron, but we do not want to configure our workers besides joining to the swarm, aren't we?

So this image is designed for running periodic system clean with zero host configuration.

## Docker comose

```yaml
version: '3.6'

services:
  periodic-prune:
    image: f213/periodic-docker-prune:1.1.0
        
    # may be omitted, 05:24 by default
    environment:
      AT: '02:44'
    
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      
```

## Manual

```sh
$ docker run -v "/var/run/docker.sock:/var/run/docker.sock" -e AT='17:20' f213/periodic-docker-prune
```
