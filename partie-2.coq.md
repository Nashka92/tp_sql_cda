## 10 Listez pour chaque ticket la quantité totale d’articles vendus. (Classer par quantité décroissante)

```mysql
select SUM(QUANTITE) as somme
from ventes
GROUP BY QUANTITE

```

## 11 Listez chaque ticket pour lequel la quantité totale d’articles vendus est supérieure à 500. (Classer par quantité décroissante)

```mysql
select sum(QUANTITE) as total, NUMERO_TICKET
from ventes
group by NUMERO_TICKET
having total >= 500
order by total desc
```

## 12 Listez chaque ticket pour lequel la quantité totale d’articles vendus est supérieure à 500. On exclura du total, les ventes ayant une quantité supérieure à 50 (classer par quantité décroissante)

```mysql
select sum(QUANTITE), NUMERO_TICKET
from ventes
where QUANTITE >= 500
group by NUMERO_TICKET
order by QUANTITE desc

```

## 13 Listez les bières de type ‘Trappiste’. (id, nom de la bière, volume et titrage)

```mysql
select ID_TYPE, NOM_ARTICLE, VOLUME, TITRAGE
from article
inner join `type`
where type.NOM_TYPE = 'Trappiste'
```

## 14 Listez les marques de bières du continent ‘Afrique’

```mysql
select NOM_MARQUE, NOM_CONTINENT
from marque
inner join pays 
inner join continent 
where continent.NOM_CONTINENT = 'Afrique' 

```

## 15 Lister les bières du continent ‘Afrique’

```mysql
select NOM_ARTICLE, NOM_CONTINENT
from article
inner join pays 
inner join continent 
inner join marque
where continent.NOM_CONTINENT = 'Afrique' 
```

## 16. Lister les tickets (année, numéro de ticket, montant total payé). En sachant que le prix de vente est égal au prix d’achat augmenté de 15%.

```mysql
SELECT ticket.ANNEE, ticket.NUMERO_TICKET, ticket.DATE_VENTE,
SUM(ventes.QUANTITE * article.PRIX_ACHAT * 1.15) AS 'Montant_total'
FROM ticket
JOIN ventes USING (ANNEE, NUMERO_TICKET)
JOIN article ON article.ID_ARTICLE= ventes.ID_ARTICLE

```

## 17  Donner le C.A. par année.

```mysql
SELECT ventes.ANNEE, SUM(ventes.QUANTITE * article.PRIX_ACHAT * 1.15) AS 'Chiffre_affaire'
FROM ventes
JOIN article ON article.ID_ARTICLE= ventes.ID_ARTICLE
GROUP BY ventes.ANNEE
ORDER BY ventes.ANNEE
```

## 18. Lister les quantités vendues de chaque article pour l’année 2016.

```mysql
SELECT ventes.ANNEE, article.NOM_ARTICLE, sum(ventes.QUANTITE) as "quantite_vendue"
FROM ventes
JOIN article ON article.ID_ARTICLE = ventes.ID_ARTICLE
WHERE ventes.ANNEE = 2016
GROUP BY article.NOM_ARTICLE
ORDER BY ventes.ANNEE

```

## 19. Lister les quantités vendues de chaque article pour les années 2014, 2015, 2016.

```mysql
SELECT ventes.ANNEE, article.NOM_ARTICLE, 
sum(ventes.QUANTITE) as "quantite_vendue"
FROM ventes
JOIN article ON article.ID_ARTICLE = ventes.ID_ARTICLE
WHERE ventes.ANNEE BETWEEN 2014 and 2016 and ventes.ANNEE  between 2015 and 2016
GROUP BY article.NOM_ARTICLE
ORDER BY ventes.ANNEE

```

