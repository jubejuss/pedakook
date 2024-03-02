---
title: "Lume, staatilise lehe generaatori seadistamine"
description: "Loe siit, kuidas panna püsti Denol baseeruv staatilise lehe generaato"
pubDate: 'Feb 03 2024 18:45:00'
heroImage: '/arvuti-tules.webp'
heroImageAlt: 'Denosaurus'
slug: 'lume'
---

## Projektikausta korrastamine
[https://lume.land/docs/configuration/config-file/](https://lume.land/docs/configuration/config-file/)
Jätta oma lehekülgede failid kõige muuga ühte folderisse, tekitab segaduse. Seega on mõistlik tõsta eri tüüpi asjad eri kaustadesse.  

Lehekülgede jms allikate jaoks on mõistlik luua folder `src`.
Et süsteem teaks sealt faile vaadata, tuleks seda ka süsteemile öelda, lisades muutes _config.ts faili:
```typescript
import lume from "lume/mod.ts";

const site = lume({
    src: "./src",
  });

export default site;
```
Nüüd jälgib süsteem `src` folderit ja kui sinna midagi lisandub, siis lisatakse ka `_site` folderisse genereeritud staatiline HTML.

Ka väljundkausta – `_site` – võib muuta, kui lisada sellekohane rida `config.ts`faili. Näiteks:
```typescript
import lume from "lume/mod.ts";

const site = lume({
    src: "./src",
    dest: "./output",
  });

export default site;
```

## Layoutid ja taaskasutus
Lehtede disainimiseks kasutatakse *layouti* faile. Nende jaoks tuleb luua `src`folderisse `_includes` folder ja sellesse esialgu `layout.vto`. Kui layoute on vaja rohkem, siis lisandub siia ka faile.

`.vto` on Vento templiitimismootori fail ja see on Lumes vaikimisi peal. Soovi korral võib liada pluginate alla ka mõne muu, nt Nunjucks'i, Pug'i, jsx'i vms.

Selline templiit on sisult lihtne html, kus mingid osad asendataklse dünaamilise sisuga.

Näiteks:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lume</title>
</head>
<body>
    {{ content }}
</body>
</html>
```
Nüüd tuleb luua `src`folderisse ka `_data.yml`fail, millesse lisada layoutide asukoht:
```yml
layout: layouts/layout.vto
```
 ja seejärel loeb süsteem `_includes` folderist `layout.vto` ja kastab seda kõikide `_includes` folderiga samas folderis olevatest algfailidest staatiliste lehtede genereerimisel. 

Layout'i kasutamist saab korraldada ka lihtsamalt – kirjutad oma markdown faili frontmatterisse (eraldatud osa päises) millist layout'i kasutada:

```md
---
title: See on minu veebileht
layout: layout.vto
---
# See on esimene leht
## Siin on alampealkiri
Ja siin lingid:
[Esilehele](/)  
[Projektist](/projektist)
```
Kui aga faile on palju, ei ole see enam lihtsam.

Nagu ülalpool näha, on frontamtteris kirjas ka lehe tiitel, selle võib nüüd layouti failis ära märkida, et see kirjutataks staatilisse faili:
```html
<title>{{title}}</title>
```
Vaata siit lisa: [https://lume.land/docs/getting-started/page-data/](https://lume.land/docs/getting-started/page-data/)

Ajapikku tekib `_includes` folderisse sisu juurde, sel juhul on mõistlik tõsta layoutid oma folderisse ja näidata ka `_data.yml` failis ära uus asukoht:
```yml
layout: layouts/layout.vto
```
Nüüd võid luua lisaks mõned testlehed.

## Navigatsioon
Kui lehti on rohkem, tekib vajadus taaskasutatava menüü järele. Lumes aitab seda korraldada nav plugin. Pluginate installeerimisest oli juttu eelmises artiklis: [deno-lume](/blog/deno-lume)

Lisa nav plugin `_config.ts`-i:
```typescript
import lume from "lume/mod.ts";
import nav from "lume/plugins/nav.ts";

const site = lume({
    src: "./src",
  });

site.use(nav());

export default site;
```
Seejärel loo `_includes` folderisse `templates` folder, kuhu omakorda kaks vento faili: `menu.vto` ja `menu_item.vto`.  

Lisa `menu.vto`-sse:
```html
<ul>
  {{ for item of nav.menu().children }}
    <li>
      {{ include "templates/menu_item.vto" { item } }}
    </li>
  {{ /for }}
</ul>
```
ja `menu_item.vto`-sse
```html
<a href="{{ item.data.url }}">
  {{ item.data.title }}
</a>
```
Esimeses käivitatakse nav plugin, mis kasutab template folderis asuvat vento faili mallina.

