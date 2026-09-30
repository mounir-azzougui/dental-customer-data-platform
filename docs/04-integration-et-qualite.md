# Intégration et qualité des données

## Principes d’intégration

Le processus prend en charge un fichier d’initialisation et prépare le fonctionnement de flux delta. Le champ `ACTION` indique l’opération demandée :

- `C` pour créer un enregistrement ;
- `M` pour créer ou mettre à jour ;
- `S` pour supprimer.

La documentation publique illustre principalement le chargement d’initialisation et présente les règles prévues pour les créations, modifications et suppressions dans les flux delta.

## Contrôles au niveau du fichier

Un fichier est accepté uniquement si :

1. il commence par une ligne `000` ;
2. il se termine par une ligne `999` ;
3. le type de fichier est `CLIENT` ;
4. le nombre de lignes déclaré correspond au nombre réel de lignes.

Une erreur à ce niveau arrête le traitement avant l’alimentation des tables métier.

## Contrôles au niveau des entités

### Comptes

- présence des champs obligatoires ;
- code de cabinet appartenant à la liste autorisée ;
- contrôle des valeurs de statut et de type.

### Clients

- présence des identifiants obligatoires ;
- existence du compte parent ;
- conversion de la date de naissance ;
- contrôle des valeurs codifiées.

### Emails

- existence du client parent ;
- présence des caractères `@` et `.` ;
- respect du nombre maximal d’emails par client.

### Adresses

- existence du client parent ;
- contrôle des valeurs de pays et de qualité ;
- respect du nombre maximal d’adresses par client.

### Téléphones

- existence du client parent ;
- contrôle du type fixe ou portable ;
- respect d’un téléphone maximal par type ;
- contrôle du statut et de l’indicateur favori.

## Gestion des rejets

Les lignes qui échouent aux règles d’intégrité ne sont pas supprimées silencieusement. Elles sont orientées vers une table de rejet associée à leur entité.

Cette approche permet :

- de mesurer la qualité des données reçues ;
- d’identifier les règles les plus fréquemment enfreintes ;
- de corriger les données sans perdre l’information source ;
- de justifier les différences entre le volume reçu et le volume intégré.

## Traçabilité

Le processus conserve le nom du fichier, la date d’exécution et le statut du chargement. L’identifiant du fichier est propagé dans les tables afin de relier chaque enregistrement à son origine.

## Évolutions possibles

Une évolution pourrait ajouter :

- un catalogue centralisé des motifs de rejet ;
- des contrôles de format plus robustes pour les emails et téléphones ;
- des indicateurs de qualité historisés ;
- des traitements idempotents ;
- des tests automatisés sur les actions `C`, `M` et `S` ;
- une séparation explicite entre dates de création et de modification.
