---
title: 'Astro algsetup'
description: 'Lorem ipsum dolor sit amet'
pubDate: 'Sep 09 2023'
heroImage: '/blogipostitus.jpg'
slug: 'astro-algsetup'
---

Esimeses postituses midagi põrutavat ei ole, peamiselt on see tehtud [Astroga](https://astro.build) tutvumise eesmärgil. Siiski räägin ära esimesed sammud, mida ma tegin.

## Niisiis esimesed tähelepankud Astro kohta

Ehitasin kogu asja üles kasutades [Astro starterkit blog templiiti](https://github.com/withastro/astro/tree/main/examples/blog). [Ettejoonistatud teemasid on muidugi veel](https://astro.build/themes/) ja võib ka [Astro juhiste järgi nullist ehitada](https://docs.astro.build/en/tutorial/0-introduction/).

Juhist ei hakka siia lisama, kuna see on selle esimeses githubi lingis kenasti olemas. Loomulikult peab arendusmasinas olema installeeritud [Node](https://nodejs.org/en), vajalikud käsklused on kirjas package.json failis. 

Blogi üldleht oli vaikimisi moel, et vanad postitused olid eespool. Selle muutmine on lihtne - blogi üldlehe astro failis (asub pages -> blog -> index.astro) vaja muuta a ja b järjekord:
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

Markdown on lihtne vormindamist lubav keel. Lihtne on ta muidugi sellele, kes seda juba mõnda aega harjutanud ja siis ta kipub juba meeldima ka. Ta on kergekaaluline ja teda on võimalik edasi ümber tõlgendada erinevatesse keeletesse, nagu nt HTML või formaatidesse nagu PDF või MSWord. Markdown on mitmetes keskkondades standardiks, Markdown on kasutusel gitihalduskeskkondades. Tänu Markdownile ei ole vaja lehte koormata erinevate "editoridega".    
Välja näeb ta umbes nii:  
```markdown
## See on h2 pealkiri
**See on bold tekst**  
See on tavaline tekst  
[Ja see on link](https://linkkuhugi.eet)
```
Eelnev koodiplokk näeb veebileheks pööratuna nii:
## See on h2 pealkiri
**See on bold tekst**  
See on tavaline tekst  
[Ja see on link](https://linkkuhugi.eet)

Markdowni juhendmaterjal [on leitav siit](https://www.markdownguide.org/cheat-sheet/)

Üldlehed luuakse HTML'i kirjutades. Seega peab antud seadistusega blogi ehitamiseks tundma ni HTML'i kui Markdowni. See pole raske, ent ilmselt tavaline inimene sellega tegelema ei viitsi hakata.