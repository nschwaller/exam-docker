# Examen Docker

Vous devez fork ce repository, créer les fichiers demandés, puis ajouter un readme comprenant le nom de vos images sous la forme <dockerhub_username>/<image_name>.

Bonne chance !

Le total des points pour cet examen est de 22 points. Voici la répartition :

- Exercice 1 : 4 points
- Exercice 2 : 4 points
- Exercice 3 : 5 points
- Exercice 4 : 3 points
- Exercice 5 : 1 point
- Exercice 6 : 2 points
- Exercice 7 : 3 points

**Exercice 1 (4pt)**
Créez un Dockerfile de dev (appelé *DockerfileDev*) où vous installerez les dépendances nécessaires à savoir :
 - pnpm
 - prisma
 - node_modules (du package.json)

Ce Dockerfile aura pour base une image avec node en version 20, et la commande par défaut lorsqu'on lance le conteneur devra être *l'application des migrations prisma puis le lancement du serveur en mode dev*.

**Exercice 2 (4pt)**

**2pts** Créez un fichier `compose.yml`. Ajoutez un service [mariadb](https://hub.docker.com/_/mariadb) avec la configuration suivante :
 - password root : passwd
 - bdd par défaut : test

*intermédiaire*
**1pt** Ajoutez des variables (d'environnement) Docker compose contenant le mot de passe root et le nom de la bdd utilisé. Créez un .env contenant ces variables d'environnement

*difficile*
**1pt** Ajoutez un healthcheck pour vous assurer du bon démarrage de mariadb

**Exercice 3 (5pt)**

**2pt** Créez un service pour lancer l'application en mode dev. Utilisez le Dockerfile créé à l'exercice 1. 
 - Liez le répertoire de l'application au conteneur via un volume.
 - Ajoutez des variables d'environnement dans le conteneur 
   - `PORT`
   - `DATABASE_URL`
   - `JWT_SECRET`
 - Mappez le port choisi au port 3000 de l'hôte

*intermédiaire*
**1pt** Utilisez des volumes anonymes pour ne pas copier les nodes_modules et le .pnpm-store du conteneur au filesystem de l'hôte
*intermédiaire*
**1pt** Utilisez les variables d'environnement précédemment créées afin de composer l'URL de connexion à la BDD, le JWT secret et le port.
*intermédiaire*
**1pt** Attendez que la bdd soit fonctionnelle (à l'aide du healthcheck) avant de lancer le conteneur de dev

**Exercice 4 (3pt)**

Créez un Dockerfile de production pour l'application graphql-auth.
 - Build l'application
 - Lancez, en commande, l'app builder (**pas de pnpm dev !**)
 - Optimisez les layers Docker
   - Un changement de la codebase ne doit pas déclencher un full rebuild, uniquement le build de l'app
   - Ajoutez dans le Dockerfile la variable d'environnement `NODE_ENV` avec la valeur `production`

Buildez l'image, attribuez-lui la version `0.1` et `latest`, puis poussez votre image sur DockerHub.

**Exercice 5 (1pt)**

Ajoutez au fichier Docker compose un service utilisant l'image de prod construite pendant l'exercice 4.

**Exercice 6 (2pt)**

**1pt** Faites un merge de la branche `with-comment` vers main. Relancez un build, en taguant cette fois l'image avec la version `0.2`. Cette image devra maintenant être celle qui sera pull par défaut si on ne spécifie pas de version.
Poussez la nouvelle image sur DockerHub.

*difficile*
**1pt** Créez la nouvelle image en mode multi plateforme pour les aarch (architecture processeur) suivants :
 - linux/arm64
 - linux/amd64

**Exercice 7 (3pt)**

Vous trouverez dans le dossier `geek-life` une application pour le terminal écrit en Golang. 
Créez un Dockerfile, en multistage build, afin de créer une image avec l'application.

```sh
# Build command
go build -o geek-life ./app
```

Faites un push de l'application sur dockerhub en la taguant en `latest`.