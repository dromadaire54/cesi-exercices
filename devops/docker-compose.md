## Docker-compose (wordpress + base de données)

### Voici un squelette du docker-compose 
```
services:
  db:
  wordpress:
```

Le docker-compose contient deux services:
* Une base de données mysql
* Une application wordpress connectée à la base de données
  
## Le service db
1. La base de données à comme mot de passe root ```hugesecret```
2. Le nom de la base est ```wordpress```
3. Le login de la base est ```wordpress```
4. Le mot de passe du user ```wordpress``` est ```secret```
5. Le service devra utiliser l'image ```mysql```
6. Permettre la persistance des données
   
## Le service wordpress
1. Le service devra utiliser l'image ```wordpress```
2. Le service devra se connecter au serveur ```db``` sur le port ```3306``` en utilisant les identifiants de l'utilisateur ```wordpress```
3. Le service devra redémarrer en cas d'erreur
4. Le port extérieur à l'application sera ```8080``` qui mappera le port du service ```80```

