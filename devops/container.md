## Manipuler un conteneur

Pour observer un conteneur en cour d'exécution lancer la commande suivante.

```docker run -d --name looper debian:bullseye-slim sh -c 'while true; do date; sleep 1; done'```

Effectuez les operations suivantes:
1. Vérifiez que le conteneur est en cours d'exécution
2. Observez en *continue* les logs générés par le conteneur
3. Mettez en pause l'exécution du conteneur et observez le résultat dans les logs
4. Débloquez l'exécution le conteneur et observez le résultat dans les logs
5. Tout en conservant un terminal qui affiche les logs, ouvrez un nouveau terminal 
   dans lequel vous viendrez vous attacher au conteneur en cours d'exécution.
   (utiliser *docker attach*)
6. Exécutez *CRTL+C* (signal *SIGINT*) pour vous détachez du conteneur et observez 
   ce qu'il se passe
7. Utilisez la commande *docker exec* pour créer un fichier au sein du conteneur
   en cours d'exécution (*touch fichier.txt*)
   - *docker exec -d [CONTAINER_ID] touch fichier.txt*
8. Vous connecter au conteneur en cours d'exécution et vérifier que le fichier a 
   bien été créé
   - *docker exec -it [CONTAINER_ID] bash*