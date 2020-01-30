# DATABSE dataia_Nancy

## Table structure for table questionresponses



| Column         		|     Type	        					| Null | Default | Links to | Comments | Media (MIME) type |
|:---------------------:|:--------------------------------:|:----------:|:-------:|:---------:|:----------:|:----------:|
| questions         	| text| No                             |      |  |   |   | 
| reponse         		| text| No                             |      |  |   |   | 
| id         		    | text| No                             |      |  |   |   | 


## Dumping data for table questionsreponses

| questions         		|     reponses	        					| id |
|:---------------------:|:--------------------------------:|:-----------:|
| Selectionner les 10 premières lignes de la table         	| SELECT * FROM dataia_Nancy LIMIT 10;| 1 |
| Combien d’individus avons-nous dans la table         	| SELECT COUNT(*) FROM sinistre;| 2 |
| Combien d’individus distincts avons-nous dans la table | | 3 |
| Recoder la variable resilies sachant que 0 correspond à non resiliés et 1 à résilies| SELECT CASE WHEN resilies=1 THEN 'resilies' ELSE 'non resilies' END AS STATUS FROM dataia_Nancy;| 4 |
| Combien de non resiliés avons-nous          	| SELECT COUNT(CASE WHEN resilies=0 THEN 'resilies' ELSE 'non resilies' END) AS STATUS FROM dataia_Nancy WHERE resilies=1;| 5 |
| Quelle est l’ancienneté moyenne des individus avec en décimal, 0 chiffre         	| SELECT ROUND(AVG(anciennete)) AS moyenne FROM dataia_Nancy;| 6 |
| Afficher le nombre d’individus en fonction de l’ancienneté et du sinistre ; interprétez| SELECT anciennete, ROUND(AVG(anciennete)) AS moyenne_anciennete FROM dataia_Nancy GROUP BY anciennete;| 7 |
|Afficher le nombre d’individus en pourcentage en fonction de l’ancienneté et du sinistre ; interprétez | SELECT anciennete, ROUND((COUNT(*) / SUM(anciennete)) * 100) AS pourcentage_anciennete, ROUND((COUNT(*) / sum(sinistre)) * 100) AS pourcetage_sinistre, ROUND((COUNT(*) / sum(anciennete+sinistre) * 100), 2) AS pourcetage_total FROM dataia_Nancy GROUP BY anciennete;| 8 |
|Parmi les non resilie, combien d'individus ont un sinistre superieur a la moyenne general |SELECT COUNT(resilies) AS personne_total, ROUND(AVG(sinistre)) AS moyenne_general FROM dataia_Nancy WHERE (SELECT AVG(sinistre) WHERE resilies = 0) > (SELECT COUNT(sinistre)); | 9|
|Cree en une seule requete la table projetA contenant les variables: resilies, parcours, anciennete et demenagement|CREATE TABLE projectA AS SELECT resilies, parcours, anciennete, demenagement FROM dataia_Nancy;| 10|
|Creer aussi en une seule requete la table "projetB contenant les variables: resilies, parcours, sinistre, devis, revisions et satisfaction"|CREATE TABLE projectB AS SELECT resilies, parcours, sinistre, devis, revision, satisfaction FROM dataia_Nancy;|11|
|Créer la table projetC à partir des tables projetA et projetB en utilisant dans un premier temps un « join » et dans un deuxieme temps « with »|1) ALTER TABLE projectA ADD id INT(11) PRIMARY KEY AUTO_INCREMENT; 2)ALTER TABLE projectB ADD id INT(11) PRIMARY KEY AUTO_INCREMENT; 3)CREATE TABLE projectC AS SELECT projectA.resilies, projectA.parcours, projectA.anciennete, projectA.demenagement, projectB.sinistre, projectB.devis, projectB.revision, projectB.satisfaction FROM projectA INNER JOIN projectB ON projectA.id = projectB.id;| 12|
