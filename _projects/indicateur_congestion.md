---
layout: page
title: Indicateur de congestion de trafic routier
description: Méthologie et exemples, à partir des vitesses de véhicule par tronçon routier.
img: assets/img/indicateur_congestion.png
importance: 1
category: professionnels
---

**Problématique :**
Obtenir un indice de congestion de trafic routier par iris.

**Sources des échantillons utilisés :**
- Iris : Contour Iris IGN
- Réseau routier : TomTom Multinet
- Données de vitesse de trafic : TomTom Speed Profile

## Indice de congestion par tronçon de réseau routier

Afin d'obtenir un tel indicateur, la première étape a été de transcrire le problème :

Grâce aux données TomTom, nosu avons accès à 2 types de données :
- la vitesse moyenne théorique sur un tronçon, ou de "free flow", donnée par l'attribut `kph` (Multinet)
- la vitesse moyenne observée sur un tronçon, donnée par les attributs `week`, `weekday`, `weekend` (Speed Profiles) selon la période de la semaine que l'on souhaite analyser.

Nous pouvons assumer que plus un tronçon routier est congestionné, plus la vitesse observée sur ce tronçon s'éloigne de la vitesse de "free flow"".
Ainsi, les 1ers indicateurs associés à chaque tronçon, en découlent directement, et sont donnés par les ratios (que nosu appelrons speed_ratio):
`kph / week`
`kph / weekday`
`kph / weekend`

Lorsque ces ratios sont > à 100%, nous plafonnerons logiquement les ratios à 100% (la vitesse de free flow peut être inférieure à une vitesse observée sur un tronçon donné.)

Concernant le comportement de l'indicateur, nosu souhaitons avoir une valeur de 1 lorsque le tronçon n'est pas congestionné, et de 10 lorsque la congestion est maximale sur l'ensemble de l'échantillon observé. Nous prendrons donc le complémentaire du ratio calculé,
`1 - speed_ratio`

## Indice de congestion par Iris
Afin d'agréger les données à l'iris,
et afin de donner plus de poids aux tronçons sur lesquels il y a + de trafic routier, (et n'ayant pas accès à des données de comptage de véhicules), nous allons émettre l'hypothèse suivante :
+ un tronçon a une classe hiérarchique importante, + il aura du poids dans le calcul de l'agrégation à l'iris.
Chaque tronçon aura ainsi une pondération dont la valeur sera relative à son importance dans la hiérarchie du réseau routier.

Pour l'agrégation elle-même, nous calculons le ratio entre la longueur du tronçon et la longueur totale des tronçons dans un iris donné, et nous croisons ainsi avec la pondération retenue multipliée par l'indicateur de congestion (1 - speed ratio).

## Cartographie
Nous pouvons observer le résultat sur la carte ci-dessous :

<!-- import css de div id=map + js d'open layers'  -->
<link rel="stylesheet" crossorigin href="../../assets/ol-maps/indicateur-congestion-style.css">
<link rel="stylesheet" crossorigin href="../../assets/ol-maps/indicateur-congestion-style-legend.css">

<!-- <link rel="stylesheet" href="node_modules/ol/ol.css"> -->
<!-- <link rel="stylesheet" href="node_modules/ol-ext/dist/ol-ext.css" /> -->

<!-- import css + js de la carte -->

<script type="module" crossorigin src="../../assets/ol-maps/assets/index-indicateur-congestion.js"></script>
<link rel="stylesheet" crossorigin href="../../assets/ol-maps/assets/index-indicateur-congestion.css">
<div id="map" class="map"></div>
<div class="layer-opacity">
      <div class="layer-opacity-txt">Opacité de l'indicateur de congestion</div>
      <div class="layer-opacity-input-range">
        <input id="opacity-input" type="range" min="0" max="1" step="0.01" value="1" />
        <span id="opacity-output"></span>
      </div>
</div>


Si cet exemple produit déjà un résultat visuellement intéressant, des pistes pour affiner l'indicateur sont à envisager, notamment en élaborant davantage le système de pondération, en croisant avec les données de densité de trafic par exemple.

.
