# Exercice Jenkins (partie 4)
## Création d'un service
Création d'un répertoire dans ```/opt/sample-springboot/``` et ```/opt/sample-springboot/config```. Ajoutez un fichier ```sample-springboot.sh``` avec le contenu suivant:
```sh
#!/bin/sh
cd /opt/sample-springboot
/usr/bin/java -jar sample-springboot.jar
```

Dans le répertoire ```/etc/systemd/system``` ajoutez un fichier ```sample-springboot.service```.
```
[Unit]
Description=Sample springboot
After=syslog.target network.target
 
[Service]
ExecStart=/opt/sample-springboot/sample-springboot.sh
Type=simple
User=root
PIDFile=/var/run/sample-springboot.pid
 
[Install]
WantedBy=multi-user.target
```

Ajoutez le nouveau service
```sh
systemctl enable sample-springboot.service
```

Dans le répertoire ```/opt/sample-springboot/config``` ajoutez un fichier ```application.yaml``` avec le contenu suivant:
```
server:
  port: 8989
```

Ajoutez un script ```update.sh``` dans le répertoire ```/opt/sample-springboot/``` (***Attention modifiez le chemin dans le requête)***.
```sh
#!/bin/sh
curl -u admin:admin http://IP_VM:8081/api/maven/latest/file/snapshots/com/sample/spring-boot/0.0.1-SNAPSHOT > /opt/sample-springboot/sample-springboot.jar
systemctl restart sample-springboot.service
```

Pour l'exécution du script sans demande de mot de passe. Il faut que l'utilisateur ```jenkins``` partage sa clé publique avec le l'utilisateur ```root```.
```sh
# Se connecter en tant qu'utilisateur jenkins
su - jenkins

# Création de paire clé publique/privée
ssh-keygen -t rsa

# Copie de la clé publique vers le user root
ssh-copy-id -i ~/.ssh/id_rsa.pub root@IP_VM
```
## Commandes utiles
```sh
ssh root@IP_VM ./opt/sample-springboot/update.sh

chmod +x fichier.sh
```

1) Modifiez lme Jenkinsfile afin de récupérer le nouvel artifact et mettre à jour le service
2) Vérifiez que le service a bien démarré
3) Ajoutez un nouveau web service dans le projet, committez et poussez les modifications
4) Une fois le build terminé vérifiez que le nouveau web service est disponible.