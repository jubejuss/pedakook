---
title: 'Kuidas installeerida "custom" Bootstrap?'
description: 'Selleks, et kasutada oma käe järgi kohandatud Bootstrapi, tuleb oma arendusarvutisse paigaldada bootstrapi arenduskeskkond. Loe kuidas paigaldada Bootstrap 5.'
pubDate: 'Oct 03 2023 18:45:00'
heroImage: '/bootstrap-5-man-sitting-behind-computer.jpg'
heroImageAlt: 'Mees istub järveäärsel paadisillal ja vaatab sülearvutit'
slug: 'custom-bootstrap'
---

Olgugi, et arendusmaailmas on ammu moodsamaid termineid, on Bootstrap endiselt üks enimlevinud CSS-raamistikke. Seetõttu on ei ole sugugi paha teada, kuidas installida Bootstrap ja teda kasutada.

Kui ambitsioone muuta vaikimisi stiilidega Bootstrap millekski omanäoliseks pole, on asi lihtne – tuleb lihtsalt lisada Bootstrapi CDN-i lingid oma HTML-i ja ongi korras. [Bootstrapi kasutusjuhendid juhendid on leitavad Bootstrapi kodulehelt.](https://getbootstrap.com/docs/5.2/getting-started/introduction/)

Sellisel juhul saate täiesti korraliku kujundusega veebilehe. Lihtsalt, et tal puudub teie, originaalne nägu:
![Bootstrp 5 näidis](https://assets.startbootstrap.com/img/screenshots/templates/modern-business.png)
Joonis 1. Bootstrapi näidis. https://assets.startbootstrap.com/img/screenshots/templates/modern-business.png.

Teine lugu on aga siis kui tekib soov kujundada oma käe ja stiili järgi veebirakendus, mis kasutab küll Bootstrapi raamistikku, ent kus vävipalett on teie ja kasutusel on vaid täpselt niipalju CSS-koodi, kui vaja.

## Bootstrapi install

Ka oma arvutisse paigaldamise juhised on Bootstrapi lehel kenasti kõik olemas – [Bootstrapi enda arvutisse paigaldamise juhised](https://getbootstrap.com/docs/5.2/getting-started/vite/), ent tunni materjalina lisan põgusa ülevaate ka siia.

### Mida on Bootstrap 5 paigaldamiseks vaja

Esmalt peab arvutisse olema paigaldatud muidugi Node. Node olemasolu saad kontrollida Terminalis käsuga `node --version`. Node puudumisel saad node installeri laadida arvutisse siit: [Node installer](https://nodejs.org/en). Selle abil paigaldame arvutisse kõik vajalikud paketid arendustööks. Ja need on Vite, Sass ja muidugi Bootstrap ise koos @popperjs-iga.

Vite, hääldatakse /viit/, on front-end arenduskeskkond ja valmis koodi nö valmis paki komplekteerija (ma ei oska seda paremini seletada). Sass meie puhul SCSS on CSS-i eelprotsessori Sass (Syntactically Awesome Style Sheets) süntaks. Sass on skriptikeel, mis tõlgitakse CSS-iks, ja see pakub mitmeid funktsioone ja võimalusi, mida tavalises CSS-is pole või pole hiljutise ajani olnud, et muuta stiilide kirjutamine paindlikumaks, korraldatumaks ja võimsamaks.

### Bootstrap 5 installimine arendusarvutisse

Esmalt loome sobivasse kohta arvutis oma projektikausta.

Terminalis:
```bash
mkdir bs5-kooliprojekt && cd bs5-kooliprojekt
npm init -y
```
Eelnevate käskudega lõime me folderi `bs5-kooliprojekt` ja liikusime sellesse folderisse ning seejärel lõime käsuga `npm init -y` uue node projekti. See `-y` ütles lihtsalt kõikidele järgnevatele küsimustele jah. Kui soovite ükshaaval vastata, võib anda käsuks ka lihtsalt `npm init`.

Nüüd on meil `bs5-kooliprojekt`kaustas `package.json` fail, kus on kirjas projekti info, kuhu lisanduvad vajalikud käsklused ja installeeritud node moodulid.

Installime vite:
```bash
npm i --save-dev vite
```
Bootstrapi koos popperiga:
```bash
npm i --save bootstrap @popperjs/core
```
ja Sassi:
```bash
npm i --save-dev sass
```
Võite vaadata `package.json` faili, kus on näha alumises pooles lisandunud moodulid. Samuti on projekti kausta tekkinud folder `node_modules`.

JSON (JavaScript Object Notation) on kerge andmevahetusformaat, mis on loodud andmete struktureerimiseks tekstina. See on inimestele lihtne lugeda ja kirjutada ning masinatele lihtne analüüsida ja genereerida.

JSON-i põhielemendid on:

Objektid: Need on võtmega-väärtusega paaride kogumid, mis on ümbritsetud loogelistesse sulgudesse `{...}`. Näiteks: `{"nimi": "Kati", "vanus": 25}`

Massiivid: Need on väärtuste loendid, mis on ümbritsetud kandilistesse sulgudesse `[...]`. Näiteks: `["õun", "banaan", "kirss"]`

Väärtused: Need võivad olla stringid (topeltjutumärkides), numbrid, tõeväärtused (`true` või `false`), objektid, massiivid või `null`.

Kui me loome vaid HTML-lehe, siis võiks luua mõned lisakaustad ja failid, nii et meie projekti struktuur näeks välja selline:

```
bs5-kooliprojekt/
├── src/
│   ├── js/
│   │   └── main.js
│   └── scss/
│   |   └── styles.scss
|   └── index.html
├── package-lock.json
├── package.json
└── vite.config.js
```
Ehk, et meil on vaja luua `src` folder, milles on folder `js`koos failiga `main.js` ja folder `scss` failiga `styles.scss` ja `index.html` ja juurkataloogi `vite.config.js`.

`styles.scss` faili loome me kõik oma stiilid.

`main.js` faili kaudu impordime me arendusfaasis scss-i oma rakendusse.

Kiirelt ja korraga kõikide nende folderite ja failide tegemiseks jooksuta järgmisi käsklusi:
```bash
mkdir {src,src/js,src/scss}
touch src/index.html src/js/main.js src/scss/styles.scss vite.config.js
```
Järgmiseks tuleb konfigureerida `vite.config.js`.
Lisa `vite.config.js`faili järgmised read:
```javascript
const path = require('path')

export default {
  root: path.resolve(__dirname, 'src'),
  server: {
    port: 8080,
    hot: true
  }
}
```
See Vite javaskriptis konfiguratsioonifail määrab mõned arendusserveri seaded ja projekti juurkataloogi asukoha.

`const path = require('path')`: See rida impordib Node.js `path` mooduli, mille abil me saame järgmisel real näidata kus asub juurkataloog.
`root: path.resolve(__dirname, 'src')`: See määrab Vite projekti juurkataloogi asukoha. `__dirname` on Node.js globaalne muutuja, mis näitab praeguse skripti kataloogi absoluutset teed. `path.resolve` ühendab selle tee `src` kataloogiga, mis tähendab, et projekti juurkataloogiks on määratud `src`.
`server: { ... }`: See osa määrab Vite arendusserveri seaded.
`port: 8080`: See määrab, et server käivitub pordil 8080.
`hot: true`: See lubab "kuuma mooduli asendamise" (HMR - Hot Module Replacement). Kui see on lubatud ja teete koodis muudatusi, siis Vite uuendab automaatselt brauseris muudetud mooduleid ilma lehte täielikult laadimata. 

Kokkuvõttes määrab see Vite konfiguratsioonifail projekti juurkataloogi asukoha kui `src` kataloogi ning lubab jooksutada serverit pordis 8080.

Nüüd võiks midagi meie `index.html` faili kirjutada ja siis saaks hakata toimetama:

```html
<!DOCTYPE html>
<html lang="et">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Custom Bootstrap</title>
  </head>
  <body>
    <div class="container py-4 px-3 mx-auto">
      <h1>Tervist, Bootstrap ja Vite!</h1>
      <button class="btn btn-primary">Primary button</button>
    </div>
    <script type="module" src="./js/main.js"></script>
  </body>
</html>
```
Pööra tähelepanu, et faili jaluses on link `main.js` failile ja failis on kasutusel Bootstrapi klassid.

Järgmiseks peame lisama `package.json` faili `vite`skripti, mis meie rakenduse käima paneb. Kui pole kunagi varem node projektiga tegelenud, võib asi ehk natuke segane olla ja peab jälgima , et vigu sisse ei tuleks. Vaja on lisada sinna alla, kus asub rida `scripts`, vajalik Vite skript `"start": "vite"`. Test skripti võib sealt ka ära kustutada. Kui on mitu skripti rida, siis vaata, et read lõpeks komaga, välja arvatud viimane. Tulemus koos eelnevaga võiks näha välja selline:
```js
{
  "name": "bs5-kooliprojekt",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    // lisatud Vite käivituskäsk
    "start": "vite"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "sass": "^1.68.0",
    "vite": "^4.4.10"
  },
  "dependencies": {
    "@popperjs/core": "^2.11.8",
    "bootstrap": "^5.3.2"
  }
}
```
Ja nüüd võiks meie rakenduse käima panna.

Node projekti jooksutamise käsklused näevad välja nii, et esmalt antakse käsk `npm`(Node package manager), siis `run` ja siis konkreetne käsklus või skript `package.json`ist. Hetkel siis nõnda:
```bash
npm run start
```
Selle peale näitab terminal, et aadressil `http://localhost:8080/`saab meie lehte näha.

Esialgu on see stiilimata, kuna me ole stiile faili linkinud:
![Bootstrap enne css-iga ühendamist](/bootstrap-5-01.jpg)

Järgmiseks ühendame Bootstrapi rakendusega, selleks konfigureerime `vite.config.js` faili moel, et Vite teaks, kus Bootstrap asub. Selleks lisame blocki, mis ütleb kus asub Bootrap ja kuidas Vite selle kätte saab, see võimaldab importida `node_modules` kaustas oleva Bootstrapi koodi:
```javascript
const path = require('path')

export default {
  root: path.resolve(__dirname, 'src'),

  // lisame Bootstrapi osa
  resolve: {
    alias: {
      '~bootstrap': path.resolve(__dirname, 'node_modules/bootstrap'),
    }
  },
  //

  server: {
    port: 8080,
    hot: true
  }
}
```
Nüüd võime Bootstrapi importida meie `styles.scss` faili:
```scss
// Import all of Bootstrap's CSS
@import "~bootstrap/scss/bootstrap";
```
ja seejärel impordime sassi ja bootstrapi ka `main.js` faili:
```javascript
// Import our custom CSS
import '../scss/styles.scss'

// Import all of Bootstrap's JS
import * as bootstrap from 'bootstrap'
```
Ja kui nüüd vaadata meie veebilehte, ongi seal juba Bootstrapi stiilides leht:
![Bootstrap css-iga ühendatult](/bootstrap-5-02.jpg)

Nüüd võiks oma lehele Bootstrapi harjutamiseks luua rohkem sisu – navigatsiooniriba koos menüüga `main` sektsiooni ja jaluse.

Fikseeritud laiusega konteineri, kolme veeruga kujunduse, mis mobiilivaates muutub üheks ja millises igas veerus on üks kaart.

[Vaata Bootstrapi tutvustust W3school.com'ist](https://www.w3schools.com/bootstrap5/index.php)

Selle tutvustuse loomiseks koos läbikatsetamisega kulus ca 4h.

Järgmisena hakkame vaatama, kuidas muuta stiilid oma disaini järgi ja miks on seda lihtsam teha oma arvutisse paigaldatud Bootstrapi arenduskeskonnas.