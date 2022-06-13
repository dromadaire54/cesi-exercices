## Manipuler un conteneur

1. Lancer un conteneur avec le nom ```test-1``` à partir de l'image ```nginx``` (vérifier que le conteneur existe).
2. Arrêter et supprimer le conteneur ```test-1```
3. Lancer un conteneur avec le nom ```test-1``` à partir de l'image de ```nginx``` avec les caractéristiques suivantes:
     * le conteneur sera accesible depuis l'extérieur depuis le port ```8180```
     * Un volume sera disponible entre le répertoire ```/tmp/data``` du host vers le répertoire ```/usr/share/nginx/html```
4. Ajouter un fichier ```index.html``` avec comme contenu ```Je suis dedans``` dans le répertoire ```/tmp/data```.
5. Depuis votre host essayer d'accèder au conteneur et afficher le contenu du répertoire ```/usr/share/nginx/html```.
6. Depuis le host faite ```curl http://localhost:8180```
7. Arrêter et supprimer le conteneur ```test-1```