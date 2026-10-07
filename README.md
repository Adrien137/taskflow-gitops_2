# taskflow-gitops — dépôt GitOps du cours CI/CD M2

Ce dépôt décrit **l'état voulu** de l'application TaskFlow dans Kubernetes.
Argo CD le surveille et aligne le cluster dessus : pour changer la production,
on ne tape pas de commande, on fait une **Pull Request**.

## Installation (à faire chez vous, avant le cours)

Prérequis : Docker Desktop démarré, 8 Go de RAM, 10 Go de disque libre.
Sous Windows : WSL2 (Ubuntu) + intégration WSL de Docker Desktop, et toutes les commandes dans WSL.

```bash
git clone https://github.com/9m7fjfpv9k-cyber/taskflow-gitops.git
cd taskflow-gitops
./scripts/install.sh
```

Le script crée un cluster local `kind`, installe Argo CD et Argo Rollouts,
puis télécharge les images des labs. Comptez 5 à 15 minutes.
Il peut être relancé sans risque.

## Structure

| Chemin | Rôle |
| --- | --- |
| `apps/taskflow/` | Les manifests surveillés par Argo CD |
| `argocd/application.yaml` | Déclare l'application dans Argo CD |
| `exemples/bluegreen/` | Manifests pour le déploiement Blue-Green |
| `exemples/canary/` | Manifests pour le déploiement Canary |
| `scripts/install.sh` | Installation de l'environnement |
| `scripts/argocd-ui.sh` | Ouvre l'interface d'Argo CD |
| `scripts/observe.sh` | Montre quelle version répond, et avec quel code HTTP |

## Images disponibles

`ghcr.io/9m7fjfpv9k-cyber/taskflow` en versions `1.0.0`, `1.1.0`, `2.0.0` et `2.1.0`.

## Équipe

- Adrien

- Ewan

## Rendu : 

Ajout du repo github a l'application ArgoCD :

![alt text](image.png)

Pod kube running : 

![alt text](image-1.png)

Push de mon code depuis la branch dev (vérifier le fonctionnement ) pour ensuite crée une pull request vers main: 

![alt text](image-2.png)

Synced + Health :

![alt text](image-3.png)

Vérification du fonctionnement grâce au script Observe.sh depuis Git bash :

![alt text](image-4.png)

L'image a bien été changé automatiquement par argocd ( les pod con crée et terminer pour les remplacer par les nouveau ) :

![alt text](image-5.png)
![alt text](image-6.png)

Replicas du nombre de 4 :

![alt text](image-7.png)

Dérive sur le nombre de replicas :

![alt text](image-8.png)

Changement de la version de l'image valide puis detection automatique de ArgoCD qui remet sous la bonne version ( verification du health status) :

![alt text](image-9.png)
![alt text](image-10.png)

Revert de l'upgrade de version et verification du revert de l'image :

![alt text](image-11.png)

Argo cd à procéder au rollback en prenant en compte notre revert :

![alt text](image-13.png)

verification du changement de l'image et de l'etat des taskflow:

![alt text](image-12.png)
![alt text](image-14.png)
![alt text](image-15.png)


# Rendu TP BlueGreen/Canary

Remplacement du fichier deployment par rollout : 
![alt text](image-16.png)

