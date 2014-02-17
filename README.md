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

Sources de données
==================

Acccidents
----------

date extration de la base: 14/02/2014
source: http://www.data.gouv.fr/fr/dataset/base-de-donnees-accidents-corporels-de-la-circulation-sur-6-annees

Cette base est extraite du fichier national des accidents corporels de la circulation, dit « Fichier BAAC1 », administré par l’Observatoire interministériel de la sécurité routière. Pour chaque accident corporel (soit un accident survenu sur une voie ouverte à la circulation publique, impliquant au moins un véhicule et ayant fait au moins une victime ayant nécessité des soins), les saisies d’information sont effectuées par l’unité des forces de l’ordre (police, gendarmerie, etc.) qui est intervenue sur le lieu de l’accident. La base répertorie l'intégralité des accidents corporels de la circulation intervenus de 2006 à 2011 en France (4 DOM inclus, à savoir Guadeloupe, Guyane, Martinique et La Réunion), avec leur description simplifiée (plus un indice de gravité – défini plus loin). Cela inclue toutes les informations de localisation disponibles dans le Fichier BAAC, telles qu’elles y sont renseignées ainsi que les informations concernant les véhicules et leurs victimes.

Cette base comporte 454 372 accidents (440 695 pour la métropole et 13 677 pour les DOM) et 775 422 véhicules présents dans les accidents (751 831 pour la métropole et 23 591 pour les DOM).

Elle est notablement plus détaillée que la base de données 2005-2010 postée précédemment sur Etalab (à l’automne 2011). 

17/02/2014
==========
- vallée de la bruche in [wikipédia](http://fr.wikipedia.org/wiki/Communaut%C3%A9_de_communes_de_la_Vall%C3%A9e_de_la_Bruche). Tableau avec la liste des communes à récupérer
- projet VL médicalisée (JCB) dans un mail pour Schiber -> copie JMM
- liste des communes du Smur de Sélestat
- secteur d'Obernai: pas de définition officielle. Listes des communes établies par JMM:
Altorf
Avolsheim
Bernardswiller
Bischoffsheim
Boersch
Dangolsheim
Dinsheim
Dorlisheim
Duttlenheim
Flexbourg
Goxwiller
Gresswiller
Griesheim-près-Molsheim
Heiligenberg
Heiligenstein
Hernolsheim
Innenheim
Klingenthal
Krautergersheim
Laubenheim
Meistratzheim
Mollkirch
Molsheim
Mutzig
Niedernai
Obernai
Ottrott
Rosenwiller
Rosheim
Saint-Nabor
Valff

corrections:
- Boersch -< Bœrsch
- Dinsheim -> Dinsheim-sur-Bruche
- Hernolsheim -> Ernolsheim-Bruche
- Klingenthal -> Bœrsch
- Laubenheim -> Mollkirch

library("XML")
library("knitr")

cla <- readHTMLTable("http://fr.wikipedia.org/wiki/Liste_des_communes_du_Bas-Rhin", stringsAsFactors = FALSE)
br <- cla[[1]]
cc <- c("Altorf","Avolsheim","Bernardswiller","Bischoffsheim","Bœrsch","Dangolsheim","Dinsheim-sur-Bruche","Dorlisheim","Duttlenheim","Flexbourg","Goxwiller","Gresswiller","Griesheim-près-Molsheim","Heiligenberg","Heiligenstein","Ernolsheim-Bruche","Innenheim","Krautergersheim","Meistratzheim","Mollkirch","Molsheim","Mutzig","Niedernai","Obernai","Ottrott","Rosenwiller","Rosheim","Saint-Nabor","Valff")

cc <- as.data.frame(cc)

a <- merge(cc,br, all.x = TRUE, by.x = 1, by.y = 3)
so <- a
write.table(so, file = "secteur_Obernai.csv", sep=",")
# a <- toupper(cc[,1])

- faire la liste des communautés de communes du secteur

Voici donc quelques précisions :

- Peux-tu m’adresser le listing des commune du « territoire de proximité de Sélestat » pour m’assurer qu’il corresponde au secteur du SMUR ou le cas échéant le compléter  
- Secteur d’Obernai : ci-joint une liste un peu arbitraire ; dis-moi ce que tu en penses si tu le mets sur une carte
- Secteur Vallée de la Bruche : je n’ai pas connaissance de définition officielle, je prendrai donc le listing « bartier »
- ehpad : le nombre de lits sera suffisant, inutile d’aller dans plus de détails
- Accidentologie et mortalité : critères secondaires

