# Architecture data

## Vue générale

L’architecture sépare l’acquisition, la préparation, l’intégration et la restitution. Cette organisation évite de transformer directement le fichier source dans les tables finales et permet de conserver une trace des anomalies.

![Architecture du pipeline](../assets/architecture-pipeline.svg)

## 1. Fichier source

Le fichier `F_CLIENT_*.txt` est un flux multi-format délimité par `|`. Le premier champ de chaque ligne détermine l’entité concernée.

Les enregistrements `000` et `999` encadrent obligatoirement le fichier. Les autres enregistrements sont facultatifs et portent les données métier.

## 2. Zone d’acquisition

La table `ACQ` reçoit les lignes du fichier dans une structure générique. Elle comporte les champs nécessaires pour conserver les différentes positions du flux, ainsi que le nom du fichier et un identifiant de ligne.

Cette couche sert à exécuter les contrôles de fichier avant toute intégration dans les tables métier.

## 3. Contrôle du fichier

Le processus vérifie :

- la présence de l’en-tête `000` ;
- la présence du pied `999` ;
- la valeur `CLIENT` dans l’en-tête ;
- la concordance entre le compteur final et le nombre réel de lignes.

Un fichier non conforme est tracé dans la table de suivi et n’alimente pas les couches suivantes.

## 4. Zone SAS

Les lignes conformes sont réparties selon leur code dans cinq tables de préparation :

- `SAS_COMPTE` ;
- `SAS_CLIENT` ;
- `SAS_EMAIL` ;
- `SAS_ADRESSE` ;
- `SAS_TELEPHONE`.

Les champs de cette couche restent principalement textuels afin de faciliter les contrôles et les conversions avant chargement dans Oracle.

## 5. Zone DWH

Les données sont intégrées dans l’ordre imposé par les relations :

1. comptes ;
2. clients ;
3. emails, adresses et téléphones.

Les tables DWH utilisent des types adaptés aux données et appliquent les contraintes fonctionnelles. Les lignes non conformes sont redirigées vers les tables de rejet correspondantes.

## 6. Restitution

Power BI se connecte aux tables Oracle via ODBC. La couche de restitution applique les derniers ajustements de format, charge la table de transcodification et construit les relations nécessaires aux rapports.

## Explication du modèle

Le modèle organise les comptes, les clients et leurs coordonnées dans des tables reliées par des clés primaires et étrangères.

Un compte peut regrouper plusieurs clients. Chaque client peut ensuite être associé à un email, une adresse et jusqu’à deux téléphones. Cette organisation garantit la cohérence des relations, limite la duplication des informations et facilite les contrôles de qualité.
