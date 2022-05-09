# Exercice jenkins (Partie 1)
## Vérification de l'installation
* Vérifier si jenkins est bien lancé (http://IP_VM:8080)
* Vérifier si le registre est bien lancé (http://IP_VM:8180)

## Création d'un projet springboot
1) Créer un projet github ```sample-springboot```
2) Créer un projet springboot ```sample-springboot``` à l'aide du site https://start.spring.io/ et télécharger le fichier zip
3) Décompresser le fichier zip et copier-le contenu dans votre projet.

## Configuration du projet maven
Dans le fichier pom.xml rajouter cette partie
```
<distributionManagement>
				<repository>
					<id>reposilite-repository-releases</id>
					<name>Reposilite Repository</name>
					<url>http://IP_VM:8081/releases</url>
				</repository>
				<snapshotRepository>
					<id>reposilite-repository-snapshots</id>
					<name>Reposilite Repository</name>
					<url>http://IP_VM:8081/snapshots</url>
				</snapshotRepository>
	</distributionManagement>
```
## Commande utiles
```sh 
# Lance les tests unitaires
mvn test

# Permet de générer le fichier artifact en ne fesant pas les tests
mvn package -DskipTests

# commande qui permet d'uploader l'artifact sur le registre
mvn deploy 
```
## Jenkinsfile
```
node {
    stage("Checkout Source Code"){
        echo "Checkout Source Code"
        checkout scm
    }
}
```

Utilisation du plugin configFileProvider et un profile:
```
configFileProvider([configFile(fileId: id_config, variable: 'MAVEN_SETTINGS')]) {
    // Exécuter la commande mvn avec le settings
    sh "mvn dhploy -s $MAVEN_SETTINGS -Preposilite"
}
```

1) Création d'une ```pipeline multibranch``` avec le nom ```sample-pipeline```
2) Ajouter une source vers votre projet github
3) Sur votre projet github ajouter un fichier Jenkinsfile avec trois étapes ```Checkout Source Code```, ```Run unit tests``` et ```Build artifact```
4) Ajouter une étape ```Deploy``` dans le jenkinsfile
5) Vérifier sur le registre si le fichier a bien été ajouté sur le bon dépôt
6) Modifier le web service en changeant le message retour et committer 
7) Pousser les chnagements sur le dépôt distant
8) Vérifier le build sur jenkins et vérifier si l'artifact a été mis à jour


