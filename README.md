# server-maincra

```
version: "3"

services:
  maincra:
    image: ${IMAGE:-itzg/minecraft-server}
    environment:
      EULA: "TRUE"
      TYPE: FORGE
      ONLINE_MODE: "FALSE"
      MAX_PLAYERS: 2
      MAX_WORLD_SIZE: 1000
      MEMORY: 1500M
      MAX_MEMORY: 1500M
      TZ: America/Mexico_City
      OPS: elAzkor
      SEED: 1785852800490497919
      ENABLE_COMMAND_BLOCK: "TRUE"
    ports:
      - 25565:25565
    volumes:
      - /root/mc:/data

volumes:
  maincra: {}

```
