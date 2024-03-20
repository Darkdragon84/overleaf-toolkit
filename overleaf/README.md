# Docker compose deployment using traefik

This folder supplies a docker compose based deployment using traefik instead of nginx as reverse-proxy and protonmail-bridge
accessible through an external docker network under the name `protonmail-bridge` using smtp port `25`.

## First startup

To initialize the database correctly, run

```bash
docker compose up mongo -d
docker compose exec -T mongo sh -c '
    while ! mongo --eval "db.version()" > /dev/null; do
      echo "Waiting for Mongo..."
      sleep 1
    done
    mongo --eval "rs.initiate({ _id: \"overleaf\", members: [ { _id: 0, host: \"mongo:27017\" } ] })" > /dev/null'
```
