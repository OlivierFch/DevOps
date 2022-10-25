# Réponses Olivier Foucher

## Réponses TP1

### 1-1: Document your database container essentials: commands and Dockerfile
- On setup un environnement de base de données avec son nom, un identifiant et un mot de passe
- On lui insère 2 tables et des données en lui précisant les chemins
- Voir [Dockerfile](./TP1/TP_Docker/Dockerfile)

### 1-2: Why do we need a multistage build? And explain each step of this dockerfile
- On a besoin d'un "multistage build"

### 1-3: Document docker-compose most important commands
- version : Ici la version de Docker
- services : Ici (database, backend, proxy/httpd)
- network : Permet de relier les containers
- volumes : Avoir de la persistance des données

### 1-4: Document your docker-compose file
- On définit la version de Docker
- On commence par créer un network dans lequel se retrouve les différents containers qui interagit entre eux.
- On créé les couches en précisant leurs noms, leurs chemins dans le projet, le network auquels ils appartiennent, les ports (httpd) et les volumes (database).
- Voir [Dockerfile](./TP1/docker-compose.yml)

## Réponses TP2

### 2-1 What are testcontainers?
- Element 1

### 2-2 Document your Github Actions configurations
- Element 1

### 2-3 Document your quality gate configuration
- Element 1

## Réponses TP3

### 3-1 Document your inventory and base commands
- Element 1

### 3-2 Document your playbook
- Element 1

### 3-3 Document your docker_container tasks configuration

