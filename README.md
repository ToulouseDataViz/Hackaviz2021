
<!-- author: "C.R, Vincent VIVANLOC" -->

<!-- date: "August 2021" -->

<!-- README.md is generated from README.Rmd. Please edit that file -->

<!-- command : markdown::render("/home/nop/dev/tdv_asso/Hackaviz2021prepa/README.Rmd", encoding = "UTF-8","all") -->

# Hackaviz 2021 : quartiers prioritaires (QP) d’Occitanie : caractéristiques et transactions immobilières.

![14 avril 2011, un immeuble en train d’être repeint à Empalot.
Olybrius, [Wikimedia
Commons](https://commons.wikimedia.org/wiki/File:Toulouse_-_Rue_des_Mouettes_-20110414_\(2\).jpg)](images/Toulouse_Rue_des_Mouettes_20110414.jpg)

Cette année, nous proposons dans un jeu de données inédit :

  - les caractéristiques démographiques et économiques des quartiers
    prioritaires
  - les transactions foncières du 1er janvier 2016 au 31 décembre 2020.
  - les contours géographiques des communes et des quartiers
    prioritaires

Ce jeu de données est réparti sur trois fichiers. Il est possible de
faire de belles visualisations à partir d’un seul de ces fichiers. Vous
pouvez aussi les combiner, mais il n’est pas certain que la plus belle
histoire ait besoin de toutes ces données.

Ces données sont extraites de sources pour lesquelles certaines valeurs
ne sont pas renseignées. Avant de vous lancer dans des calculs
d’indicateurs statistiques, pensez à examiner la qualité des données
et le nombre d’échantillons considérés \!

N’hésitez pas à nous contacter sur le
[discord](https://discord.com/invite/RbTR4jKRp9) du Toulouse DataViz
pour discuter entre participants, si vous avez besoin d’aide à propos
des données ou pour rapporter des bugs.

Bonne chance \!

# Description générale des données

Ces données sont disponibles sous forme de 4 fichiers, déclinés sous
forme de données tabulaires au format
[`.csv`](https://fr.wikipedia.org/wiki/Comma-separated_values) et
géographique au format
[`.geojson`](https://fr.wikipedia.org/wiki/GeoJSON).

| Fichier de données                                                                                   | Contenu                                                         |
| ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| [`qp.csv`](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/data/qp.csv)                     | caractéristiques des 105 quartiers prioritaires d’Occitanie     |
| [`foncier_qp.csv`](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/data/foncier_qp.csv)     | transactions immobilières dans ces quartiers entre 2016 et 2020 |
| [`communes.geojson`](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/data/communes.geojson) | contour géographique des communes d’Occitanie                   |
| [`qp.geojson`](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/data/qp.geojson)             | contour géographique des quartiers de ces communes              |

Une archive (`.zip`) est aussi disponible pour
[télécharger](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/data/data.zip)
toutes les données.

## Format de fichiers CSV

  - Les fichiers sont encodés en UTF-8.
  - Les fichiers `csv` utilisent le séparateur de colonne “`,`” et le
    caractère décimal “`.`”.
  - Ces `csv` ont été exportés depuis à un paramètre régional anglais.
    Pensez à modifier les paramètres d’import de votre logiciel préféré
    \!
  - Si vous avez des difficultés à importer ces `csv`, nous vous
    proposons une alternative sous forme de fichier Microsoft Excel.

## Format de fichiers JSON

  - Les latitudes et longitudes sont exprimées dans la projection `World
    Geodetic System 1984` (WGS 84).
  - Elles sont tronquées sur 4 décimales.

## Jointures

  - Nous avons pris le soin d’unifier les noms de colonnes des
    différents fichiers afin que vous puissiez faire des
    [jointures](https://fr.wikipedia.org/wiki/Jointure_\(informatique\)).
  - Vous n’avez aucune obligation à fusionner ces fichiers : pensez
    d’abord à l’histoire que vous voulez raconter \!
  - Pour joindre deux `csv`, vous pouvez utiliser un modèle
    [ObservableHQ](https://ressources.toulouse-dataviz.fr/newsletter--toulouse-dataviz-15--spcial-hackaviz-2021),
    des librairies comme [Pandas](https://pandas.pydata.org/) ou le
    coder directement.
  - Pour fusionner des données géographiques `geojson` et un `csv`, si
    vous ne connaissez pas QGIS ou R, nous vous suggérons [Geo Data
    Merger](https://funkeinteraktiv.github.io/geo-data-merger/) qui vous
    permet de faire cela via une interface graphique simple.
    Sélectionnez un fichier `geojson` puis un `csv` qui va venir
    enrichir le geojson. Désignez ensuite une colonne “clé” sur les 2
    fichiers pour faire la jointure.

## Format des valeurs

  - Les codes de départements et de communes ont été formattés
    respectivement sur 2 et 5 caractères conformément au [code officiel
    géographique](https://fr.wikipedia.org/wiki/Code_officiel_géographique).
  - Les codes de quartiers sont formés par le préfixe “QP” et 6
    chiffres.
  - Les dates sont au format ISO-8601 (YYYY-MM-DD) ex: `2020-12-31`.
  - Les valeurs foncières sont exprimées en euros.
  - Les surfaces sont en mètres carrés.

# Description détaillée des données

## Description du fichier `qp.csv`

Caractéristiques démographiques et économiques des quartiers
prioritaires d’Occitanie

  - Définitions
    
      - Quartier prioritaire (QPV) de la politique de la ville :
        territoires en difficulté, cibles prioritaires de la [politique
        de la
        ville](https://www.cohesion-territoires.gouv.fr/quartiers-de-la-politique-de-la-ville),
        définis par la part de la population ayant un revenu inférieur à
        11 250 € par an.
    
      - Communes englobantes : pour un quartier prioritaire, l’unité
        urbaine (une ou plusieurs communes) à laquelle le quartier
        appartient.
    
      - Population municipale : comprend les personnes ayant leur
        résidence habituelle sur le territoire de la commune, dans un
        logement ou une communauté; détenues dans les établissements
        pénitentiaires de la commune ; les sans-abri recensées sur le
        territoire de la commune ; résidant habituellement dans une
        habitation mobile recensée sur le territoire de la commune.
    
      - Population étrangère : toute personne résidant en France qui n’a
        pas la nationalité française.
    
      - Taux parmi la population : taux calculé par rapport à la
        population municipale.
    
      - Taux de pauvreté au seuil de 60% : part de la population sous le
        seuil de 60% du [niveau de vie
        médian](https://www.insee.fr/fr/statistiques/4797606?sommaire=4928952)
        métropolitain. Les revenus sont calculés depuis les revenus
        fiscaux.
    
      - Taux de bas revenus : part de la population sous le seuil de 60
        % du revenu déclaré par unité de consommation médian
        métropolitain. Les revenus sont issus des fichiers de la CAF.
        En savoir plus sur la différence entre le taux de pauvrété et de
        bas revenu : [DOSSIER D’ETUDE N° 107 Août 2008 CAF,
        pp24-25](https://www.caf.fr/sites/default/files/cnaf/Documents/Dser/dossier_etudes/Dossier%20107%20-%20Basrevenus.pdf).
    
      - Emploi précaire : contrat d’apprentissage, placé par une agence
        d’intérim, emplois-jeunes, CES, contrats de qualification,
        stagiaires rémunérés en entreprise, autres emplois à durée
        limitée

  - Note sur la source des données
    
      - Le comptage de la population municipale (colonne ‘pop\_com’) est
        une estimation de l’Insee et de la Caisse nationale des
        allocations familiales ([Cnaf](http://data.caf.fr/site/)) en
        2015. Ces valeurs diffèrent de celles du recensement INSEE
        effectué en 2016.
      - Les données sont calculées pour la période 2015-2020. Elles ont
        été publiées par l’INSEE pour l’année 2019, sauf pour les
        données concernant l’insertion professionnelle. Pour ces
        dernières, l’année 2020 est considérée, le fichier de l’année
        2019 étant corrompu.

Cette description est disponible sous forme de fichier `.csv`
[meta\_qp.csv](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/meta/meta_qp.csv).

| colonne         | description                                                                                                                   | type\_valeur         | exemple      |
| :-------------- | :---------------------------------------------------------------------------------------------------------------------------- | :------------------- | :----------- |
| code\_qp        | Code du quartier prioritaire                                                                                                  | chaîne de caractères | QP082003     |
| nom\_qp         | Libellé du quartier prioritaire                                                                                               | chaîne de caractères | Centre Ville |
| nom\_commune    | Libellé géographique de la (des) commune(s) englobante(s)                                                                     | chaîne de caractères | Moissac      |
| pop\_mun        | Population municipale du quartier prioritaire                                                                                 | entier               | 2470         |
| pop\_com\_qp    | Cumul de la population municipale de tous les quartiers prioritaires de la (des) commune(s) englobante(s)                     | entier               | 3672         |
| pop\_com        | Population municipale de la (des) commune(s) englobante(s)                                                                    | entier               | 12564        |
| ind\_jeune      | Indice de jeunesse : population de 0 à 19 ans / population de 60 ans et plus                                                  | nombre rationnel     | 0.9          |
| tx\_tot\_et     | Part des étrangers parmi la population                                                                                        | nombre rationnel     | 25.4         |
| tx\_f           | Part des femmes parmi la population                                                                                           | nombre rationnel     | 50.6         |
| tx\_f\_et       | Part des étrangères parmi les femmes                                                                                          | nombre rationnel     | 22.8         |
| percou          | Nombre de personnes couvertes par au moins une prestation CAF (allocataire + conjoint + enfants et autres personnes à charge) | entier               | 1307         |
| pmimp           | Part des ménages imposés                                                                                                      | nombre rationnel     | 24.7         |
| part\_chomprinc | Part des ménages dont l’origine principale du revenu déclaré repose sur des indemnités de chômage                             | nombre rationnel     | 8.1          |
| decuc\_q2       | Médiane (en euros) du revenu déclaré par unité de consommation                                                                | entier               | 10136        |
| decuc\_d1       | Premier décile du revenu déclaré par unité de consommation                                                                    | entier               | 1404         |
| decuc\_d9       | Neuvième décile du revenu déclaré par unité de consommation                                                                   | entier               | 26388        |
| disp\_q2        | Médiane (en euros) du revenu disponible par unité de consommation                                                             | entier               | 13305        |
| disp\_d1        | Premier décile (en euros) du revenu disponible par unité de consommation                                                      | entier               | 6421         |
| disp\_d9        | Neuvième décile (en euros) du revenu disponible par unité de consommation                                                     | entier               | 25058        |
| tp60            | Taux de pauvreté                                                                                                              | nombre rationnel     | 43.9         |
| brev            | Taux de bas revenus                                                                                                           | nombre rationnel     | 59.1         |
| a               | Nombre total de foyers allocataires percevant au moins une prestation CAF                                                     | entier               | 642          |
| tx\_tot\_empl   | Part des personnes de 15 à 64 ans actives ayant un emploi parmi les personnes de 15 à 64 ans                                  | nombre rationnel     | 47.5         |
| tx\_f\_empl     | Part des femmes de 15 à 64 ans actives ayant un emploi parmi les femmes de 15 à 64 ans                                        | nombre rationnel     | 41           |
| tx\_et\_empl    | Part des étrangers de 15 à 64 actifs ayant un emploi parmi les étrangers de 15 à 64 ans                                       | nombre rationnel     | 36.7         |
| tx\_tot\_eprec  | Part des personnes en emploi précaire parmi les personnes ayant un emploi.                                                    | nombre rationnel     | 34.4         |
| tx\_f\_eprec    | Part des femmes en emploi précaire parmi les femmes ayant un emploi.                                                          | nombre rationnel     | 31.9         |
| tx\_et\_eprec   | Part des étrangers en emploi précaire parmi les étrangers ayant un emploi.                                                    | nombre rationnel     | 59.3         |
| abcde           | Nombre total de demandeurs d’emploi en fin de mois                                                                            | entier               | 774          |
| abcde\_f        | Nombre total de demandeurs d’emploi femmes                                                                                    | entier               | 327          |
| abcde\_h        | Nombre total de demandeurs d’emploi hommes                                                                                    | entier               | 447          |
| abc\_capbep     | Nombre de demandeurs d’emploi de catégorie A, B ou C de niveau de formation CAP-BEP                                           | entier               | 187          |
| abc\_bac        | Nombre de demandeurs d’emploi de catégorie A, B ou C de niveau de formation BAC                                               | entier               | 111          |
| abc\_supbac     | Nombre de demandeurs d’emploi de catégorie A, B ou C de niveau de formation supérieur au BAC                                  | entier               | 64           |
| ec\_mat         | Nombre d’écoles maternelles à moins de 100m du QP                                                                             | entier               | 1            |
| ec\_elem        | Nombre d’écoles élémentaires à moins de 100m du QP                                                                            | entier               | 2            |
| ec\_elem\_pri   | Nombre d’écoles élémentaires privées à moins de 100m du QP                                                                    | entier               | 1            |
| coll            | Nombre de collèges à moins de 300m du QP                                                                                      | entier               | 2            |
| coll\_pri       | Nombre de collèges privés à moins de 300m du QP                                                                               | entier               | 1            |
| nbetab          | Nombre d’établissements                                                                                                       | entier               | 282          |
| ens\_sante      | Nombre d’établissements de service aux particuliers : enseignement, santé et action sociale                                   | entier               | 37           |
| serv\_par       | Nombre d’établissements de service aux particuliers                                                                           | entier               | 72           |
| serv\_tot       | Nombre d’établissements de service : services aux entreprise et services aux particuliers                                     | entier               | 137          |
| auto\_ent       | Nombre d’auto-entrepreneurs parmi les créations d’établissements                                                              | entier               | 3            |

## Description du fichier `foncier_qp.csv`

Transactions foncières du 1er janvier 2016 au 31 décembre 2020

  - Afin de simplifier les données, nous n’avons conservé que les
    transactions sur les maisons, les appartements et les locaux
    industriels. Les dépendances ainsi que les transactions de terrains
    non bâtis ont été supprimées.
  - Ce fichier contient des transactions entre particuliers mais aussi
    celles effectuées par des investisseurs privés (groupe immobilier)
    ou institutionnels (office du logement). Selon l’histoire que vous
    voulez raconter, c’est à vous de trouver un moyen de différencier ou
    d’éliminer des transactions.

Cette description est disponible sous forme de fichier `.csv`
[meta\_foncier\_qp.csv](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/meta/meta_foncier_qp.csv).

| colonne                     | description                                  | type\_valeur         | exemple        |
| :-------------------------- | :------------------------------------------- | :------------------- | :------------- |
| code\_departement           | Code département INSEE                       | chaîne de caractères | 09             |
| nom\_departement            | Nom du département                           | chaîne de caractères | Ariège         |
| code\_commune               | Code commune INSEE                           | chaîne de caractères | 09261          |
| nom\_commune                | Nom de la commune                            | chaîne de caractères | Saint-Girons   |
| code\_qp                    | Code du quartier prioritaire                 | chaîne de caractères | QP009001       |
| nom\_qp                     | Libellé du quartier prioritaire              | chaîne de caractères | Coeur De Ville |
| id\_mutation                | Identifiant de vente                         | chaîne de caractères | 2019-100563    |
| id\_parcelle                | Identifiant de parcelle (14 caractères)      | chaîne de caractères | 092610000D0167 |
| longitude                   | Longitude du centre de la parcelle concernée | nombre rationnel     | 1.14377        |
| latitude                    | Latitude du centre de la parcelle concernée  | nombre rationnel     | 42.98314       |
| nombre\_lot                 | Nombre de lots                               | entier               | 0              |
| date\_mutation              | Date de la vente                             | date                 | 2019-11-25     |
| jour\_mutation              | Jour de la vente                             | chaîne de caractères | 25             |
| mois\_mutation              | Mois de la vente                             | chaîne de caractères | 11             |
| annee\_mutation             | Année de la vente                            | chaîne de caractères | 2019           |
| nature\_mutation            | Type de mutation                             | chaîne de caractères | Vente          |
| valeur\_fonciere            | Valeur foncière                              | entier               | 85000          |
| code\_type                  | Code de type de local                        | chaîne de caractères | 1              |
| type\_local                 | Libellé du type de local                     | chaîne de caractères | Maison         |
| surface\_reelle\_bati       | Surface réelle du bâti                       | entier               | 75             |
| nombre\_pieces\_principales | Nombre de pièces principales                 | entier               | 4              |
| surface\_terrain            | Surface du terrain                           | entier               | 60             |

## Description du fichier `communes.geojson`

Contour des communes

Cette description est disponible sous forme de fichier `.csv`
[meta\_communes.csv](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/meta/meta_communes.csv).

| nom colonne       | description            | type\_valeur         | exemple   |
| :---------------- | :--------------------- | :------------------- | :-------- |
| code\_commune     | Code commune INSEE     | chaîne de caractères | 81021     |
| code\_departement | Code département INSEE | chaîne de caractères | 81        |
| nom\_commune      | Nom de la commune      | chaîne de caractères | Aussillon |

## Description du fichier `qp.geojson`

Contour des quartiers prioritaires

Cette description est disponible sous forme de fichier `.csv`
[meta\_contours\_qp.csv](https://github.com/ToulouseDataViz/Hackaviz2021/raw/main/meta/meta_contours_qp.csv).

| nom colonne       | description                        | type\_valeur         | exemple                |
| :---------------- | :--------------------------------- | :------------------- | :--------------------- |
| code\_qp          | Code du quartier prioritaire       | chaîne de caractères | QP066007               |
| nom\_qp           | Nom du quartier prioritaire        | chaîne de caractères | Bas-Vernet Nouveau QPV |
| commune\_qp       | Nom de la commune principale du QP | chaîne de caractères | Perpignan              |
| code\_commune     | Code commune INSEE                 | chaîne de caractères | 66136                  |
| nom\_commune      | Nom de ou des communes englobantes | chaîne de caractères | Perpignan              |
| code\_departement | Code département INSEE             | chaîne de caractères | 66                     |

# Sources des données

  - Caractéristiques des quartiers prioritaires: données produites par
    l’INSEE,
    [démographie 2015](https://www.insee.fr/fr/statistiques/5359592) et
    [revenus 2017](https://www.insee.fr/fr/statistiques/5359605).
  - Transactions foncières: données publiées et produites par la
    direction générale des finances publiques. Ces données énumèrent les
    transactions intervenues au cours des cinq dernières années sur le
    territoire métropolitain et les DOM-TOM, à l’exception de l’Alsace,
    de la Moselle et de Mayotte. Les données contenues sont issues des
    actes notariés et des informations cadastrales. Les données brutes
    sont disponibles
    [ici](https://www.data.gouv.fr/fr/datasets/demandes-de-valeurs-foncieres-geolocalisees/).
    Elles peuvent être explorées par l’[application
    Etalab](https://www.data.gouv.fr/fr/datasets/demandes-de-valeurs-foncieres-geolocalisees/).
  - Liste des communes: liste publiée par l’INSEE
    [ici](https://www.insee.fr/fr/information/4316069).
  - Contours des quartiers prioritaires: fichier
    [`.shapefile`](https://fr.wikipedia.org/wiki/Shapefile) est
    disponible
    [ici](https://www.data.gouv.fr/fr/datasets/quartiers-prioritaires-de-la-politique-de-la-ville-qpv/).

# Historique des versions

  - Juin 2021: construction du jeu de données avec Python, Pandas et
    jupyter-lab et création des fichiers
  - Juillet 2021: première version de la consolidation des fichiers sous
    R et Rstudio et étude autour d’aggrégats
  - Août 2021: consolidation des fichiers et génération du readme sous R
    et Visual Studio Code et export
