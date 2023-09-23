---
title: 'Artikli või blogipostituse kirjutamine Astros'
description: 'Kuidas üldse Astos blogida. Vaata ja loe siit.'
pubDate: 'Sep 23 2023 10:30:00'
heroImage: '/astronaut_is_writing_blogpost.png'
slug: 'astro-blogisse-kirjutamine'
---

Suure hurraaga alustasin juhendamist, aga unustasin peamise – kuidas siinsesse blogisse kirjutada.

Siinse seadistuse puhul käib blogipostituse kirjutamine markdown failidesse, mis asuv `src` kataloogi `blog` alamkataloogis.

Kasutatud pildid asuvad `public`kataloogis.

Markdown faili frontmatterisse kirjutatakse kogu metainfi jms:  
```yaml
---
title: 'Artikli või blogipostituse kirjutamine Astros'
description: 'Kuidas üldse Astos blogida. Vaata ja loe siit.'
pubDate: 'Sep 23 2023 10:30:00'
heroImage: '/astronaut_is_writing_blogpost.png'
slug: 'astro-blogisse-kirjutamine'
---
```