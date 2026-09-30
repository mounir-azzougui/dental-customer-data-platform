# Stratégie de recette

## Objectif

La recette vérifie que les fichiers sont contrôlés avant intégration, que les relations entre entités sont respectées et que les anomalies restent traçables.

La [matrice de recette](../tests/matrice-de-recette.csv) reprend les principaux cas de test sous une forme claire et structurée.

## Niveaux de test

### 1. Contrôles du fichier

Les tests valident les quatre prérequis du fichier : en-tête, pied, type de fichier et nombre de lignes.

### 2. Chargement des comptes

Les tests contrôlent les champs obligatoires et la liste des cabinets autorisés.

### 3. Chargement des clients

Les tests vérifient l’existence du compte parent et l’orientation vers les rejets lorsqu’il est absent.

### 4. Chargement des contacts

Les cas couvrent l’existence du client parent, le format minimal des emails et les cardinalités des adresses et téléphones.

### 5. Traçabilité

Les tests vérifient l’enregistrement du fichier, de la date, du statut et du motif d’erreur, ainsi que la présence de l’identifiant de fichier dans les tables métier.

## Structure d’un cas de test

Chaque cas comporte :

- un identifiant stable ;
- la règle contrôlée ;
- un scénario d’entrée ;
- le résultat attendu ;
- une priorité ;
- un statut prévu pour l’exécution.

## Cahier de recette

Le cahier de recette couvre les contrôles de fichier, l’intégrité référentielle, les rejets, la traçabilité et les flux delta. Les fichiers de test, les résultats détaillés et les preuves d’exécution ne sont pas diffusés pour des raisons de confidentialité.

## Améliorations recommandées

Une version industrialisée devrait ajouter :

- une requête ou un contrôle automatisé pour chaque cas ;
- une preuve d’exécution horodatée ;
- les volumes attendus et obtenus ;
- des tests de non-régression ;
- des tests dédiés aux flux delta et à l’idempotence ;
- une traçabilité entre règle métier, mapping technique et cas de test.
