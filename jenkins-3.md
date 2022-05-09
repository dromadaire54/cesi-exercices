# Exercice Jenkins (partie 3)
## Commandes utiles
```sh 
# Commande qui de changer la version de l'artifact dans le pom.xml
# -e produit les messages d'erreur pendant l'execution
# -B exécute en mode batch
mvn -e -B versions:set -DnewVersion=<version>
mvn -e -B versions:commit
```
## Préparer la release
1) Modifier le jenkinsfile afin de gérer les tags
2) Vérifier dans jenkins dans l'onglet ```tags``` que le build a bien été ajouté

## Déployer la release vers le registre
1) Modifer le jenkinsfile afin que l'artifact soit déployé vers le registre
2) Vérifier sur le registre que l'artifact se trouve le bon répertoire