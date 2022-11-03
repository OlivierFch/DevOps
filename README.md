# Réponses Olivier Foucher

## Réponses TP1 - Docker

### 1-1: Document your database container essentials: commands and Dockerfile
- On setup un environnement de base de données avec son nom, un identifiant et un mot de passe
- On lui insère 2 tables et des données en lui précisant les chemins
- Voir [Dockerfile](./TP1/TP_Docker/Dockerfile)

### 1-2: Why do we need a multistage build? And explain each step of this dockerfile
- Le "multistage build" permet d'optimiser les Dockerfiles tout en les gardant faciles à lire et à maintenir. On peut utiliser plusieurs instruction ```FROM``` dans le Dockerfile. Chaque instruction ```FROM```, on peut utiliser une base différente, et chacune d'entre elles commence une nouvelle étape de build.

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

## Réponses TP2 - Github Actions

### 2-1 What are testcontainers?
- Les testcontainers sont des containers qui fournissent des instances légères et jetables de bases de données courantes que l'on utilise pour run des tests unitaires.

### 2-2 Document your Github Actions configurations
Le .main.yml se décompose en deux jobs, ```test-backend``` et ```build-and-push-docker-image```.
- Le ```test-backend```:
    - Checkout repository
    - Set up JDK 11
    - Cache SonarCloud packages
    - Cache Maven packages
    - Build and test with Maven
- Le ```build-and-push-docker-image```:
    - A besoin que le test-backend soit réalisé
    - Checkout code
    - Login to DockerHub
    - Build image and push backend
    - Build image and push database
    - Build image and push httpd

### 2-3 Document your quality gate configuration
![Quality gate](./images/Quality%20gate.png)

## Réponses TP3 - Ansible

### 3-1 Document your inventory and base commands
- Dans le dossier inventory, on trouve le fichir de setup. Ce fichier de setup permet, grâce à Ansible, de se connecter a un serveur distant. Dans ce fichier on définit l'user, le chemin pour acceder à la clé privée, et le nom de l'hôte

### 3-2 Document your playbook
- Dans le dossier rôle, on trouve deux playbook, ``playbook.yml`` est celui créée lors du td, pour tester. ``playbookDocker.yml`` est le playbook permettant de lancer tous les rôles.
- Dans ``playbookDocker.yml`` on retrouve l'ensemble des rôles définis dans Ansible. Cela permet de lancer toutes les tâches dans le bon ordre : Docker > network > proxy > database > app
- Ensuite, dans chacun des dossier de chaque rôle (db, httpd, simple api...) on retrouve le détail des commandes que Ansible doit réaliser

### 3-3 Document your docker_container tasks configuration
- On retrouve 8 commandes dans les task pour le role docker:
    - *clean package* : enlève tous les packages dans le systeme
    - *Install device-mapper-persistent-data* : permet de donner accès a de l'espace de stockage pour les futurs containers
    - *Install lvm2* : lvm2 permet gérer le volume physique
    - *add repo docker* : ajoute un répository docker
    - *Install Docker* : télécharge docker
    - *install python3* : installer python3
    - *Pip Install* : installer pip
    - *Make sure Docker is running* : on vérifie que docker run, si docker run , toutes les commandes précédentes se sont bien exécutées