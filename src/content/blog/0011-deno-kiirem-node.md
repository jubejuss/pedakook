---
title: "Deno – moodne Node. Lume – staatilise lehe generaator Node'le"
description: "Loe siit, kuidas panna püsti Denol baseeruv staatilise lehe generaato"
pubDate: 'Feb 02 2024 18:45:00'
heroImage: '/deno.webp'
heroImageAlt: 'Denosaurus'
slug: 'deno-lume'
---

Astro on tore, ent on muidki lahendusi.  
## Deno ja Lume
Deno on moodsa JavaScripti ja TypeScripti käituse keskkond, mille on loonud Ryan Dahl, Node.js looja. See on loodud eesmärgiga parandada Node.js-i mõningaid puudusi.  

Deno pakub mitmeid olulisi omadusi:
* **Turvalisus:** Deno on vaikimisi turvaline. Skriptidel pole juurdepääsu failisüsteemile, võrgule või muudele ressurssidele, kui selleks pole antud selgesõnalist luba.
* **TypeScripti Tugi:** Deno toetab TypeScripti otsekarbil, ilma et oleks vaja eraldi tõlkida.
* **Moodulite Importimine URL-ide Kaudu:** Deno võimaldab importida mooduleid otse URL-idelt, mis kaotab vajaduse eraldi paketihaldurite järele.
* **Standardraamatukogu:** Deno sisaldab laia standardraamatukogu, mis on kirjutatud TypeScriptis ja on hoolikalt läbi mõeldud ja üle vaadatud.
* **Kaasaegne API:** Deno API on lubadustel põhinev (promises) ja kasutab moodsaid JavaScripti võimalusi, nagu async/await, et parandada asünkroonse koodi kirjutamist.

### Lume
Mis on lume?
Lume on staatiliste lhtede generaator Deno'le.

### Deno ja Lume setup
**Deno** install on lihtne, juhend leitav tema kodulehelt: [https://docs.deno.com/runtime/manual/getting_started/installation](https://docs.deno.com/runtime/manual/getting_started/installation)

**Lume** vajab muidugi pisut enam seadistamist, kuid on ülesehituselt lollakalt lihtne – lehe valmistamiseks tuleb Lume lihtsalt installida ja kirjutada nt Markdown fail, kõik muu teeb juba süsteem vaikimisi. Muidugi tuleb keerulisema lehe puhul korrastada süsteem ja näidata kus asuvad algfailid jne.

Niisiis, [installimiseks](https://lume.land/docs/overview/installation/) jälgi ametlikku juhendit või kasuta siinset. Loo projektifolder ja jooksuta selles käsklust:
```bash
deno run -Ar https://deno.land/x/lume/init.ts
```
Selle tagajärjel genereeritakse projektifolderisse kaks faili – `_config.ts ja `deno.json`
Installides küsitakse, mis pluginaid soovid installida, kuid võib piirduda minimaalsega – pluginate lisamine on lihtne, tuleb vaid `_config.ts`faili lisada mõned read.

`_config.ts` ilma pluginateta:
```typescript
import lume from "lume/mod.ts";

const site = lume();

export default site;
```
Sama kui installimisel on lisatud `attributes` plugin:
```typescript
import lume from "lume/mod.ts";
import attributes from "lume/plugins/attributes.ts";

const site = lume();

site.use(attributes());

export default site;
```
`deno.json` jääb mõlemal juhul samasuguseks:
```json
{
  "tasks": {
    "lume": "echo \"import 'lume/cli.ts'\" | deno run --unstable -A -",
    "build": "deno task lume",
    "serve": "deno task lume -s"
  },
  "compilerOptions": {
    "types": [
      "lume/types.ts"
    ]
  },
  "imports": {
    "lume/": "https://deno.land/x/lume@v2.0.3/"
  }
}
```
Ja sellega juba süsteem töötabki – lisa projekti juurkataloogi markdown fail, jooksuta terminalis käsklust `deno task lume --serve --port=8000` ja näedki tulemust. `deno task lume` loob staatiliste failide kataloogi `_site`, `--serve` paneb süsteemi muudatusi jälgima ja `--port=8000`on muidugi pordi number, kust tulemust näed. Ehk, et vaata brauseris `localhost:8000`




