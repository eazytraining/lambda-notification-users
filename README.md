# Déploiement d’une App sur Lambda et DynamoDB pour des notifications de transaction bancaires

![](<Architecture App.png>)


## Fonctionnalités :
- Notification par mail
- Schedule des opérations
- Persistance des données

## Services :

### Réseau
- **API GATEWAY** : permet de créer, publier, maintenir et sécuriser des API à grande échelle. Il facilite le routage des requêtes vers des services backend, gère l'authentification et le contrôle d'accès, et permet d'intégrer des fonctions comme la mise en cache et la surveillance des performances. AWS API Gateway simplifie le développement et l'exploitation d'API pour les applications basées sur le cloud.

### Sécurité
- **SECRET MANAGER** : Service qui permet de stocker et de gérer les secrets (comme les mots de passe et les clés API) de manière sécurisée.
- **IAM (Identity and Access Management)** : Définir ce que les utilisateurs et les rôles peuvent faire avec les ressources AWS.
  - **Rôle** : Un rôle IAM est une entité qui définit un ensemble de permissions pour effectuer des actions sur des ressources AWS. Contrairement aux utilisateurs, les rôles ne sont pas associés à une personne ou un compte spécifique, mais peuvent être assumés par des services AWS, des utilisateurs ou des applications. Les rôles sont souvent utilisés pour accorder des permissions temporaires.
  - **Permission** : Définir ce que les utilisateurs et les rôles peuvent faire avec les ressources AWS.
 
### Stockage
- **S3 (Simple Storage Service)** : Service de stockage d'objets pour stocker et récupérer des données à tout moment.

### Base de données
- **DynamoDB** : Base de données NoSQL entièrement gérée qui offre des performances rapides et prévisibles à n'importe quelle échelle, avec un modèle de données flexible et une latence faible.

### Calcul
- **Lambda** : Service de calcul sans serveur qui exécute du code en réponse à des événements et gère automatiquement l'échelle, permettant de payer uniquement pour le temps d'exécution.

### Messagerie
- **SES (Simple Email Service)** : Service de messagerie évolutif qui permet d'envoyer et de recevoir des e-mails facilement et à faible coût, souvent utilisé pour les notifications et les campagnes marketing.

### Evenement et d'intégration d'applications
- **EventBridge** : Permet de relier différentes applications et services en facilitant la gestion et le routage des événements, favorisant ainsi une architecture orientée événements dans le cloud

### Surveillance et Gestion des Ressources
- **CLOUDWATCH** : Service de surveillance qui collecte et suit les métriques, les journaux, et les événements pour les ressources AWS.
  - **Logs Groups** : Regroupe les journaux pour une gestion et une analyse centralisées.

## Process : 

# Processus d'Implémentation des Notifications d'Opérations Bancaires avec AWS

## 1. Conception de l'Architecture

### 1.1. Diagramme d'Architecture
- Créer un diagramme représentant les services interconnectés :
  - API Gateway pour les points d'entrée
  - Lambda pour le traitement
  - DynamoDB pour le stockage des données
  - SES pour l'envoi d'e-mails
  - EventBridge pour la gestion des événements
  - CloudWatch pour la surveillance

## 2. Configuration des Services AWS

### 2.1. API Gateway
- **Création d'API :**
  - Définir des endpoints pour les opérations de notification (ex. création, mise à jour).
  - Configurer l'authentification avec IAM.

### 2.2. IAM et Secret Manager
- **Gestion des Accès :**
  - Créer des rôles IAM pour définir les permissions d'accès nécessaires pour les services.
  - Utiliser AWS Secrets Manager pour stocker les informations sensibles (ex. clés API, mots de passe).

### 2.3. Stockage avec S3 et DynamoDB
- **DynamoDB :**
  - Concevoir une structure de base de données pour stocker les informations des utilisateurs et leurs opérations.
- **S3 :**
  - Utiliser S3 pour stocker des fichiers de logs ou des données supplémentaires si nécessaire.

## 3. Mise en Place de la Logique Métier

### 3.1. AWS Lambda
- **Développement de Fonctions Lambda :**
  - Écrire des fonctions pour traiter les notifications et interagir avec DynamoDB.
  - Configurer des déclencheurs Lambda via API Gateway et EventBridge.

## 4. Gestion des Événements

### 4.1. Amazon EventBridge
- **Configuration des Règles :**
  - Créer des règles pour déclencher des événements en fonction des opérations bancaires (ex. dépôt, retrait).
  - Intégrer les événements avec des fonctions Lambda pour le traitement.

## 5. Envoi des Notifications

### 5.1. Amazon SES
- **Configuration d'Amazon SES :**
  - Vérifier les domaines et les adresses e-mail pour l'envoi d'e-mails.
  - Créer des modèles d'e-mails pour les notifications (ex. confirmation de dépôt).

## 6. Surveillance et Gestion

### 6.1. Amazon CloudWatch
- **Mise en Place de la Surveillance :**
  - Configurer des groupes de logs pour collecter les journaux des fonctions Lambda et des API Gateway.
  - Créer des alarmes pour suivre les métriques importantes (ex. erreurs, latence).

## 7. Tests et Validation

### 7.1. Tests de Fonctionnalité
- Effectuer des tests unitaires et d'intégration pour s'assurer que tous les composants fonctionnent ensemble.

### 7.2. Scénarios de Charge
- Simuler des scénarios de charge pour tester la scalabilité de l'architecture.

## 8. Déploiement et Maintenance

### 8.1. Déploiement
- Utiliser AWS CloudFormation ou un autre outil d'infrastructure as code pour déployer l'architecture.

### 8.2. Maintenance
- Mettre en place un plan de maintenance pour surveiller et mettre à jour les ressources au besoin.
