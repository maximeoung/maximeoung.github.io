---
layout: page
title: project 10 - Indice de congestion
description:
img:
importance: 1
category: work
related_publications: true
---

Test map project.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    map: ???
    ---
```html
<script type="module" crossorigin src="../assets/ol-maps/assets/index-B3jjzupI.js"></script>
<link rel="stylesheet" crossorigin href="../assets/ol-maps/assets/index-D09opdbs.css">
<div id="map" class="map"></div>
```

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
