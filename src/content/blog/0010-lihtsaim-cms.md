---
title: 'Kuidas teha ise väiksemahuline Wordpressi alternatiiv'
description: "Loe kuidas selle asemel, et väiksemahulise veebi jaoks luua Worpressi leht, teha staatilise lehe generaatori, git'i ja markdowni tekstiredaktori abil lihtne CMS"
pubDate: 'Oct 27 2023 18:45:00'
heroImage: '/content_management.png'
heroImageAlt: 'Hulk kasse nagu githubi versioonid'
slug: 'lihtsaim-cms'
---

Mind ja ilmselt veel mõnda analoogsel tasemel veebiapusserdajat kipub kimbutama üks probleem – nö "all-in-one" lahendused on pisikeste projektide jaoks ebamõistlikult suured.

Näiteks on mul vaja kliendile luua veebileht mis koosneb vaid esilehest ja veel kahest sisulehest, nt meist ja kontakt vms. Selleks panen ma püsti mahuka [Wordpressi](http://wordpress.org) või [Drupali](http://drupal.org), milleks on mul vaja rentida server, luua arendusarvutis arendussüsteem, hallata andmebaasi, uuendada mooduleid, uuendada PHP-d, hoida pidevalt kogu asja silma peal, et lehte ära ei häkitaks, installida mingeid pluginaid jne, jne.

See on tüütu ja kallis.

## Kuidas teha väiksemahuline, oma disainiga, veebis hallatav veebileht
Ei ole probleemi, kui valdad HTML-i, CSS-i ja JavaScript'i ja teed lehe iseendale, siis võidki lihtsalt HTML-i meisterdada ja kogu lugu. Ei ole väga pointi isegi mingit peent Front-endi süsteemi kasutusele võtta. Iseasi kui tead, miks ja milleks.   
Aga kui sa ei tee endale, kui sul on vaja teha kliendile ja moel, et klient – veebiarenduse võhik – suudaks valmis lehel pisimuudatustega hakkama saada?

Mul on endal töökogemus Drupali ja Wordpressiga.  

On olemas nö "flat-file" tüüpi, andmebaasivabad lahendused, nagu [GravCMS](https://getgrav.org) ja [Pico](https://picocms.org). Grav'iga olen teinud mõned lehed ja väga hea lahendus, kui tahad MySQL andmebaasid oma arendusest välja jätta. Siiski eelpoolkirjeldatu jaoks liig.

Lihtsamat oleks vaja.  

Siinne leht on ehitatud statiliste lehtede generaator [Astroga](https://astro.build/), mille sisu luuakse Markdown keelt kasutades ja genereeritakse ümber staatiliseks leheks. Kogu arendus istub lisaks kohalikul arendusmasinale ka [Githubis](https://github.com/jubejuss/pedakook). Hetkel kirjutan sisu oma arendusarvutis ja "pushin" muudatused Githubi, kust omakorda [Cloudflare](https://www.cloudflare.com) automaatsed tööseadistused sellest staatilised lehed genereerivad. Kirjutasin sellest mõne sõnaga [Astro "livesse" laskmise postituses](https://pedakook.wtf/blog/veebi-livesse-laskmine/).

Tekkis mõte, et idee poolest võiks ju olla mingi lahendus, kuidas Markdowni töödelda otse veebis. ([Markdownist kirjutasin mõne sõnaga siin](https://pedakook.wtf/blog/astro-algsetup/#markdown)). Jah muidugi, seda saaks teha otse Githubis, mh ka läbi Visual Studio Code veebieditori, ent vaja oli midagi, mis oleks tavakasutajale arusaadav.  

Ja pärast mõningat otsingut ning kolleeg Kaspar-Martini soovitust ka leidsin, esmalt [Stackedit](https://stackedit.io/), mis on ok, aga seejärel juba [Readmestack][https://www.readmestack.com/], mis on täpselt see, mis vaja. Mõlemad ühilduvad Githubiga, teine on lihtsam mõneti kasutaja silmasõbralikum ja lihtsam.
![Readmestack kuvatõmmis](/readmestack.jpg)

## Millised on miinused?
Kindlasti on markdown editor pisut puine võreldes nt CKEditori või Guttenbergiga. St juhul kui sa oled eelnevatega harjunud.

Readmestackis puudub piltide üleslaadimise võimalus, mis on Wordpressil ja Drupalil. Seega peaks lisaks seadistama mingi pildihoidla. Nt Google Drive või Google Photos vms. Hea oleks kui seal oleks kasutada ka mingi piltide parajaks lõikamise tööriist.

Parajad piltide suurused tuleks lehe arendamise käigus välja mõelda. Pildihoidlad, millistel on ka lihtsad elementaarsed pilditöölusvahendid, leiab googledades kiirelt. [Näiteks siin üks artikkel tasuta ja tasulistest pildihpidlatest.](https://expertphotography.com/best-free-image-hosting/).

Aga mõistlik on võtta ilmselt mingi kõige lihtsam, nt Google Photos on täitsa ok.

## Kui mõistlik selline lahendus on?
Raske öelda, peab mõne kliendiga proovima, aga kuna lõpptulemusena on tegemist staatilise lehega, on viiruste võimalus nullilähedane. Erinevalt Wordpressist, mida pidvalt rünnatakse. Seega võiks klient siit raha kokku hoida küll.

Nii väikese lehe võiks muidugi Astro asemel nt Eleventyga teha. Teen selle kohta peagi postituse.


