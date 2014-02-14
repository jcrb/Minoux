Minoux
======

Projet Smur paramedicalisé dans la région de S. pour faire du TIIH + assistance Ehpad

Todo
----
- liste des Ehpad du secteur + places
- liste des commmunes concernées
- cartographie

13/02/2014
----------
Suite à notre dernière conversation, voici des chiffres dont j’aurais besoin (2013 ou à défaut 2012) :
population, ehpad,
accidentologie, mortalité,
transports secondaires au départ d’Obernai, Schirmeck et Erstein,
interventions de secours à personne par pompiers, smur et dragon
et toutes autres données que tu estimerais utiles

d’une part sur le secteur actuel du smur Sélestat
d’autre part sur le secteur Obernai (rayon de  15 km)
enfin  sur le secteur vallée de la bruche

Disposes-tu facilement de ces chiffres ou as-tu des « adresses » où je pourrai les obtenir ?
Par ailleurs, as-tu une cartographie informatisée de ces secteurs ?

14/02/2014
-----------
la "granularité" la plus fine dont je dispose est la commune (population et limites géographiques). A partir de ces 2 informations je peux construire par "agglomération" la démographie et la cartographie d'un secteur composé d'un ensemble de communes (identifiées par leur n°INSEE pour éviter les pb liés aux accents et aux noms composés). Je sais construire actuellement
- le secteur sanitaire 2
- le territoire de proximité de Sélestat (qui devrait correspondre au territoire du SMUR de Sélestat, à vérifier)
Par contre je dois construire le secteur Obernai qu'il faut que tu me définisse en terme de communes, ce qui me permet ensuite d'extraire population, cartographie, interventions SMUR, EHPAD, etc. Pour la vallée de la bruche, j'ai une définition basée sur le liste des communes. Mais c'est une liste un peu arbitraire que j'avais fixée en 2006 dans la cadre de la création d'une antenne SMUR sur le secteur. Y a t'il à ta connaissance une définition "officielle" de la vallée de la bruche ?
A titre d'illustration je te joins les fonds de cartes que l'on peut faire (territoire de proximité de Sélestat) en agglomérant des communes. On peut bien sur peupler ces fonds (couleurs, légendes). Tu peut voir sur le site de Resural une cartographie des tensions hospitalières en Alsace construite sur de principe (Activités/groupe de travail/hopital en tension).

Points particuliers
- EHPAD: je peux extraire une liste à partir du fichier FINESS (avec le nombre de lits de chaque établissement. Par contre il existe des indicateurs comme l'age moyen des résidents ou leur degré de dépendance mais je ne sais pas si cette information est facilement accessible ou pas. Je peux essayer de voir au niveau de l'ARS)
- accidentologie: il existe un registre national alimenté par les données de la police, gendarmerie et DDE. L'ccès est libre (open data) mais il faut que je voie concrètement extraire les données
- mortalité: je ne sais pas. Peut être à partir des données de l'INSEE. A explorer.
- secours à personne:je pense qu'on peut obtenir l'info du SAMU mais il serait peut être utile de la croiser avec des données du SDIS (via LT ?)
- SMUR et Dragon: ça ne devrait pas poser de pb.
