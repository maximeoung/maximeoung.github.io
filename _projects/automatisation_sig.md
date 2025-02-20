---
layout: page
title: Automatisation SIG
description: Aperçu de quelques projets d'automatisation SIG
img: assets/img/earth-8552339_1280.jpg
importance: 2
category: professionnels
---

## Bulk file export, bulk map production
- Production automatisée de cartes par Python QGIS, Python Arcgis
- Conversions et production de fichier en masse (PostgreSQL/PostGIS, Batches)
- Conversion de format Apache AVRO (Hadoop) vers PostGIS (sous Apache Spark)


## Traitement de bases de données SIG
- Data processing (PostgreSQL / PostGIS / PL/SQL) : agrégations et redécoupages en masse
- Data prep (PostgreSQL / PostGIS / RegEx) : combinaison de sources SIG variées pour construction de bases de données unifiées.

<div class="row">
    <div class="col-sm mt-4 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/mun_submun.png" title="Municipalités et arrondissements municipaux" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-4 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/postal.png" title="Zones postales" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-4 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/fond_unif.png" title="Fond unifié : unités administratives et postales" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A partir d'unités administratives (à gauche) et de zones postales (au centre), construction d'un fond unifié dont la géométrie est simplifiée, permettant la reconstruction de tous les niveaux administratifs et postaux supérieurs avec préservation de topologie (à droite).
</div>

- GeoJSON Minifying (Python)

extrait du script :

```python
# open file
with open(path, 'rt',encoding='utf8') as f:
    file_source = f.read()

    # on enchaîne les suppressions d'espaces
    replace_string = replace_string.replace(' [','[')
    replace_string = replace_string.replace(' ]',']')
    replace_string = replace_string.replace('[ ','[')
    replace_string = replace_string.replace('] ',']')
    replace_string = replace_string.replace(' {','{')
    #...
    replace_string = replace_string.replace(', 0',',0')
    replace_string = replace_string.replace(', 1',',1')
    #...

with open(path, 'wt',encoding='utf8') as f:
    f.write(replace_string)
    f.close()
```

Autre exemple (plus élégant, mais moins performant)

```python
strings_to_minify = [' \"','[ ',' [','] ',' ]','{ ',' {','} ',' }',': ',' :']
# 1ère passe avec la fonction replace
for str in strings_to_minify:
    # on imbrique replace(' ','') dans l'appel de replace sur la chaîne de caractères de départ
    replace_string = replace_string.replace(str, str.replace(' ',''))

# 2ème passe avec regex pour gérer les nombres
import re
str_rex = re.compile('(,)\s([0-9])'
str_rex.sub(r'\1\2', replace_string)
```

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/geojson.png" title="GeoJSON original" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    GeoJSON original
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/geojson_minified.png" title="Minified GeoJSON" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Minified GeoJSON
</div>
