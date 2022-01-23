# DockerMC

## Table des matières

- [DockerMC](#dockermc)
  - [Table des matières](#table-des-matières)
  - [Information](#information)
  - [Minimum requis](#minimum-requis)
  - [Fonctionnement](#fonctionnement)
    - [Lancement d'un serveur](#lancement-dun-serveur)
    - [Création d'un nouveau serveur](#création-dun-nouveau-serveur)
      - [Exemples de fichier docker-compose.yml](#exemples-de-fichier-docker-composeyml)
        - [Avec le lien du monde](#avec-le-lien-du-monde)
        - [Sans le lien du monde](#sans-le-lien-du-monde)
  - [Commandes utiles](#commandes-utiles)

## Information

Chaque dossier est un serveur Minecraft

## Minimum requis

- Avoir Docker installé sur sa machine
- Avoir Minecraft installé sur sa machine

## Fonctionnement

### Lancement d'un serveur

- Choissisez le serveur qui vous intéresse
- Déplacez-vous dans le dossier du serveur
- Puis dans l'invite de commandes, tapez : ```docker-compose up``` ou ```docker-compose up -d```
- Ensuite il vous reste qu'à vous connecter au serveur Minecraft avec votre adresse IP locale
- Pour arrêter le serveur vous pouvez tapez : ```docker-compose down```

---

### Création d'un nouveau serveur

- Créer un dossier du nom du serveur
- Déplacez-vous dans le nouveau dossier
- Créez les dossiers **minecraft-data** et **world**
- Créez le fichier **docker-compose.yml**
- Rajoutez les informations
  - Nom du service (Nom du serveur)
  - Numéro de version de Minecraft
  - Carte (Lien ou déplacez le contenu de la carte dans le dossier world)
  - Options
  - **Les volumes** (**minecraft-data** et **world** s'il ne s'agit pas d'un lien)

#### Exemples de fichier docker-compose.yml

##### Avec le lien du monde

```
version: "3"

services:
  InfiniteDungeon:
    image: itzg/minecraft-server
    container_name: infinitedungeon
    ports:
      - 25565:25565
    environment:
      EULA: "TRUE"
      VERSION: 1.18
      MEMORY: 8G
      WORLD: https://www.dropbox.com/s/2nrdo4vdj3h0b0b/InfinityDungeons%20v1.1.1.1.1.18.zip
      ENABLE_COMMAND_BLOCK: "TRUE"
      SPAWN_PROTECTION: 0
      DIFFICULTY: easy
      GAMEMODE: 2
      OP_PERMISSION_LEVEL: 4
      OPS: loviflo
    tty: true
    stdin_open: true
    restart: unless-stopped
    volumes:
      - ./minecraft-data:/data
```

##### Sans le lien du monde

```
version: "3"

services:
  SuperMinecraftGalaxy:
    image: itzg/minecraft-server
    container_name: superminecraftgalaxy
    ports:
      - 25565:25565
    environment:
      EULA: "TRUE"
      VERSION: 1.16.4
      MEMORY: 8G
      WORLD: /worlds/world
      FORCE_WORLD_COPY: "TRUE"
      ENABLE_COMMAND_BLOCK: "TRUE"
      SPAWN_PROTECTION: 0
      DIFFICULTY: easy
      GAMEMODE: 0
      OP_PERMISSION_LEVEL: 4
      OPS: loviflo
    tty: true
    stdin_open: true
    restart: unless-stopped
    volumes:
      - ./minecraft-data:/data
      - ./world:/worlds/world
```

## Commandes utiles

- [Commandes Serveur](https://github.com/itzg/docker-minecraft-server)
- [Commandes Server.properties](https://github.com/petemcw/docker-minecraft-server)
