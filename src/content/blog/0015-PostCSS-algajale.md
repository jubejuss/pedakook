---
title: "Kui juba, siis juba – ehk PostCSS Sassi asemel"
description: "Kuigi Bootstrapis on veel Sass sees, siis hetkel kasutavad moodsad arendused pigem puhast CSS-i. See siiski vajab veel mõnd vidinat"
pubDate: 'March 14 2025 16:50:00'
heroImage: '/hirmul-arendaja.webp'
heroImageAlt: 'hirmul-arendaja'
slug: 'postcss-algajale'
---

**PostCSS: Lihtne setup algajale**

Pikka aega olid CSS-i ladusamaks kirjutamiseks kasutusel preprotsessorid, ehk  abivahendid, mis lubasid kasutada keerukmaid lahendusi nagu muutujad, funktsioonid, mixinid (eelkomponeeritud) jms keerukad lahendused, mis võimaldasid kirjutada CSS-i kiiremini. Tuntumad abibahendid neist SASS ja LESS.

CSS on aga täiustunud, nt saab kaasaegses CSS-is kasutada muutujaid, pesastamist (nesting) ja peagi ka funktsioone. Selle arengu tagajärjel on taas populaarsemaks muutunud css-i kasutamine ilma eeltöötlejateta. Näiteks kasutavad enamus moodsamatest või uuematest front-end teekidest kaasajal Tailwind raamistikku, mis omakorda baseerub puhtal css-il.

Siin on aga mõned agad – endiselt ei saa puhta css-iga kõiki nõudeid automatiseerida ja seetõttu tuleb kasutada mõningaid abivahendeid.

## PostCSS

PostCSS on tööriist, mis muudab CSS-i JavaScripti abil. Erinevalt Sassist või Lessist pole PostCSS ise eelprotsessor, vaid pigem raamistik, mis laseb sul kasutada erinevaid pistikprogramme (plugin'e), et oma CSS-i täiendada, mh kasutada SASS'ist või LESS'ist tuntud funktsionaalsust. Ja neid pistikuid on palju. Lihtsamalt öeldes võid kirjutada jõledalt sodise CSS-i ja PostCSS-i abil saad sella ära korrastada. Saad kasutada keerulisemat pesastamist ja igasuguseid keerukaid lahendusi, mis muudavad arenduse kiiremaks.

PostCSS'i head küljed:
- Võtad ainult need pistikprogrammid, mida päriselt vajad
- Töötleb CSS-i kiiremini kui teised tööriistad
- Saad luua oma pistikprogramme või valida sadade olemasolevate seast
- Võimaldab kasutada tuleviku CSS-i omadusi juba praegu

Võibolla suurem probleem ongi pistikprogrammide üleküllus :)  
https://postcss.org/docs/postcss-plugins


## PostCSS: Lihtne setup algajale

Siin on lihtne PostCSS seadistus, mis laseb kasutada tuleviku CSS-i omadusi ja lisab automaatselt vajalikud prefiksid.  
Ehk et, mida on tavaliselt vaja – tüütu on kirjutada erinevatele brauserite sobivaid erisusi, mugavam on kasutada pesastamist, mõnusam on lasta tarkvaral kogu kood korrastada jne. Seega...

### 1. Minimaalne PostCSS-i pakett, mis teeb minimaalse vajaliku.

**Esmalt põhiline – tegemist on Node lahendusega**  
Seega sul peab olema Node.js installitud.

Seejärel installime vajalikud npm paketid:

```bash
npm install --save-dev postcss postcss-cli autoprefixer postcss-preset-env
```

Mida need paketid teevad?
- `postcss` – põhipakett CSS-i muutmiseks
- `postcss-cli` – käsurea tööriist PostCSS-i kasutamiseks
- `autoprefixer` – lisab automaatselt vajalikud vendor-prefiksid (nt `-webkit-`, `-moz-`)
- `postcss-preset-env` – võimaldab kasutada tuleviku CSS-i omadusi

Näiteks võimaldab `postcss-preset-env` kasutada täielikku pesastamist:  
```css
.card {
    &__header {
        // code
    }
}

```

### 2. Konfiguratsioonifail

Järgmiseks loome PostCSS konfiguratsiooni faili `postcss.config.js`:

```javascript
module.exports = {
  plugins: [
    require('postcss-preset-env')({
      stage: 1, // Kasutame uuemaid CSS omadusi
      features: {
        'nesting-rules': true // Lubame CSS-i pesastamist
      }
    }),
    require('autoprefixer')
  ]
};
```

See lihtne seadistus võimaldab:
- Kasutada CSS-i pesastamist (nesting), mis on sarnane Sassi süntaksile
- Kasutada tuleviku CSS-i omadusi
- Lisada automaatselt vajalikke vendor-prefikseid

### 3. Browserslist seadistus

Autoprefixer tahab teada, milliseid brausereid peab toetama. Selleks lisame `package.json` faili järgmise osa:

```json
"browserslist": [
  "> 1%",
  "last 2 versions",
  "not dead"
]
```

See ütleb, et toetame:
- Brausereid, mille turuosa on suurem kui 1%
- Iga brauseri kahte viimast versiooni
- Aktiivselt toetatavaid brausereid (mitte vananenud brausereid)

### 4. NPM skriptid

Postcss-i saab jooksutada käsuga `postcss` mille järel näidatakse ära, kus asuvad lähtefailid ja kuhu soovitakse lõpfailid kirjutada. Saab kasutada ühekordse käsuna, kuid saab panna ka muudatusi jälgima nii, et kui midagi lähtefailidesm muuta, kirjutatakse see kohe ka lõõpfaili:
```bash
postcss src/css/style.css -o dist/css/style.css
```
või
```bash
postcss src/css/style.css -o dist/css/style.css --watch
```
Aga, et asja lihtsamalt kasutada, lisame käsud `package.json` faili:

```json
"scripts": {
  "css": "postcss src/css/style.css -o dist/css/style.css",
  "watch:css": "postcss src/css/style.css -o dist/css/style.css --watch"
}
```
Nüüd saame jooksutada terminalis käsklusi vastavalt:
- `npm run css` – töötleb CSS-i ühe korra
- `npm run watch:css` – jälgib CSS-i muudatusi ja töötleb neid automaatselt


## PostCSS kasutamine praktikas

Nüüd, kui seadistus on paigas, vaatame, kuidas PostCSS-i päriselt kasutada.

### CSS-i pesastamine

Üks populaarsemaid PostCSS funktsioone on CSS-i pesastamine, mis laseb kirjutada selektoreid hierarhiliselt, sarnaselt Sassile:

```css
/* Enne (tavaline CSS) */
.card { background: white; }
.card__title { color: blue; }
.card__body { padding: 1rem; }
.card__body-text { margin-bottom: 0.5rem; }

/* Pesastamine */
.card {
  background: white;
  
  &__title {
    color: blue;
  }
  
  &__body {
    padding: 1rem;
    
    &-text {
      margin-bottom: 0.5rem;
    }
  }
}

/* Värvi funktsioon /*
.button {
  /* color-mix võib vajada tuge mõnedes brauserites */
  background-color: color-mix(in srgb, #3490dc 80%, white);
  
  &:hover {
    /* Funktsioon võrdleb põhivärvi kontrastsust kahe värviga – valge (white) ja must (black) ja selle tulemusena tagastatakse see värv, mis annab parima kontrasti põhivärviga. */
    color: color-contrast(var(--primary-color) vs white, black);
  }

```

## Kasulikud PostCSS pistikprogrammid

Lisaks põhiseadistusele on olemas palju PostCSS pistikprogramme, mis teevad su töö lihtsamaks:

- **postcss-import** – `@import` nii, et impordib teised css-failid põhifaili
- **cssnano** – CSS-i minimeerimine, kirjutab kogu css-i ühte ritta
- **postcss-nested** – alternatiivne pesastamise süntaks, muudab pesastamise täielikuks
- **postcss-custom-media** – lisab toetuse kohandatud meediapäringutele
- **postcss-color-function** – lisab CSS-i värvi funktsioonid

Alljärgnevalt on näide installeeritud pistikutega `package.json` ja `postcss.config.js` failidest: 

```json
{
  "name": "Postcss example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "css:dev": "MINIFY_CSS=false postcss src/style.css -o css/style.css --map --watch",
    "css:build": "MINIFY_CSS=true postcss src/style.css -o css/style.css --map",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "autoprefixer": "^10.4.21",
    "cssnano": "^7.0.6",
    "postcss": "^8.5.3",
    "postcss-cli": "^11.0.1",
    "postcss-custom-media": "^11.0.5",
    "postcss-import": "^16.1.0",
    "postcss-nested": "^7.0.2",
    "postcss-sorting": "^9.1.0"
  }
}

```

```json
// Keskkonna muutuja, mis määrab, kas minimeerida CSS-i või mitte
// Vaikimisi on minimiseerimine välja lülitatud (arenduskeskkonna jaoks)
const MINIFY_CSS = process.env.MINIFY_CSS === 'true';

module.exports = {
    plugins: [
      // Põhilised töötlemise pluginad
      require('postcss-import'),      // Käsitleb @import reegleid
      require('postcss-nested'),      // Võimaldab CSS reeglite pesastamist
      require('autoprefixer'),        // Lisab tarnija eesliited
      
      // Vormindamine ja organiseerimine
      require('postcss-sorting')({
        'order': [
          'custom-properties',        // :root { --color: red; }
          'dollar-variables',         // $color: red;
          'declarations',             // color: red;
          'at-rules',                 // @media, @supports
          'rules'                     // .foo { ... }
        ],
        // Kasutame SMACSS järjestust omaduste jaoks
        'properties-order': 'smacss',
        // Säilitame tühikud reeglite vahel
        'preserve-empty-lines-between-children-rules': true
      }),
      
      // Optimeerimine (tingimuslik)
      ...(MINIFY_CSS ? [require('cssnano')] : []),
      
      // Funktsioonid
      require('postcss-custom-media')  // Käsitleb kohandatud meediapäringuid
    ],
    map: {
      inline: false,
      annotation: true,
      sourcesContent: true
    }
  };
```

See seadistus loob tervikliku CSS töövoo, mis automatiseerib mitu keerukat ülesannet. 

## Installeeritud pistikprogrammid

- **postcss** ja **postcss-cli** - tuumikpaketid, mis võimaldavad CSS-i muutmist ja käsureatoe
- **autoprefixer** - lisab automaatselt brauseripõhised eesliited (nt `-webkit-`, `-moz-`), et CSS töötaks erinevates brauserites
- **cssnano** - minimeerib CSS-i, eemaldades tühikud, kommentaarid ja optimeerides koodi tootmiskeskkonna jaoks
- **postcss-import** - lahendab `@import` laused, ühendades kõik imporditud CSS-failid ühte väljundfaili
- **postcss-nested** - võimaldab Sassi-sarnast stiilide pesastamist (nesting), mis teeb CSS-i kirjutamise intuitiivsemaks
- **postcss-custom-media** - lisab toe kohandatud meediapäringutele (nt `@custom-media --mobile (max-width: 768px);`)
- **postcss-sorting** - organiseerib CSS-i reeglid ja omadused kindla struktuuri järgi, muutes koodi loetavamaks

## Skriptid (package.json)

```json
"scripts": {
  "css:dev": "MINIFY_CSS=false postcss src/style.css -o css/style.css --map --watch",
  "css:build": "MINIFY_CSS=true postcss src/style.css -o css/style.css --map"
}
```

- **css:dev** - arendusrežiim, mis:
  - Seab keskkonna muutuja `MINIFY_CSS=false` (ei minimeeri CSS-i)
  - Töötleb CSS-i lähtekoodist (`src/style.css`) väljundisse (`css/style.css`)
  - Loob source map'i (--map), mis aitab brauseri dev-tools'is näha, millisest algsest failist CSS pärineb
  - Jälgib muudatusi (--watch) ja uuendab väljundit automaatselt, kui lähtefailid muutuvad

- **css:build** - tootmisrežiim, mis:
  - Seab keskkonna muutuja `MINIFY_CSS=true` (minimeerib CSS-i)
  - Töötleb CSS-i ühekordselt, optimeerides seda tootmiskeskkonna jaoks

## Konfiguratsioonfail (postcss.config.js)

```javascript
const MINIFY_CSS = process.env.MINIFY_CSS === 'true';

module.exports = {
    plugins: [
      // Põhilised töötlemise pluginad
      require('postcss-import'),      // Ühendab failid
      require('postcss-nested'),      // Võimaldab pesastamist
      require('autoprefixer'),        // Lisab vajalikud eesliited
      
      // Vormindamine ja organiseerimine
      require('postcss-sorting')({
        'order': [
          'custom-properties',        // CSS muutujad
          'dollar-variables',         // Preprocessori muutujad
          'declarations',             // Tavalised CSS omadused
          'at-rules',                 // @media, @supports jne
          'rules'                     // Alamselektorid
        ],
        'properties-order': 'smacss', // Järjestab omadused SMACSS metoodika järgi
        'preserve-empty-lines-between-children-rules': true // Säilitab loetavuse
      }),
      
      // Tingimuslik minimeerimine
      ...(MINIFY_CSS ? [require('cssnano')] : []),
      
      // Funktsioonid
      require('postcss-custom-media')  // Lisab kohandatud meediapäringud
    ],
    // Source map seadistus
    map: {
      inline: false,     // Loob eraldi .map faili
      annotation: true,  // Lisab viite map failile
      sourcesContent: true  // Sisaldab originaalkoodi map failis
    }
};
```

## Töövoog

1. **Failide ühendamine** - PostCSS kogub kõik `@import` kaudu viidatud failid
2. **Pesastamine** - Teisendab pesastatud CSS-i (Sass-stiilis hierarhiad) tavaliseks CSS-iks
3. **CSS omaduste sorteerimine** - Järjestab omadused loogiliselt SMACSS metoodika järgi
4. **Brauseri eesliidete lisamine** - Lisab vajalikud eesliited (-webkit, -moz jne)
5. **Kohandatud meediapäringute lisamine** - Teisendab kohandatud meediapäringud brauseritele arusaadavateks
6. **Minimeerimine (ainult tootmisrežiimis)** - Eemaldab kommentaarid, tühikud ja optimeerib koodi

## Mis on selle seadistuse sisu?

1. **Tingimuslik minimeerimine** - Kasutab keskkonna muutujat, et otsustada, kas CSS minimeerida või mitte
2. **Struktureeritud sorteerimine** - Järgib SMACSS metoodikat CSS omaduste järjestamisel
3. **Source maps** - Muudab lähtekoodi silumisel leitavaks, isegi kui väljund on transformeeritud
4. **Moodulaarsu**s - Iga plugin vastutab ühe konkreetse ülesande eest
5. **Arendaja kogemus** - Watch režiim jälgib failide muudatusi ja uuendab väljundit automaatselt

See seadistus muudab CSS-i kirjutamise lihtsaks ja hooldatavaks, pakkudes samal ajal modernse CSS-i võimalusi ja brauseritega ühilduvust, ilma et peaksid selleks käsitsi tööd tegema.


## PostCSS vs Sass: millal mida kasutada?

Kuigi PostCSS on tore tööriist, ei tähenda see, et Sass oleks halb valik. Mõlemal on omad tugevused:

**PostCSS plussid:**
- Võtad ainult need funktsioonid, mida vajad
- Saad kasutada tuleviku CSS-i omadusi
- Töötleb CSS-i kiiremini
- Saad luua oma pistikprogramme

**Sassi plussid:**
- Stabiilne ja laialdaselt kasutatav
- Sisseehitatud funktsioonid ja mixinid
- Lihtsam alustada
- Palju olemasolevaid teeke ja näiteid

Lisaks on Sass tõenäoliselt kasutusel just enamikus juba olemasolevates arendustes.

## Integreerimine build-tööriistadega

PostCSS-i saab ühendada populaarsete build-tööriistadega:

### Webpack

```javascript
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader',
          'postcss-loader'
        ]
      }
    ]
  }
};
```

### Vite

Vite'il on juba PostCSS tugi olemas. Lisa lihtsalt `postcss.config.js` fail ja Vite kasutab seda automaatselt.

### Next.js

Next.js toetab samuti PostCSS-i. Lisa `postcss.config.js` fail projekti juurkataloogi ja Next.js kasutab seda automaatselt.

## Kokkuvõte

PostCSS on paindlik tööriist, mis laseb sul kasutada tuleviku CSS-i omadusi juba praegu. Lihtne setup on kiire teha, aga annab sulle ligipääsu paljudele kasulikele funktsioonidele.

Kui oled algaja, soovitan alustada lihtsa seadistusega, mida siin kirjeldasin, ja siis järk-järgult lisada uusi pistikprogramme vastavalt vajadusele. Nii saad PostCSS-i võimalusi kasutada, ilma et peaksid kohe alguses liiga palju õppima.

Puhta CSS-i ja PostCSS-i kombinatsioon on hea viis kirjutada koodi, mis töötab kõigis brauserites ja kasutab uusimaid võimalusi.

*Illustratsioon: Midjourney  
Viip:  
"front-end developer/student in front of computer, waving hands, are very creepy, untrustfull, looking over the shoulders, drawn with bold, expressive lines typical of comic art: Style elements. --ar 16:9 --v 6.1*

