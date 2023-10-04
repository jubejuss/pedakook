---
title: 'Kuidas seadistada Bootstrapis enda värvipalett?'
description: 'Bootstrap annab eelseadistatud värvi- ja stiilivaliku, kuid kui tahad rakenduse stiilida oma käe järgi, vajad veidi enamat. Seadista Bootstrap 5 värvipalett.'
pubDate: 'Oct 04 2023 18:45:00'
heroImage: '/bootstrap-5-color-palette.jpg'
heroImageAlt: 'Mees istub järveäärsel paadisillal ja vaatab sülearvutit'
slug: 'custom-bootstrap-colors'
---

Jätkame sealt kus pooleli jäime – [Kuidas installida custom bootstrap?](/blog/custom-bootstrap)

Bootstrap CSS raamistikuga arenduskeskkond on meil nüüd püsti, aeg on teha seda, mis plaanis – muuta värvipalett selliseks, mida meie disain ette näeb.

## Bootstrapi värviskeem
Bootstrapis ja see on ilmselt levinud värviskeem üldse, on värvid jaotatud nö funktsionaalsuse järgi nö muutujateks [vaata Bootstrapi värve Bootstrapi kodulehelt](https://getbootstrap.com/docs/5.3/customize/color/).

### Bootstrapi põhiskeemi värvide muutujate nimed:
* **primary** – disaini põhivärv, nö brandi värv
* **secondary** – sekundaarne ehk täiendvärv
* **tertiary** – madalama prioriteediga elementide värv, mis täiendab eelnevaid kuid ei konkureeri nendega.
- **body** – vaikimisi esiplaani ja tausta värv
- **dark**
- **light**
- **emphasis**
- **border**  
  
### Süsteemi värvid:
- **success** – tavaliselt roheline, teavitusteks kui mingid tegevused õnnestuvad
- **danger** – tavaliselt punane, ebaõnnestunud tegevused, vead.
- **warning**
- **info**

Viimasena välja toodud nö süsteemi värve ei ole tark vahetada, need on kasutajakogemuse mõttes aastate jooksul pika lokunud – me teame, et punane tähendab, et midagi on jama, roheline, et kõik on hästi.

## Bootstrapi värvipalett
Vaikimisi on Bootstrapi primaarvärviks sinine ja sekundaarseks värviks hall.
![Bootstrapi värvid](/bootstrap-colors.jpg)

Lisaks on Bootstrapis olemas valik värvipalette: [Bootstrapi lisavärvipaletid](https://getbootstrap.com/docs/5.3/customize/color/#all-colors)

## Oma värvid Bootstrapis
Loome oma värvidega Bootstrapi.

Esmalt sätime oma eelmises juhendis lodud arenduskeskkonna ümber selliseks, et iga juhend on omaette fail, millel ka sõltumatu scss fail. Nii saame hoida juhendid lihtsad. Kuna `index.html` fail sai juba eelmise juhendiga loodud, siis las ta jääb ja sinna võib lisada lingid teistele juhendite näidistele. Loome uue HTML-faili ja SCSS-i sellelel, kopeerides need eelmise juhendi failidest. Kopeerime ja nimetame need vastavalt `bootstrap-02.html` ja `bootstrap-02.scss`. Lisame `main.js`faili rea, mis impordib `bootstrap-02.scss`. 

Lisame `index.html` faili lingi `<a href="bootstrap-02.html">Bootstrapi värvide muutmine</a>` ja loodud `bootstrap-02.html`faili link indeks failile tagasi.

Et värvide muutmise effekt paremini ilmsiks tuleks, lisame lisaks olemasoleva nupu (eelmises juhendis loodud nupule) alla veel ühe. Sedapuhku sekundaarse nupu, ehk `<button class="btn btn-secondary">Secondary button</button>`

Pistame `h1` pealkirja ja esilehele viiva lingi `div`-i sisse ning lisame sellel konteinerile primaarse taustaväri ja teksti värvi muutva utiliitklassi `text-bg-primary`, 3rem-i paddingut `p-5`ja 1rem marginit alla `mb-3`.

H1 elemendile lisame ülesse ja alla 3rem-i marginit ning lingile värviklassi `link-light`

Nüüd võiks meie lehekülje sisuplokk näha välja umbes selline:
```html
<div class="container py-4 px-3 mx-auto">
  <div class="text-bg-primary p-5 mb-3">
    <h1 class="my-5">Tervist, Bootstrap ja Vite!</h1>
    <ul>
      <li><a class="link-light" href="index.html">Esilehele</a></li>
    </ul>
  </div>
  <button class="btn btn-primary">Primary button</button>
  <button class="btn btn-secondary">Secondary button</button>
</div>
<script type="module" src="./js/main.js"></script>
```
![bootstrap](/public/bootstrap-colors-2.jpg)

### Enda värvipaleti kasutuselevõtt
Järgmiseks avame `bootstrap-02.scss` faili ja impordime bootstrapi funktsiooid ja muutujad. Need read peame lisama faili algusesse, enne seal olevat bootstrapi importi:
```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
```
Ja nüüd võime muuta värve.

Anname muutujale `$primary` uue väärtuse. Nt Bootstrapis endas defineeritud muutuja `$indigo` ja anname muutujale `$secondary` enda loodud väärtuse `#F2E911`. Lisaks peame me Boottrapile oma tegevusest teada ka andma ja selleks lisame defineerie, et muutuja `$theme-colors` kasutab meie poolt määratud muutujaid.

Eelnevat kokku võttes, näeb meie `scss`fail välja nüüd selline:
```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";

$primary: $indigo;
$secondary: #F2E911;

$theme-colors: (
  "primary": $primary,
  "secondary": $secondary,
);

@import "~bootstrap/scss/bootstrap";
```
Ja nüüd näeb meie leht välja selline:
![Bootstrap muudetud värvidega](/public/bootstrap-colors-3.jpg)

Peamine, mille me sedapidi setupiga saavutame on see, et Bootstrapi funktsioonid loovad ise kõik vajalikud pooltoonid juurde – hover, active, focus – olekud, mis kõik on väikse toonierinevusega:
![Bootstrap muudetud värvidega olekud](/public/bootstrap-colors-4.jpg)

Nuppude olkute kohta olen ma pisut veel kirjutanud:
[milline on "õige" fookuse indikaator](https://vilejakell.studio/wcag-fookus-olek) ja [kui palju peaks hover state erinema tavalisest olekust](https://vilejakell.studio/hover-state-wcag)