---
title: 'Githubi ja VS Code seadistamine mitmete kasutajatega arvutis'
description: "Vaata kuidas seadistada Visual Studio Code ja Github'i töövoog ja kasutajainfo kui töötad arvutis, kus peale sinu veel kasutajaid."
pubDate: 'Oct 11 2023 18:45:00'
heroImage: '/lot-of-cats-like-github-meaning.jpg'
heroImageAlt: 'Hulk kasse nagu githubi versioonid'
slug: 'vscode-github-user'
---

Üks problemaatiline koht õpetajatöös on 30 arvutit, milliste taga 300 õpilast oma erinevate kontodega, mistap su isiklik kogemus normaalsest töövoost põrub alati. Reeglina on probleemide lahendused lihtsad, ent nad lahenevad just alles siis kui tund läbi saab.

## Probleem – ei saa oma muudatusi github'i üles lükata
Kloonid giti repo githubist, teed oma muudatused ära, teed `git add .` siis `git commit -m "sinu kommentaar"` ja `git push`... ja ei midagi, antakse teade, et:
```bash
error: The requested URL returned error: 403 Forbidden...
```
jne

Võimalik, et isegi ütleb, et sa tahad mingi võõra nime all muudatusi oma Githubi reposse lükata.

Ja siin on ka vastus – järelikult on kuskil salvestatud (eelmine kasutaja on salvestanud) teise kasutaja andmed, mida nüüd süsteem kasutab.

Kuna ma logisin VSCode's Githubi sisse siis ei tulnud selle peale, et sellest ei piisa ja et süsteem kasutab varem salvestatud salasõnu.

### Lahendus – kustuta eelmise Github'i kasutaja andmed

Lühidalt – kustuta süsteemist varem talletatud Githubi logimisparameetrid.

MAC'il ava Keychain, otsi üles githubi kirjed ja kustuta need. Seejärel saad VSCode kaudu Githubi sisse logides juba oma git'i vajalikud muudatused üles laadida.

Vindowsi puhul liigu `control panel > user accounts > credential manager > Windows credentials > Generic credentials` ja kustuta githubi sissekanded.

Peakski kõik olema.