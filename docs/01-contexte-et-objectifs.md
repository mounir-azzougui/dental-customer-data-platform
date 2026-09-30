# Contexte et objectifs

## Contexte métier

Un groupe dentaire implanté dans plusieurs villes du nord de la France souhaitait centraliser les informations de ses patients afin de faciliter leur identification, la mise à jour de leurs coordonnées et le suivi global de la base clients.

Les données étaient transmises sous la forme d’un fichier texte hiérarchique. Une même interface regroupait plusieurs types d’enregistrements : comptes, clients, emails, adresses et téléphones.

## Problématique

Le fichier source ne pouvait pas être exploité directement par les équipes métier. Il fallait :

- contrôler sa structure avant tout chargement ;
- séparer les différents types d’enregistrements ;
- appliquer les règles de cohérence et d’intégrité ;
- conserver les anomalies pour analyse ;
- tracer l’origine et le statut de chaque chargement ;
- rendre les informations consultables dans un outil de restitution.

## Objectifs du projet

Le projet devait aboutir à une chaîne data couvrant les besoins suivants :

1. modéliser une base clients relationnelle ;
2. charger un fichier d’initialisation ;
3. préparer l’intégration de flux delta réguliers ;
4. contrôler la conformité des fichiers ;
5. appliquer les règles de gestion ;
6. gérer les enregistrements rejetés ;
7. tracer les traitements et les fichiers sources ;
8. produire une restitution Power BI adaptée aux utilisateurs.

## Utilisateurs ciblés

Deux profils principaux ont été retenus :

- le front-office, qui doit retrouver rapidement un client et ses coordonnées ;
- le back-office, qui doit suivre la complétude, la répartition et la qualité globale des données.

## Mes contributions

J’ai contribué à la conception du modèle de données, à l’analyse fonctionnelle, à la formalisation des règles, à la stratégie de recette, à la coordination et à la restitution BI. J’ai également participé à certains travaux techniques d’intégration dans le cadre du fonctionnement collectif de l’équipe.
