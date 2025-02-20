---
layout: page
title: Automatisation de PAO
description: Quelques projets d'automatisation de PAO
img: assets/img/drawing-933207_1280.jpg
importance: 3
category: professionnels
---

## Automatisation d'import d'objets dans une pagination Indesign
Création d'Atlas - Javascript

Le snippet Javascript ci-dessous est une fonction prend en argument un fichier (par ex. EPS, TIFF ...) et le place au centre d'une page. Le script dans son ensemble permet d'importer un ensemble de fichier, ce qui est idéal pour la création d'atlas, où chaque page contient un bloc de cartographie standardisé.

```javascript
// fonction placement des objets selectionnés
function myPlaceEPS(myDocument, myPage, myEPSFile){
	var myEPSPage;
	var pgWidth = myPage.bounds[3]-myPage.bounds[1]
	var pgHeight = myPage.bounds[2]-myPage.bounds[0]
//	app.pdfPlacePreferences.pdfCrop = PDFCrop.cropMedia;
	var myCounter = 0;
	var fileNb=myEPSFile.length
	var myBreak = false;
	while(myCounter != fileNb){
		if(myCounter > 0){
			// rajoute une page
			myPage = myDocument.pages.add(LocationOptions.after, myPage);
		}

		// rajoute l'object en cours sous le nom item[0]
		myEPSPage = myPage.place(File(myEPSFile[myCounter]));
		var myObject = myPage.pageItems.item(0)
		// récupère les dimensions de l'objet et de la page
		var objectWidth = myObject.geometricBounds[3]-myObject.geometricBounds[1];
		var objectHeight = myObject.geometricBounds[2]-myObject.geometricBounds[0];;
		var newX = (pgWidth-objectWidth)/2;
		var newY = (pgHeight-objectHeight)/2;
		myObject.move(undefined,[newX,newY]);
//		myEPSPage.move(newX,newY);
//		myEPSPage = myPage.place(File(myEPSFile[myCounter]),[newX,newY]);
		myCounter = myCounter + 1;
	}
}
```


## Automatisation de pagination de listes sous Indesign / Indata
Production de catalogue, index - InData

<div class="row justify-content-sm-center">
  <div class="col-sm mt-6 mt-md-0">
    {% include figure.liquid path="assets/img/indata0.png" title="exemple de formule indata" class="img-fluid rounded z-depth-1" %}
    <div class="caption">Exemple de formule InData</div>
  </div>
  <div class="col-sm mt-6 mt-md-0">
    {% include figure.liquid path="assets/img/indata1.png" title="rendu" class="img-fluid rounded z-depth-1" %}    
    <div class="caption">Rendu Associé</div>
  </div>
</div>


<div class="row justify-content-sm-center">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/indata2.png" title="autre exemple de rendu" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/indata3.png" title="autre exemple de rendu" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/indata5.png" title="autre exemple de rendu" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">Autres exemples de rendu</div>
