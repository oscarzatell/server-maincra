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


```
# Minecraft 1.17 Setup and Installation Ubuntu 16+
# Updating OS and download OpenJDK-16
apt-get update && apt-get upgrade -y
mkdir -p /usr/java/openjdk
mkdir -p /usr/java/openjdk/jdk-16/bin/javac
cd /usr/java/openjdk
wget https://download.java.net/java/GA/jdk16.0.1/7147401fd7354114ac51ef3e1328291f/9/GPL/openjdk-16.0.1_linux-x64_bin.tar.gz
tar zxf openjdk-16.0.1_linux-x64_bin.tar.gz

# Edit profile paths
echo "# OpenJDK 16" >> /etc/profile
echo "JAVA_HOME=/usr/java/openjdk/jdk-16" >> /etc/profile
echo "PATH=$PATH:$HOME/bin:$JAVA_HOME/bin" >> /etc/profile
echo "export JAVA_HOME" >> /etc/profile
echo "export PATH" >> /etc/profile

# Install OpenJDK
#apt install openjdk-11-jre-headless -y
apt install default-jre -y
apt install openjdk-16-jre-headless -y

# List java alternatives and select 16 as the correct version
#update-alternatives --config java

# Create Minecraft 1.17.0
mkdir -p /minecraft/1.17.0/
cd /minecraft/1.17.0/
wget https://launcher.mojang.com/v1/objects/0a269b5f2c5b93b1712d0f5dc43b6182b9ab254e/server.jar
mv server.jar minecraft_server.1.17.0.jar
java -Xmx1024M -Xms1024M -jar minecraft_server.1.17.0.jar nogui

echo "eula=true" > eula.txt

# Start Daemon on Reboot
cd /etc/systemd/system/

touch minecraft-1.17.0.service
chmod +x minecraft-1.17.0.service
echo "[Unit]" >> minecraft-1.17.0.service
echo "Description=Start Mincraft" >> minecraft-1.17.7.service
echo "After=network.target" >> minecraft-1.17.0.service
echo "" >> minecraft-1.17.0.service
echo "[Service]" >> minecraft-1.17.0.service
echo "Type=simple" >> minecraft-1.17.0.service
echo "ExecStart=/minecraft/1.17.0/start.sh" >> minecraft-1.17.0.service
echo "TimeoutStartSec=0" >> minecraft-1.17.0.service
echo "" >> minecraft-1.17.0.service
echo "[Install]" >> minecraft-1.17.0.service
echo "WantedBy=default.target" >> minecraft-1.17.0.service

# Setup MC start script
mkdir -p /minecraft/1.17.0/
cd /minecraft/1.17.0/
touch start.sh
chmod +x start.sh
echo "#!/bin/sh" >> start.sh
echo "cd /minecraft/1.17.0/" >> start.sh
echo "exec java -Xmx1024M -Xms1024M -jar minecraft_server.1.17.0.jar nogui" >> start.sh

# Setup Server Properties
cp server.properties server.properties.old

echo "#Minecraft server properties" > server.properties
echo "#Sun Jun 13 09:20:44 UTC 2021" >> server.properties
echo "enable-jmx-monitoring=false" >> server.properties
echo "rcon.port=25575" >> server.properties
echo "level-seed=666" >> server.properties
echo "enable-command-block=false" >> server.properties
echo "gamemode=survival" >> server.properties
echo "enable-query=false" >> server.properties
echo "generator-settings=" >> server.properties
echo "level-name=devils_asshair" >> server.properties
echo "motd=Welcome to Devils Peak" >> server.properties
echo "query.port=25565" >> server.properties
echo "pvp=false" >> server.properties
echo "generate-structures=true" >> server.properties
echo "difficulty=easy" >> server.properties
echo "network-compression-threshold=256" >> server.properties
echo "max-tick-time=60000" >> server.properties
echo "max-players=20" >> server.properties
echo "use-native-transport=true" >> server.properties
echo "enable-status=true" >> server.properties
echo "online-mode=false" >> server.properties
echo "allow-flight=true" >> server.properties
echo "broadcast-rcon-to-ops=true" >> server.properties
echo "view-distance=10" >> server.properties
echo "max-build-height=256" >> server.properties
echo "server-ip=" >> server.properties
echo "allow-nether=true" >> server.properties
echo "server-port=25565" >> server.properties
echo "sync-chunk-writes=true" >> server.properties
echo "enable-rcon=false" >> server.properties
echo "server-name=Devils Peak" >> server.properties
echo "op-permission-level=4" >> server.properties
echo "prevent-proxy-connections=false" >> server.properties
echo "resource-pack=" >> server.properties
echo "entity-broadcast-range-percentage=100" >> server.properties
echo "player-idle-timeout=0" >> server.properties
echo "rcon.password=" >> server.properties
echo "force-gamemode=false" >> server.properties
echo "rate-limit=0" >> server.properties
echo "hardcore=false" >> server.properties
echo "white-list=false" >> server.properties
echo "broadcast-console-to-ops=true" >> server.properties
echo "spawn-npcs=true" >> server.properties
echo "spawn-animals=true" >> server.properties
echo "snooper-enabled=true" >> server.properties
echo "function-permission-level=2" >> server.properties
echo "level-type=default" >> server.properties
echo "text-filtering-config=" >> server.properties
echo "spawn-monsters=true" >> server.properties
echo "enforce-whitelist=false" >> server.properties
echo "spawn-protection=16" >> server.properties
echo "resource-pack-sha1=" >> server.properties
echo "max-world-size=29999984" >> server.properties

# Enable / Start Service
systemctl enable minecraft-1.17.0.service
systemctl start minecraft-1.17.0.service
systemctl status minecraft-1.17.0.service

```

```
# Minecraft 1.17 Setup and Installation Ubuntu 16+
# Updating OS and download OpenJDK-16
apt-get update && apt-get upgrade -y
mkdir -p /usr/java/openjdk
mkdir -p /usr/java/openjdk/jdk-16/bin/javac
cd /usr/java/openjdk
wget https://download.java.net/java/GA/jdk16.0.1/7147401fd7354114ac51ef3e1328291f/9/GPL/openjdk-16.0.1_linux-x64_bin.tar.gz
tar zxf openjdk-16.0.1_linux-x64_bin.tar.gz

# Edit profile paths
echo "# OpenJDK 16" >> /etc/profile
echo "JAVA_HOME=/usr/java/openjdk/jdk-16" >> /etc/profile
echo "PATH=$PATH:$HOME/bin:$JAVA_HOME/bin" >> /etc/profile
echo "export JAVA_HOME" >> /etc/profile
echo "export PATH" >> /etc/profile

# Install OpenJDK
#apt install openjdk-11-jre-headless -y
apt install default-jre -y
apt install openjdk-16-jre-headless -y

# List java alternatives and select 16 as the correct version
#update-alternatives --config java

# Create Minecraft 1.17.1
mkdir -p /minecraft/1.17.1/
cd /minecraft/1.17.1/
wget https://launcher.mojang.com/v1/objects/a16d67e5807f57fc4e550299cf20226194497dc2/server.jar
mv server.jar minecraft_server.1.17.1.jar
java -Xmx1024M -Xms1024M -jar minecraft_server.1.17.1.jar nogui

echo "eula=true" > eula.txt

# Start Daemon on Reboot
cd /etc/systemd/system/

touch minecraft-1.17.1.service
chmod +x minecraft-1.17.1.service
echo "[Unit]" >> minecraft-1.17.1.service
echo "Description=Start Mincraft" >> minecraft-1.17.1.service
echo "After=network.target" >> minecraft-1.17.1.service
echo "" >> minecraft-1.17.1.service
echo "[Service]" >> minecraft-1.17.1.service
echo "Type=simple" >> minecraft-1.17.1.service
echo "ExecStart=/minecraft/1.17.1/start.sh" >> minecraft-1.17.1.service
echo "TimeoutStartSec=0" >> minecraft-1.17.1.service
echo "" >> minecraft-1.17.1.service
echo "[Install]" >> minecraft-1.17.1.service
echo "WantedBy=default.target" >> minecraft-1.17.1.service

# Setup MC start script
mkdir -p /minecraft/1.17.1/
cd /minecraft/1.17.1/
touch start.sh
chmod +x start.sh
echo "#!/bin/sh" >> start.sh
echo "cd /minecraft/1.17.1/" >> start.sh
echo "exec java -Xmx1024M -Xms1024M -jar minecraft_server.1.17.1.jar nogui" >> start.sh

# Setup Server Properties
cp server.properties server.properties.old

echo "#Minecraft server properties" > server.properties
echo "#Sun Jun 13 09:20:44 UTC 2021" >> server.properties
echo "enable-jmx-monitoring=false" >> server.properties
echo "rcon.port=25575" >> server.properties
echo "level-seed=666" >> server.properties
echo "enable-command-block=false" >> server.properties
echo "gamemode=survival" >> server.properties
echo "enable-query=false" >> server.properties
echo "generator-settings=" >> server.properties
echo "level-name=devils_asshair" >> server.properties
echo "motd=Welcome to Devils Peak" >> server.properties
echo "query.port=25565" >> server.properties
echo "pvp=false" >> server.properties
echo "generate-structures=true" >> server.properties
echo "difficulty=easy" >> server.properties
echo "network-compression-threshold=256" >> server.properties
echo "max-tick-time=60000" >> server.properties
echo "max-players=20" >> server.properties
echo "use-native-transport=true" >> server.properties
echo "enable-status=true" >> server.properties
echo "online-mode=false" >> server.properties
echo "allow-flight=true" >> server.properties
echo "broadcast-rcon-to-ops=true" >> server.properties
echo "view-distance=10" >> server.properties
echo "max-build-height=256" >> server.properties
echo "server-ip=" >> server.properties
echo "allow-nether=true" >> server.properties
echo "server-port=25565" >> server.properties
echo "sync-chunk-writes=true" >> server.properties
echo "enable-rcon=false" >> server.properties
echo "server-name=Devils Peak" >> server.properties
echo "op-permission-level=4" >> server.properties
echo "prevent-proxy-connections=false" >> server.properties
echo "resource-pack=" >> server.properties
echo "entity-broadcast-range-percentage=100" >> server.properties
echo "player-idle-timeout=0" >> server.properties
echo "rcon.password=" >> server.properties
echo "force-gamemode=false" >> server.properties
echo "rate-limit=0" >> server.properties
echo "hardcore=false" >> server.properties
echo "white-list=false" >> server.properties
echo "broadcast-console-to-ops=true" >> server.properties
echo "spawn-npcs=true" >> server.properties
echo "spawn-animals=true" >> server.properties
echo "snooper-enabled=true" >> server.properties
echo "function-permission-level=2" >> server.properties
echo "level-type=default" >> server.properties
echo "text-filtering-config=" >> server.properties
echo "spawn-monsters=true" >> server.properties
echo "enforce-whitelist=false" >> server.properties
echo "spawn-protection=16" >> server.properties
echo "resource-pack-sha1=" >> server.properties
echo "max-world-size=29999984" >> server.properties

# Enable / Start Service
systemctl enable minecraft-1.17.1.service
systemctl start minecraft-1.17.1.service
systemctl status minecraft-1.17.1.service


```

