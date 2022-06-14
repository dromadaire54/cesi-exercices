# Evaluation docker & docker-compose

## Introduction

1. Ce projet contient:
   * un Jenkinsfile avec les instructions afin de build le projet
   * Le projet est en maven
   * Il permet de ce connecter à la base données ainsi que d'ajouter et les lister des personnes
   * Il y a un fichier yaml qui permet de ce connecter à la base
   * L'application est accessible via le port ```8989```
2. Deux web services sont disponibles:
   * ```/add?usualLastName=<last_name>&birthLastName=<birth>&firstName=<first>```
   * ```/all``` 
   
## Création d'un docker-compose

  1. Créer un fichier ```docker-compose.yaml```
  2. Ce fichier contiendra deux service ```db``` et ```sample```
  3. le service ```db``` utilisera l'image ```mariadb:10.8.2``` et il aura comme mot de passe root ```test```. Les données devront être persistées à l'aide d'un volume qui s'appelle ```sample-data```. Un autre volume sera créé qui permettra de relier le répertoire ```fixtures``` au répertoire ```/docker-entrypoint-initdb.d``` afin d'initialiser la base.
  4. Le service ```sample``` utilsera le ```Dockerfile``` précédemment créé. le port l'extérieur sera le même que celui du conteneur.
  5. Créer un fichier .env.list qui contiendra les variables suivantes (on utilisera les identifiants ```root```):
    * MYSQL_HOST=
    * USER=
    * PASSWORD=
  6. Exécuter le docker-compose et essayer d'ajouter des personnes puis lister les.
   
