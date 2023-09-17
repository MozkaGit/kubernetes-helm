# Déploiement de l'application WordPress avec Helm

Ce dépôt contient les instructions et les commandes nécessaires pour déployer l'application WordPress en utilisant Helm.

## Étapes

1. Installez Helm en suivant la documentation disponible ici : [https://github.com/diranetafen/supinfokubernetes/tree/minikube/tp07#-install-helm-](https://github.com/diranetafen/supinfokubernetes/tree/minikube/tp07#-install-helm-)

2. Utilisez le chart WordPress [https://github.com/bitnami/charts/tree/main/bitnami/wordpress](https://github.com/bitnami/charts/tree/main/bitnami/wordpress) pour déployer l'application.

3. Utilisez un service de type NodePort en HTTP. Vous pouvez choisir le numéro de port (NodePort) à utiliser.

4. Surchargez les variables nécessaires en créant un fichier nommé `values.yml` et spécifiez les valeurs suivantes :

```
wordpressUsername: admin
wordpressPassword: password
service:
  type: NodePort
  nodePorts:
    http: "32000"
persistence:
  enabled: false
mariadb:
  enabled: true
  primary:
    persistence:
      enabled: false
```

5. Attendre que les conteneurs démarre puis se connecter sur WordPress à l'aide de son navigateur web en utilisant l'ip du système hôte suivi du NodePort.

## Commandes utilisées

```shell
# Ajout du référentiel Bitnami à Helm
helm repo add bitnami https://charts.bitnami.com/bitnami

# Installation de WordPress en utilisant les valeurs du fichier values.yml
helm install wordpress bitnami/wordpress -f values.yml

# Obtention des ressources déployées dans Kubernetes
kubectl get all

# Description du pod en cours d'exécution
kubectl describe pod

