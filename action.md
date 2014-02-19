Etapes projet Minoux
========================================================

Zone de proximité de Sélestat
-----------------------------

Il faut récupérer le fichier *base.Rda*

Variables:
- base: résultat de la lecture de carto_alsace.Rda: dataframe de 904 lignes correspondant auc communes d'Alsace et 31 colonnes correspondant aux caractéristiques de chaque commune


```r
load("../RPU_2013/doc/cartographie/RPU2013_Carto_Pop/base.Rda")
zp_selestat <- base[base$zone_proximite == "7", "ville_nom"]
write.table(zp_selestat, file = "zp_selestat.csv", sep = ",")
```



Création de la zone Obernai (zo)
--------------------------------

Fichiers nécessaires:
- carto_alsace.rda
- secteur_Obernai.csv

Variables:
- als: résultat de la lecture de **carto_alsace.Rda**: SpatiialPolygon contenant
  - les limites géographiques de chaque commune d'Alsace
  - un dataframe *als@data* contenant les caractéritiques IGN de ces communes
- zpo: dataframe des 29 communes du secteur d'Obernai et 6 colonnes dont le dode INSEE de chaque commune. Le fichier a été construit à partir de la liste de JMM croisée avec la iste des communes d'Alsace de wikipedia (cf Readme)
- zpob: vecteur correspondant à la colonne code_INSEE de zpo
- zp1: sous-ensemble de *als* obtenu en croisant *als* et *zpob* au travers de la méthode %in%. On obtient un *SpatiialPolygon* limités aux 29 communes du secteur d'Obernai. On sauvegarde ce fichier sous le nom de **zp_obernai.Rda**, correspondant au fond de carte du secteur.


```r
library("maptools")
```

```
## Loading required package: foreign
## Loading required package: sp
## Loading required package: grid
## Loading required package: lattice
## Checking rgeos availability: TRUE
```

```r
source("../copyright.R")
load("../RPU_2013/doc/cartographie/carto_alsace.rda")

zpo <- read.table("secteur_Obernai.csv", header = T, sep = ",")

zpob <- zpo$Code.Insee

zp1 <- als[als@data$INSEE_COM %in% zpob, ]
save(zp1, file = "zp_obernai.Rda")
# load('zp_obernai.Rda')
names(zp1)
```

```
##  [1] "ID_GEOFLA"  "CODE_COMM"  "INSEE_COM"  "NOM_COMM"   "STATUT"    
##  [6] "X_CHF_LIEU" "Y_CHF_LIEU" "X_CENTROID" "Y_CENTROID" "Z_MOYEN"   
## [11] "SUPERFICIE" "POPULATION" "CODE_CANT"  "CODE_ARR"   "CODE_DEPT" 
## [16] "NOM_DEPT"   "CODE_REG"   "NOM_REGION"
```

```r
plot(zp1)

# affichage de la commune d'Obernai
a <- zp1@data
obernai <- a[a$NOM_COMM == "OBERNAI", ]
x <- obernai$X_CHF_LIEU * 100
y <- obernai$Y_CHF_LIEU * 100
nom <- obernai$NOM_COMM
points(x, y, pch = 19, col = "red")
text(x, y, labels = nom, pos = 3, cex = 0.8)
copyright()
```

![plot of chunk zo](figure/zo1.png) 

```r

# Affichage du nom de toutes les communes
plot(zp1)
x <- a$X_CHF_LIEU * 100
y <- a$Y_CHF_LIEU * 100
points(x, y, pch = 19, col = "red")
nom <- a$NOM_COMM
text(x, y, labels = nom, pos = 3, cex = 0.6)
copyright()
```

![plot of chunk zo](figure/zo2.png) 

```r

# formation d'une région par fusion des polygones
contour <- unionSpatialPolygons(zp1, IDs = zp1@data$NOM_DEPT)
```

```
## Loading required package: rgeos
## rgeos version: 0.3-2, (SVN revision 413M)
##  GEOS runtime version: 3.3.3-CAPI-1.7.4 
##  Polygon checking: TRUE
```

```r
plot(contour, col = "khaki")
x <- a$X_CHF_LIEU * 100
y <- a$Y_CHF_LIEU * 100
points(x, y, pch = 19, col = "red")
nom <- a$NOM_COMM
text(x, y, labels = nom, pos = 3, cex = 0.6)
copyright()
```

![plot of chunk zo](figure/zo3.png) 



