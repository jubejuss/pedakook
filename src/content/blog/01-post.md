---
title: 'Esimene oma postitus'
description: 'Lorem ipsum dolor sit amet'
pubDate: 'Jan 15 2023'
heroImage: '/blogipostitus.jpg'
---

Esimeses postituses midagi põrutavat ei ole, peamiselt on see tehtud Astroga tutvumise eesmärgil. Siiski räägin ära esimesed sammud, mida ma tegin.

## Niisiis esimesed tähelepankud

Blogi üldleht oli vaikimisi moel, et vanad postitused olid eespool. Selle muutmine on lihtne blogi üldlehe astro failis (asub pages -> blog -> index.astro) vaja muuta a b:
```javascript
const posts = (await getCollection("blog")).sort(
  (b, a) => a.data.pubDate.valueOf() - b.data.pubDate.valueOf()
);
```

Teine props tekkis linkidega, nimelt Markdown keele puhul, millega seda blogi sisustan, puudub uues tabis avanemise võimalus. See on halb, sest sel moel klikab lugeja siit end minema. Kiirel või põghusal otsimisel ei leidnud ka Astro kodulehelt sellele lahendust.

Seega kirjutasime koos ChatGPT-ga selle tarbeks javaskripti funktisooni, mille pistsin blogiposti templiiti:
```javascript
<script>
    document.addEventListener("DOMContentLoaded", function () {
      const mainLinks = document.querySelectorAll("main a");
      mainLinks.forEach((link) => {
        link.setAttribute("target", "_blank");
        link.setAttribute("rel", "noopener noreferrer");
      });
    });
  </script>
  ```

## Markdown
Paar sõna ka **Markdown keelest**

Jätkub kui aega tekib

Teemad, mida pean siin käsitlema:  
Git,  
Markdown,  
Cloudflare,  
...
