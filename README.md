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

```
version: "3"

services:
  maincra:
    image: ${IMAGE:-itzg/minecraft-server}
    environment:
      EULA: "TRUE"
      TYPE: BUKKIT
      ONLINE_MODE: "FALSE"
      MAX_PLAYERS: 2
      MAX_WORLD_SIZE: 1000
      MEMORY: 1500M
      MAX_MEMORY: 1500M
      TZ: America/Mexico_City
      OPS: elAzkor
      SEED: 1785852800490497919
      ENABLE_COMMAND_BLOCK: "TRUE"
      plugins: https://papermc.io/api/v2/projects/paper/versions/1.17.1/builds/251/downloads/paper-1.17.1-251.jar
      SPIGET_RESOURCES: 9089,34315
    ports:
      - 25565:25565
    volumes:
      - /root/docker/maincra:/data
```

```
version: "3"

services:
  maincra:
    image: ${IMAGE:-itzg/minecraft-server}
    environment:
      EULA: "TRUE"
      VERSION: 1.17.1
      TYPE: PAPER
      ONLINE_MODE: "FALSE"
      MAX_PLAYERS: 2
      MAX_WORLD_SIZE: 1000
      MEMORY: 1500M
      MAX_MEMORY: 1500M
      TZ: America/Mexico_City
      OPS: elAzkor
      SEED: 1785852800490497919
      ENABLE_COMMAND_BLOCK: "TRUE"
      plugins: https://ci.opencollab.dev//job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifa$
      SPIGET_RESOURCES: 9089,34315
    ports:
      - 25565:25565
      - 19132:19132
    volumes:
      - /root/docker/maincra:/data

```

```
version: "3"

services:
  maincra:
    image: ${IMAGE:-itzg/minecraft-server}
    environment:
      EULA: "TRUE"
      VERSION: 1.17.1
      TYPE: PAPER
      ONLINE_MODE: "FALSE"
      MAX_PLAYERS: 2
      MAX_WORLD_SIZE: 1000
      MEMORY: 1500M
      MAX_MEMORY: 1500M
      TZ: America/Mexico_City
      OPS: elAzkor
      SEED: 1785852800490497919
      ENABLE_COMMAND_BLOCK: "TRUE"
      plugins:
      SPIGET_RESOURCES: 9089,34315,28140,82278
    ports:
      - 25565:25565
      - 19132:19132
    volumes:
      - /root/docker/maincra:/data
```












