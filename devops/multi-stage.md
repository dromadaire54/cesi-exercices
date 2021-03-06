# Utilisation du multistage
## Introduction
 Deux web services sont disponibles:
   * ```/add?usualLastName=<last_name>&birthLastName=<birth>&firstName=<first>```
   * ```/all``` 
   * Les artifacts sont dans le dossier ```target```
## Création de l'image de l'application
  
  1. La création d'un image de l'application à partir d'un argument ```VERSION``` qui sera ```1.0.0-SNAPSHOT``` par défaut ***dans les deux stages***.
  2. Créer un ```Dockerfile``` **multistage**. Le premier stage utilisera l'image ```maven:3.8.5-openjdk-11-slim``` et consistera à builder le projet afin d'avoir un artifact (fichier ```spring-boot-${VERSION}.jar```).
  3. La deuxième partie utiliera ```eclipse-temurin:11.0.15_10-jre-alpine``` et consistera à copier le fichier jar du premier stage dans le home et de le renommer en ```sample.jar``` (par défaut ```/root```) et de lancer le le fichier à l'aide de la commande ```java -jar```
  4. Builder l'image avec le nom ```sample```
  5. Vérifier qui l'image est construit correctement
  6. Essayer de lancer un conteneur à partir de l'image ```sample``` avec les variables suivantes:
       * MYSQL_HOST=
       * USER=
       * PASSWORD=

Pour la partie base de données:
 * lancer la commande suivante ```docker run --name db -e MARIADB_ROOT_PASSWORD=test -v votre-path-à-vous/sample-springboot/fixtures/:/docker-entrypoint-initdb.d -v /tmp/data:/var/lib/mysql mariadb:10.8.2```
 * Récupérer l'ip du conteneur à l'aide de ```docker inspect```
 * Renseigner les variables d'environnement

L'ip du ```MYSQL_HOST``` est celui de votre host il contenu dans l'interface ```docker0```