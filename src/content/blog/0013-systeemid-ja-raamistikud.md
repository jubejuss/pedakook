---
title: "CSS-raamistikud, komponentide teegid, disainisüsteemid, dokumenteerimise tööriistad ja UI-kitid"
description: "Mis vahe on disainisüsteemidel, raamistikel ja teekidel. Kus mida ja milleks kasutatakse"
pubDate: 'Oct 26 2024 18:38:00'
heroImage: '/frameworks.webp'
heroImageAlt: 'Front-end arendaja joob kohvi'
slug: 'disainisysteemid-ui-teegid'
---

Kaasaegses veebirakenduste arenduses on saadaval lai valik erinevaid tööriistu ja süsteeme, mis aitavad luua kasutajasõbralikke ja visuaalselt atraktiivseid rakendusi. Vaatame lähemalt, millised need on ja kuidas neid parimal viisil rakendada.

## Mis on disainisüsteem?

Disainisüsteem on kui digitaalne disainikeel – terviklik kogum reegleid, komponente ja juhiseid, mis määratleb, kuidas rakendus peaks välja nägema ja käituma. See hõlmab kõike alates värvipaletist ja tüpograafiast kuni interaktsioonimustrite ja kasutajakogemuse põhimõteteni.

Tuntumad disainisüsteemid on:

- [Google Material Design](https://m3.material.io/) - Google'i loodud disainisüsteem Android ja veebirakenduste jaoks
- [IBM Carbon Design](https://www.carbondesignsystem.com/) - IBM-i ettevõtte disainisüsteem
- [Salesforce Lightning](https://www.lightningdesignsystem.com/) - Salesforce'i platvormile loodud disainisüsteem
- [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) - Apple'i seadmete ja rakenduste disainisüsteem 
- [Microsoft Fluent Design](https://www.microsoft.com/design/fluent/) - Microsofti rakenduste ja Windows'i disainisüsteem
- [Atlassian Design System](https://atlassian.design/) - Atlassiani toodete disainisüsteem
- [Shopify Polaris](https://polaris.shopify.com/) - E-kaubanduse platvormile loodud disainisüsteem
- [Base Web](https://baseweb.design/) - Base web rakenduste disainisüsteem
- [Orbit Design System](https://orbit.kiwi.com/) - Kiwi.com'i reisindusrakenduste disainisüsteem

Üks parimaid ligipääsetavusele orienteerunud disainisüsteeme on [Gov.uk Design System](https://design-system.service.gov.uk/).

Disainisüsteemides on arendajad ja disainerid kulutanud tuhandeid tunde tööaega, et luua hästi töötavad, hea disaini, ligipääsetavuse reegeleid ja kasutajakogemust arvestavad lahendused, mistap oleks tark neist õppust võtta või neid kasutada.

## Komponentide teegid (UI Component libraries) – ehitusklotsid veebirakenduste loomiseks

Kui disainisüsteem on kui arhitekti joonised, siis komponentide teegid on kui valmis ehitusplokid. Need pakuvad arendajatele valmis UI elemente – nuppe, vorme, tabeleid ja palju muud. Effektiivne töö on selline, kus võimalikult väikese ressursikuluga teed võimalikult palju. Valmis komponentide teegid pakuvad just sellist võimalust. Endal jääb vaid pisut lihvida – muuta värve, raadiuseid võid suurusi vastavalt enda kavandatule.

Mõned tuntumad neist:

- [Material-UI (MUI)](https://mui.com/  )
- [Ant Design](https://ant.design/)
- [Chakra UI](https://chakra-ui.com/)
- [Shadcn/ui](https://ui.shadcn.com/)
- [Next UI](https://nextui.org/)
- [Headless UI](https://headlessui.com/)
- [Radix UI](https://www.radix-ui.com/)
- [React Bootstrap](https://react-bootstrap.github.io/)
- [Mantine](https://mantine.dev/)
- [Semantic UI](https://semantic-ui.com/)


Komponentide teekide kasutamine teeb arendamise palju kiiremaks. Selle asemel, et ise kõiki nuppe, vorme ja muid elemente nullist ehitada, saad kasutada juba valmis tehtud ja läbi testitud komponente. 

## CSS raamistikud

CSS raamistikud jagunevad kahte põhikategooriasse. Traditsioonilised raamistikud nagu Bootstrap pakuvad valmis komponente ja paigutusi, samas kui utiliidi-põhised raamistikud nagu Tailwind CSS keskenduvad väikestele, ühe-eesmärgilistele klassidele.

Tailwind CSS on viimastel aastatel tõusnud eriti populaarseks tänu oma paindlikkusele. Selle asemel, et pakkuda valmis komponente, võimaldab see kiiresti luua unikaalseid disaine läbi utiliidi-klasside. Bootstrap seevastu sobib hästi kiireks prototüüpimiseks ja lihtsamate veebilehtede loomiseks.  

Siinses kontekstis märgin, et css-raamistikud võivad olla kasutuses koos UI-teekidega, lihtsustades stiilimist. Osad UI-teegis kasutavad mõnd CSS-raamistikku.

Populaarsemad UI-teegid:

- **React UI teegid**
  - Material-UI (MUI)
  - Ant Design
  - Chakra UI
  - Shadcn/ui
  - Next UI
  - React Bootstrap
  - Mantine
  - Radix UI
  - Headless UI
  - React Suite
  - Grommet
  - Blueprint

- **Vue UI teegid**
  - Vuetify
  - Element Plus
  - Quasar
  - PrimeVue
  - Vue Material
  - Buefy
  - Naive UI

- **Angular UI teegid**
  - Angular Material
  - PrimeNG
  - NG-Bootstrap
  - Nebular
  - NGX-Bootstrap
  - Clarity Design

- **Universaalsed UI teegid**
  - Bootstrap
  - Foundation
  - Bulma
  - Semantic UI
  - UIkit
  - Materialize


## Kuidas valida õige süsteem?
Kogemustega arendaja teab ilmselt juba ise, kuidas valida õige süsteem.  Lihtne reegel peaks aga olema see, et süsteem, mis on sulle kõige tuttavam on ka kõõige parem. Õppimiseks võiks aga hoida silma peal trendidel, millest ja miks parasjagu räägitakse. Hetkel, oktoober 2024, tundub mulle huvi pakkuvad Chakra, Shad ja Headless UI.

Claude AI, aga kirjutas näiteks sellise selgituse:

**Suurte organisatsioonide projektidele** sobivad täielikud disainisüsteemid nagu Material Design või Carbon Design. Need pakuvad põhjalikke juhiseid ja tagavad järjepideva kasutajakogemuse läbi erinevate rakenduste.

**Keskmise suurusega projektidele** on head valikud komponentide teegid nagu MUI või Chakra UI. Need pakuvad head tasakaalu valmis komponentide ja kohandamisvõimaluste vahel.

**Väiksematele projektidele ja prototüüpimiseks** sobivad CSS raamistikud nagu Bootstrap või Tailwind CSS. Need võimaldavad kiiresti luua atraktiivseid veebilehti ilma liigse keerukuseta.

**Modernsete rakenduste** jaoks tasub kaaluda hübriidsüsteeme nagu Shadcn/ui või Next UI, eriti kui kasutate React'i või Next.js'i.

## Dokumentatsioon ja komponendid

Dokumentatsioon aitab:
- Uutel arendajatel kiiremini projekti sisse elada
- Vältida samu küsimusi korduvalt küsimast
- Hoida meeles, miks mingid otsused tehti
- Leida kiiresti vajalikku infot
- Vähendada vigu ja arusaamatusi
- Hoida koodi kvaliteeti

### Storybook – dokumentatsiooni standard

Storybook on muutunud UI komponentide arenduse ja dokumentatsiooni standardiks, pakkudes:
- Isoleeritud arenduskeskkonda komponentide loomiseks
- Interaktiivseid näiteid ja dokumentatsiooni
- Automaatset testimist ja visuaalse regressiooni kontrolli
- Head koostööd disainerite ja arendajate vahel

### Dokumentatsiooni sisu

- Selgitus, milleks komponent või süsteem mõeldud on
- Näited, kuidas seda kasutada
- Tehnilised detailid ja seadistused
- Võimalikud probleemid ja nende lahendused
- Infot selle kohta, kuidas komponenti muuta või edasi arendada

### Dokumenteerimise alternatiivid

1. Ladle
2. MDX + Next.js
3. Docusaurus
4. Histoire
5. Sandpack
6. Nextra

## UI-kitid
Nüüd, kus on juttu olnud disainissüsteemidest ja komponentide teekidest, jääb veel küsimus – mis on UI-kit?  
Tegelikult on mõneti kõik need kolm kokku langevad – paljud disainissüsteemid sisaldavad ka juba komponentide teeke ja UI-kit iseenesest võiks olla defineeritud sama moodi kui komponentide teek, ehk komplekt valmis disainitud komponente, stiilie ja tookeneid. Endale on mulle silma jäänud, et UI-kit on kasutusel pigem disainis, nt Figma failis loodud komponentide kogum. Leidsin ühe artikli, kus kirjeldatakse asja nõnda:  
"Disainisüsteem: See on terviklik juhend, mis sisaldab reegleid, põhimõtteid ja tööriistu, et tagada ühtne ja järjepidev disain kogu toote või brändi ulatuses. See hõlmab stiilijuhendeid, värvipalette, tüpograafiat ja muid visuaalseid elemente.  
Komponentide teek: See on kogum taaskasutatavaid UI-komponente, nagu nupud, vormid ja kaardid, mis on loodud vastavalt disainisüsteemi juhistele. Komponentide teek aitab arendajatel ja disaineritel kiiresti ja tõhusalt luua kasutajaliideseid.  
UI-kit: See on tööriistakomplekt, mis sisaldab erinevaid UI-komponente ja mustreid, mida saab kasutada disainiprotsessis. UI-kit võib sisaldada ka visuaalseid elemente, nagu ikoonid ja illustratsioonid, ning see on sageli saadaval erinevates disainitarkvarades, nagu Sketch või Figma."
Siin [link.](https://medium.com/@rushabhpathak/design-system-design-library-and-ui-kit-what-makes-them-different-fdf06efc98a1)

## Kokkuvõte

Õige disaini- ja arendussüsteemi valik võib oluliselt mõjutada projekti edu. Oluline on arvestada:
- Projekti suurust ja keerukust
- Meeskonna oskusi ja eelistusi
- Ajalist ressurssi
- Kohandamisvajadust
- Pikaajalise toe vajadust

Modernne veebirakenduste arendus liigub üha enam paindlike ja kombineeritud lahenduste poole. Traditsioonilised CSS raamistikud arenevad utiliidi-põhisteks, komponentide teegid muutuvad "headless" suunas ja hübriidsüsteemid pakuvad parimat mõlemast maailmast. Oluline on valida lahendus, mis sobib projekti vajadustega ja meeskonna oskustega.