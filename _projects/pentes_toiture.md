---
layout: page
title: Pentes de toiture
description: Calcul de la pente à partir des données contenues dans la BD Topo de l'IGN
img: assets/img/pentes_toiture.png
importance: 1
category: professionnels
---

**Problématique :**
Evaluer les pentes de toiture

**Sources des échantillons utilisés :**
- Bâtiments : BD Topo IGN

## Méthodologie
La table "Batiments" de la BD Topo contient des attributs intéressants :
- l'altitude minimale toit, `z_min_toit`
- l'altitude maximale du toit, `z_max_toit`

On opère la simplification suivante :
- on considère l'altitude à l'égoût du toit = `z_min_toit`
- on considère l'altitude au faitage = `z_max_toit`
- on considère grossièrement que les bâtiments sont rectangulaires dans l'ensemble.

Nous avons 1 premier côté de la tangente de la pente, `z_max_toit - z_min_toit`

Le 2ème côté se retrouve par opération géométrique. Dans PostGIS, la fonction `ST_MinimumBoundingCircle` permet de créer le cercle englobant notre bâtiment considéré rectangulaire. On obtient l'hypothénuse. Ce qui permet de retrouver une approximation des dimensions de chaque côté du rectangle. En découle la moitié de la largeur qui nous donne le 2ème côté de la tangente.

## Cartographie
Nous pouvons observer le résultat de l'estimation de la pente sur la carte ci-dessous :

<!-- import css de div id=map + js d'open layers'  -->
<link rel="stylesheet" crossorigin href="../../assets/ol-maps/pentes-toiture-style.css">
<link rel="stylesheet" crossorigin href="../../assets/ol-maps/pentes-toiture-style-legend.css">

<!-- <link rel="stylesheet" href="node_modules/ol/ol.css"> -->
<!-- <link rel="stylesheet" href="node_modules/ol-ext/dist/ol-ext.css" /> -->

<!-- import css + js de la carte -->

<script type="module" crossorigin src="../../assets/ol-maps/assets/index-pentes-toiture.js"></script>
<link rel="stylesheet" crossorigin href="../../assets/ol-maps/assets/index-pentes-toiture.css">
<div id="map" class="map"></div>
<div class="layer-opacity">
    <div class="layer-opacity-txt">Opacité des pentes de toiture</div>
    <div class="layer-opacity-input-range">
      <input id="opacity-input" type="range" min="0" max="1" step="0.01" value="1" />
      <span id="opacity-output"></span>
    </div>
</div>
<div class="caption"> </div>

.
