# Automatisation-analyse-des-op-rations-de-transactions-OM

## Objectif

Ce projet a pour objectifs de:

- Identifier toutes les opérations d'annulation faites sur OM
- Identfier les auteurs et leurs droits (fiabilisation)
- s’assurer que toutes les opérations de reset de code ont été effectuées 48h après un CA  (anti fraude)
- s’assurer que toutes les opérations d’annulation OM ont été effectuées 48h après un CA  (anti fraude)
- s’assurer que toutes les opérations d’ annulation OM sur les numéros des clients se font sur demande formelle des clients.


[Voir rapport complet](https://github.com/Smben-Mlk/Automatisation-analyse-des-op-rations-de-transactions-OM/blob/main/RAPPORT%20CONTR%C3%94LE%20DES%20OP%C3%89RATIONS%20DE%20CA%20SUIVI%20DE%20RESET%20PIN%20ET%20ANNULATION%20DES%20TRANSACTIONS%20OM.pdf)

## Outils

- Python (pandas numpy matplolib)

- Power BI

- Excel

## Compétences

- analyse de logs
- Deep learning
- Machine learning
- automatisation
- Analyse de données
- Netoyage de données
- aggrégation de données
- corrélation de données

## Dataset

## Inputs

 Logs tango 
contient les reset pin effectuées sur tango
			format: fichier texte (.csv)
			période de couverture: du vendredi au jeudi (7 jours )
- Log BO360 
contient les reset pin et annulations effectuées sur BO360)
			format: fichier texte (.csv)
			période de couverture: du vendredi au jeudi (7 jours )
- Export Kibaru 
contient toutes les signalisations relatifs au reset pin
			format: fichier excel (.xlsx)
			période de couverture: du lundi au dimanche (7 jours )
- Logs CA 
contient les CA
			format: fichier excel (.xlsx)
			période de couverture: à filtrer (voir annexe)
- Login (contient tous les utilisateurs SI et leurs structures respectives)
		format: fichier excel (.xlsx)
			à fiabiliser au besoin

## Outputs

- CONTROLE ANNULATION(.xlsx)
feuille 1
Contient toutes les annulations effectuées au sein de la DESC et leurs cases respectives.

feuille 2 (A JUSTIFS)
Contient toutes les annulations DESC sans cases (à chercher manuellement).

feuille 3 (CA ANNUL)
Contient toutes les annulations DESC précédées d’un CA .

Nous nous sommes servi de la bibliothèque time de python pour créer la colonne temps de différence où est calculée le délais:
- SI < 48h , CONSTAT = NOK
- SINON , CONSTAT = OK

feuille 4 (TCD)

- CARESET(.xlsx)
feuille 1
Contient tous les CA suivis de reset pin effectués dans la période.
feuille 2
Contient tous les CA suivis de reset pin effectués au sein de la DESC.


## Approche d'analyse

Les grandes lignes de la méthodologie adoptée dans le script python careset.py sont:
- Lire, vérifier et joindre tous les logs tango 
- Concaténer avec les logs tango et les logs BO360
- Filtrage sur RÉINITIALISATION /DÉBLOCAGE RÉINITIALISATION
- Corrélation avec des reset pin avec le login par le biais de la colonne email
- Croisement des reset pin avec les CA
- Filtrage DESC
- Corrélation avec des annulations avec le login par le biais de la colonne email
- Corrélation des annulations avec l’export Kibaru par le biais du ND
- Filtrage des opérations sans case
- Croisement des annulations  avec les CA
- Vérification du délais 48H
- Elaboration TCD pour besoin du rapport



