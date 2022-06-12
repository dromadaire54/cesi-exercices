## Construire une image

### Construire une image
Nous allons construire une image à partir d'un fichier Dockerfile

Créer un répoertoire dans lequel sera stocké le ```Dockerfile```
```
mkdir whalesay
cd whalesay
nano Dockerfile
```

Ajoutez le contenu suivant dans le fichier ```Dockerfile```

```
FROM docker/whalesay

CMD cowsay meeuuuuh
```

Expliquez le contenu de ce Dockerfile

Créer une image avec le nom ```my-whalesay```

Puis démarrer un conteneur avec le nom ```whalesay-start``` à partir de l'image ```my-whalesay```.

Créer un fichier ```fortune.Dockerfile``` et ajouter le contenu suivant.

```
FROM docker/whalesay:latest

RUN apt-get -y update
RUN apt-get install -y fortunes

CMD /usr/games/fortune -a | cowsay
```

Lancer une image à partir du fichier ```fortune.Dockerfile``` avec le nom ```fortune-image```

Puis lancer un conteneur avec le ```fortune-start``` à partir de l'image ```fortune-image```