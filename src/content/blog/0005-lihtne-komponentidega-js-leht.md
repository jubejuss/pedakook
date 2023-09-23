---
title: 'Kuidas teha väike dünaamilise päise ja jalusega veebileht'
description: 'Kuidas teha väike dünaamilise päise ja jalusega veebileht kasutades javaskripti. Kuidas teha modaaliga pildiportfoolio.'
pubDate: 'Sep 23 2023 10:31:00'
heroImage: '/portfolio_website_example.png'
slug: 'javascriptiga-veebileht'
---

Üks paras peavalu on see, kuidas õpilastele, kes ei tea midagi veebilehtede koodimisest, javascriptist, seda neile ärahirmutamata õpetada. Et nad suudaks enamvähem ise või AI abil hakkama saada. Põhiprobleem võib olla see, et teadmata, miks seda teha, ei teki neil ka huvi või motivatsiooni.

## Üks võimalus kuidas õpetada javascripti, on 2-3 lehelise, enda tööde portfoolio loomine. 

See on vast lihtsalt mõistetav ja kasu peaks olema nö käega katsutav.

Selleks hetkeks oleme me jõudnud HTML/CSS-i läbi käia, parasjagu vaatame ka mis on CSS raamistikud. Selgeks on saanud, et mitme lehekülje puhul on tüütu käsitsi muudkui päist või jalust igal lehel muuta. Seega on paras aeg näidata, et kui leht lammutada taaskasutatavateks komponentideks, mida saab ühes kohas muuta, nii et muutus toimub kõikjal, lendab töö märksa reipamalt. See on aga hea võimalus näidata miks ja kuidas javascript on hea ja aitab.

Seda võiks vabalt teha koostöös ChatGPT või mõne muu "tehisintelligendiga".

Kõik peaks hakkama nagu ikka disainikavandist ja eelkõige mõistmisest, miks sul portfooliot vaja läheb. Antud juhul on portfoolio kasulik praktikale minnes – selmet seletada, mida sa kõike oskad, saad näidata, mida sa teinud oled.

Antud näites teeme 3-alamlehega portfooliolehe – esileht, enesetutvustus ja galerii.


Skeem on selline, et meil on igale lehele omane originaalne sisuosa ja see osa, mis on kõikidel lehtedel sama. Sama osa on päis, ehk *header* ja jalus, ehk *footer*. Mutuv osa on index leht, enesetutvustuse leht ja galeriileht.

Seega tuleb meil teha järgmised lehed:
- index.html
- minust.html
- galerii.html
- header.html
- footer.html

Footer.html ja header.html on antud juhul taaskasutatavad komponendid, millised me impordime oma põhilehtede sisse.

Siin ei ole praegu täpne sisu oluline. Seega teeme lihtsalt kolm sarnast sisulehte ja eristamiseks kirjutame igale ühele midagi erinevat sisse ning samuti teeme *headeri* ja *footeri*, mille sisse kirjutame, et need on *header* ja *footer*.

Põhilehed:
```html
<!DOCTYPE html>
<html lang="et">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Minu uhke koduleht</title>
  </head>
  <body>

    <main>

      <h1>Esileht</h1>

    </main>


  </body>
</html>

```

Lisame nüüd siia ka dünaamilised osad:
```html
<!DOCTYPE html>
<html lang="et">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Minu uhke koduleht</title>
  </head>
  <body>
    <!-- headeri asukoht-->
    <div id="header"></div>

    <main>
      <h1>Esileht</h1>
    </main>

    <!-- footeri asukoht-->
    <div id="footer"></div>

  </body>
</html>
```
Ja, et see asi meil ka mingit väljanägemist omaks, siis ka stiililehe:
```html
<!DOCTYPE html>
<html lang="et">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Minu uhke koduleht</title>

    <!-- Stiililehe asukoht -->
    <link rel="stylesheet" href="styles.css" />

  </head>
  <body>
    <div id="header"></div>
    <main>
      <h1>Esileht</h1>
    </main>
    <div id="footer"></div>
  </body>
</html>
```
Lisame javascripti, nt faili `loadComponents.js`

```javascript
function loadComponent(componentId, componentUrl) {
    fetch(componentUrl)
        .then(response => response.text())
        .then(data => {
            document.getElementById(componentId).innerHTML = data;
        });
}

loadComponent('header', 'header.html');
loadComponent('footer', 'footer.html');
```
Jagame juppideks:

Funktsiooni nimi on `loadComponent` ja sellele järgnevates sulgudes on meile vajalikud parameetrid: `componentId`, ehk HTML-failis asuva elemendi ID, kuhu me tahame sisu panna ja `componentUrl`on selle faili aadress, kust me võtame sisu, mida sinna sobiliku ID-ga elementi pista. Funktsiooni käivitamisel asendatakse need konkreetsete ID-de ja URL-idega.

See oleks ka koht, kus võiks tõstatada DOM-manipulatsioonide teema, kuna siinne on hea näide. Juhul kui pole varem teinud ja õppida sedapidi, et enne sisu ja siis mõisted.

Funktsiooni töö käik:

- `fetch(componentUrl)`: Alustatakse sisu laadimist antud componentUrl aadressilt. fetch on JavaScripti funktsioon, mis võimaldab teha võrgupäringuid.
- `.then(response => response.text())`: Kui päring on lõpetatud, saame vastuse (response). Seejärel konverteerime vastuse tekstiks kasutades response.text() meetodit.
- `.then(data => {...})`: Kui vastus on konverteeritud tekstiks, saame selle teksti data muutujas. Järgnevalt otsime HTML dokumendist elemendi, mille ID on `componentId`, ja määrame selle elemendi sisuks laetud teksti (data).
- `loadComponent('header', 'header.html');`ja `loadComponent('footer', 'footer.html');`ridadega käivitataksegi funktsioon ise, millega HTML-is asuvad ID-d `header`ja `footer` vastavalt `header.html`ja `footer.html`failide sisudega.

Lühidalt: See funktsioon laeb sisu antud URL-ilt ja paigutab selle HTML dokumendi kindlasse elementi, mille ID on antud parameetriga.

Ja seejärel lisame javascripti asukoha ka meie HTML-i(desse)

```html
<!DOCTYPE html>
<html lang="et">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Minu uhke koduleht</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div id="header"></div>
    <main>
      <h1>Esileht</h1>
    </main>
    <div id="footer"></div>
  </body>
      <!-- javascripti asukoht -->
  <script src="loadComponents.js" type="module"></script>  
</html>
```
Ja nõnda ka kaks ülejäänud plaanitud lehte.