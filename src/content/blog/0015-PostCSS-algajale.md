---
title: "Kui juba, siis juba – ehk PostCSS Sassi asemel"
description: "Kuigi Bootstrapis on veel Sass sees, siis hetkel kasutavad moodsad arendused pigem puhast CSS-i. See siiski vajab veel mõnd vidinat"
pubDate: 'March 14 2025 16:50:00'
heroImage: '/computer-sciences-teatcher.webp'
heroImageAlt: 'hirmul-arendaja.webp'
slug: 'postcss-algajale'
---

**PostCSS: Lihtne setup algajale**

CSS-i kirjutamine on aastate jooksul muutunud. Varem oli kiiremaks css-i kirjutamiseks Sass või Less, aga viimastel aastatel on taas pigem CSS teemaks. Esiteks on CSS ise muutunud, saab kasutada muutujaid ja osaliselt ka nestingut ning importida teisi css-failie, ent puuduvaks funktsionaalsuseks on vaja nats veel. Selleks on PostCSS. Vaatame, kuidas seada üles lihtne PostCSS keskkond, mis muudab arenduse kiiremaks.

## Mis on PostCSS?

PostCSS on tööriist, mis muudab sinu CSS-i JavaScripti abil. Erinevalt Sassist või Lessist pole PostCSS ise eelprotsessor, vaid pigem raamistik, mis laseb sul kasutada erinevaid pistikprogramme (plugin'e), et oma CSS-i täiendada.

Lihtsamalt öeldes:
- Sass/Less lisavad CSS-ile uusi võimalusi (muutujad, mixinid jne)
- PostCSS muudab sinu CSS-i vastavalt sinu vajadustele

PostCSS'i head küljed:
- Võtad ainult need pistikprogrammid, mida päriselt vajad
- Töötleb CSS-i kiiremini kui teised tööriistad
- Saad luua oma pistikprogramme või valida sadade olemasolevate seast
- Võimaldab kasutada tuleviku CSS-i omadusi juba praegu

## Lihtne PostCSS setup

Alustame kõige lihtsama PostCSS seadistusega, mis laseb sul kasutada tuleviku CSS-i omadusi ja lisab automaatselt vajalikud prefiksid.

### 1. Vajalikud paketid

Kõigepealt installime vajalikud npm paketid:

```bash
npm install --save-dev postcss postcss-cli autoprefixer postcss-preset-env
```

Mida need paketid teevad?
- `postcss` – põhipakett CSS-i muutmiseks
- `postcss-cli` – käsurea tööriist PostCSS-i kasutamiseks
- `autoprefixer` – lisab automaatselt vajalikud vendor-prefiksid (nt `-webkit-`, `-moz-`)
- `postcss-preset-env` – võimaldab kasutada tuleviku CSS-i omadusi

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

Autoprefixer vajab teadmist, milliseid brausereid peab toetama. Selleks lisame `package.json` faili järgmise osa:

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

Nüüd lisame `package.json` faili skriptid CSS-i töötlemiseks:

```json
"scripts": {
  "css": "postcss src/css/style.css -o dist/css/style.css",
  "watch:css": "postcss src/css/style.css -o dist/css/style.css --watch"
}
```

Need skriptid teevad:
- `npm run css` – töötleb CSS-i ühe korra
- `npm run watch:css` – jälgib CSS-i muudatusi ja töötleb neid automaatselt

## PostCSS kasutamine praktikas

Nüüd, kui seadistus on paigas, vaatame, kuidas PostCSS-i päriselt kasutada.

### CSS-i pesastamine

Üks populaarsemaid PostCSS funktsioone on CSS-i pesastamine, mis laseb sul kirjutada selektoreid hierarhiliselt, sarnaselt Sassile:

```css
/* Enne (tavaline CSS) */
.card { background: white; }
.card .title { color: blue; }
.card .body { padding: 1rem; }
.card .body p { margin-bottom: 0.5rem; }

/* Pärast (PostCSS nesting) */
.card {
  background: white;
  
  & .title {
    color: blue;
  }
  
  & .body {
    padding: 1rem;
    
    & p {
      margin-bottom: 0.5rem;
    }
  }
}
```

### Tuleviku CSS-i omadused

PostCSS Preset Env laseb sul kasutada mitmeid tuleviku CSS-i omadusi:

```css
/* CSS muutujad */
:root {
  --primary-color: #3490dc;
}

/* Arvutused calc() funktsiooniga */
.container {
  width: calc(100% - 2rem);
}

/* CSS Grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
}

/* Logical Properties */
.box {
  margin-inline: 1rem;
  padding-block: 0.5rem;
}
```

## Kasulikud PostCSS pistikprogrammid

Lisaks põhiseadistusele on olemas palju PostCSS pistikprogramme, mis teevad su töö lihtsamaks:

- **postcss-import** – võimaldab kasutada `@import` käsku failide ühendamiseks
- **cssnano** – vähendab CSS-i faili suurust tootmiskeskkonnas
- **postcss-nested** – alternatiivne pesastamise süntaks
- **postcss-custom-media** – lisab toetuse kohandatud meediapäringutele
- **postcss-color-function** – lisab CSS-i värvi funktsioonid

Nende lisamiseks tuleb need kõigepealt installida:

```bash
npm install --save-dev postcss-import cssnano
```

Ja seejärel lisada `postcss.config.js` faili:

```javascript
module.exports = {
  plugins: [
    require('postcss-import'),
    require('postcss-preset-env')({
      stage: 1,
      features: {
        'nesting-rules': true
      }
    }),
    require('autoprefixer'),
    process.env.NODE_ENV === 'production' ? require('cssnano') : false
  ].filter(Boolean)
};
```

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

Paljud arendajad kasutavad neid koos – kirjutavad Sassis ja töötlevad tulemust PostCSS-iga.

## Integreerimine build-tööriistadega

PostCSS-i saab lihtsalt ühendada populaarsete build-tööriistadega:

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

