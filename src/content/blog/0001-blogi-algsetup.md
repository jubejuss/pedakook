---
title: 'Astro algsetup'
description: 'Kuidas seadistada blogi Astroga ja lahendada linkide avanemine. Ülevaade Markdownist ja selle integreerimisest Astro projektiga.'
pubDate: 'Sep 09 2023'
heroImage: '/blogipostitus.jpg'
heroImageAlt: 'Trükimasin sügislehtedega'
slug: 'astro-algsetup'
---

See leht on loodud [Astroga](https://astro.build) tutvumise eesmärgil. Kirjutan siin postituses lahti esimesed sammud, mida Astro püstipanemiseks tegin.

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
    const href = link.getAttribute("href");
    if (href && (href.startsWith("http://") || href.startsWith("https://"))) {
      link.setAttribute("target", "_blank");
      link.setAttribute("rel", "noopener noreferrer");
    }
  });
});
</script>
```
Mida see skript täpsemalt teeb:

- `document.addEventListener("DOMContentLoaded", function () {`
See rida alustab sündmuste kuulamist, mis toimub siis, kui HTML-dokument on täielikult laaditud (DOMContentLoaded sündmus).
- `const mainLinks = document.querySelectorAll("main a");`
See rida leiab kõik lingid (`<a>` elemendid) peamises sisuosas (element märgistatud `<main>`), ja salvestab need muutujasse mainLinks.
- `mainLinks.forEach((link) => {`
See rida algatab tsükli, mis käib läbi kõik leitud lingid ükshaaval.
- `const href = link.getAttribute("href");`
See rida võtab lingi href atribuudi väärtuse ja salvestab selle muutujasse href.
- `if (href && (href.startsWith("http://") || href.startsWith("https://"))) {`
See rida kontrollib, kas href muutuja eksisteerib ja kas see algab kas "http://" või "https://". Kui tingimus on tõene (st kui link on välimine link), siis järgmine osa töötab.
- `link.setAttribute("target", "_blank");`
Kui link on välimine, siis see rida seab lingile target atribuudi väärtuseks "_blank", mis tähendab, et link avatakse uues veebibrauseri aknas või vahekaardil.
- `link.setAttribute("rel", "noopener noreferrer");`
See rida seab lingile "rel" atribuudi väärtuseks "noopener noreferrer", mis on turvameede, et tagada, et uues aknas avatud link ei saaks juurdepääsu teie lehe koodile ja brauseri funktsioonidele.
- `});`
See rida sulgeb tsükli, mis käis läbi kõik leitud lingid.

Kokkuvõttes teeb see skript järgmist:

- See ootab, kuni HTML-dokument on täielikult laaditud.
- See otsib kõik lingid, mis asuvad peamises sisuosas.
- See kontrollib iga lingi href atribuuti, et teha kindlaks, kas see on välimine link (algab "http://" või "https://").
- Kui leitakse välimine link, siis see seatakse nii, et see avatakse uues brauseri aknas või vahekaardil.
- Lisaks lisatakse turvameetmed, et vältida juurdepääsu teie lehele ja brauseri funktsioonidele uues aknas avatud lingi kaudu.

## Pildi alt tag *frontmatteris*
Frontmatterisse peaks lisama ka heroImage pildi alt tag'i. No sest igale pildile on vaja alt tag'i. Selleks on vaja seadistada kaks välist faili: `config.ts` ja `BlogPost.astro`layout ehk laotuse fail.
Esimesse neist tuleb *Schema* alla lisada oma *image-alt* rida, nt selline: `heroImageAlt: z.string().optional()`:
```javascript
import { defineCollection, z } from 'astro:content';
const blog = defineCollection({
	schema: z.object({
		... 
		heroImageAlt: z.string().optional()
	}),
});
export const collections = { blog };
```

ning sama `heroImageAlt` tuleks seejärel lisada ka `BlogPost.astro`failis kahte kohta. 
```javascript
---
import ...
...
const { title, ..., heroImageAlt } =
  Astro.props;
---
...
  <body>
    ...
    <main>
      ...
          {
            heroImage && (
              <img
                width={1020}
                height={510}
                src={heroImage}
                alt={heroImageAlt}
              />
            )
          }
// ülejäänud kood

```

Lõpuks tuleks lisada `heroImageAlt`rida ka iga postituse frontmatterisse:
```yaml
---
title: 'Artikli või blogipostituse kirjutamine Astros'
description: 'Kuidas üldse Astos blogida. Vaata ja loe siit.'
pubDate: 'Sep 23 2023 10:30:00'
heroImage: '/astronaut_is_writing_blogpost.png'
heroImageAlt: 'astronaut kirjutab kosmoses blogipostitust'
slug: 'astro-blogisse-kirjutamine'
---
```
## Markdown
Paar sõna ka **Markdown keelest**

Nagu ütlesin, kasutan blogipostituste tegemiseks Markdown keelt. Astrol on ka integratsoonid enamkasutatud [JAMStack'i CMS'idele](https://docs.astro.build/en/guides/cms/), ent stardin ilma. Hiljem teen ka nnendega tutvust.

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

Ainult ebatavaline :)
