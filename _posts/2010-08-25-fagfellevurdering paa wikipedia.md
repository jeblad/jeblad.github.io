---
layout: post
language: nb
date: 2010-08-25 20:00:00 (CET)
title: Fagfellevurdering på Wikipedia
tagline: fagfelle innenfor Wikipedias eksisterende rammer
description: Er det mulig å gjøre fagfellevurdering av innhold på Wikipedia, uten å endre rammebetingelsene?
authors:
  - jeblad
categories :
  - encyclopedia
tags: wikipedia, fagfelle, peer review
licenses:
  - CC-BY-SA-4.0
---

Det er mulig å få en form for fagfellevurdering til å fungere på Wikipedia uten alt for store og gjennomgripende endringer. Det er til og med mulig å få til en løsning som fungerer *bedre* enn tradisjonell fagfellevurdering. De nødvendige endringene er moderate og vil ha liten betydning for brukeres mulighet til å bidra i et levende leksikon.

<!--mer-->

### Konstant feilrate

Når noen skriver et innlegg på Wikipedia så formidler denne personen kunnskap slik han eller hun selv oppfatter den. Dette har både fordeler og ulemper. Fordelene er hovedsakelig at formidlingen skjer raskt, ulempen er hovedsakelig at formidlingen inneholder feil i personens forståelse av kunnskapen. En andel av leserne vil oppdage feilene, men i prosessen skriver de inn sine egne feiloppfatninger sammen med annen ny tekst. Fordi dette er kontinuerlige prosesser så vil den formidlede kunnskapen etterhvert inneholde en konstant andel feilaktig informasjon som er fremstilt som sannferdig kunnskap. Dette er beskrevet i artikkelen [Feilretting på Wikipedia](http://nettdugnad.origo.no/-/bulletin/show/589117_feilretting-paa-wikipedia) og i artikkelen [Crowdsourcing og peer review](ttp://nettdugnad.origo.no/-/bulletin/show/588542_crowdsourcing-og-peer-review.)

Det vi trenger er noe som endrer prosessen slik at vi øker sjansen for at gode korreksjoner overlever og senker sjansen for at det samme skjer med feil.

### Synlig fagfellevurdering av reviewers

Vi vet ikke hvem som er faglig sterke på de enkelte områdene, men vi vet at noen er villige til å gjøre en vurdering av andres arbeid. Det kan være flere forhold som er grunnen til at de vil dette, kanskje er de fagpersoner på området eller kanskje de skal bruke materialet i en sammenheng hvor de må kvalitetssikre det. Noen av disse er villig til å si hvem de er og dermed vet vi at de er villig til å sette sin faglige autoritet bak vurderingen. Andre av dem vet vi ikke hvem er, men ved å sammenligne med arbeidet de gjør så kan vi si noe om de faglige evnene. For alle gjelder at vi kan bruke *web of trust* for å finne ut hvem som går god for hvilken andre.

Når disse brukerne vurderer en revisjon så sier de om de går god for det som står der, de gir en global vurdering av revisjonen. De har også mulighet til å merke deler av teksten som ekskludert fra denne globale vurderingen. Disse ekskluderte delene kan knyttes til egne kommentarer.

I prinsippet så *godkjennes* teksten, en tekst som er underkjent er å anse som beheftet med feil. Visuelt fremstår godkjent tekst på normalfarget bakgrunn, mens underkjent tekst får en bakgrunn som signalerer at teksten er feil.

### Fortsatt bearbeiding av skribenter

Når skribenter fortsetter å gi bidrag til teksten så blir denne teksten merket som *ukjent* og vil relatere til siste fagfellevurderte versjon. Det er typisk to former for merking som er aktuelle, er noe lagt til eller er noe trukket ifra. Ved endringer så kan begge former vises. Dette blir dermed en form for inlinediff. Metoden er allerede kjent fra Mediawiki som *fancy diff*.

Artikkelvisning vil ikke låses på versjonen som har gått gjennom fagfellevurdering. Den vil hele tiden være siste versjon, men det vil vises hva som er endringene i forhold til denne versjonen.

Personen som gjør fagfellevurderingen vil komme i en situasjon hvor han forhandler med forfatteren om hva som er riktig kunnskapsforståelse. Det gjør at forfatteren får en mulighet til å modifisere sin egen kunnskapsforståelse. Vi har dermed oppnådd å ta et snitt mellom forfatterens og reviewers kunnskapsforståelse og vi får en feilreduksjon.

### Kollektiv fagfellevurdering

Ved at endringene er synlige for lesere av artikkelen så vil den visuelle eksponeringen av mulige feil øke. Når denne øker så går sjansen opp for at noen vil påvise feil og mangler i denne teksten. Disse kan da rette feilene, eller om vi knytter inlinediffene til et enkelt menysystem så kan de si hvilken av alternativene som er riktig. Hvis det er enkelt å angi hvilken versjon som er riktig så vil antakelig flere være villig til å si hva de mener enn om de må inn på diskusjonssiden for å angi dette.

Leserne sier ikke bare noe om hva som er riktig ved å angi det i artiklene, de sier også noe om hva de mener når de leser en artikkel og *ikke* merker en endring som feil. Denne mekanismen er mye svakere enn å angi dette eksplisitt, men fordi antall lesere er veldig stort så vil det en slik prosess konvergere raskt.

Når prosessen har akkumulert tilstrekkelig konfidens for at endringen er god så fjernes inlinediffen.

Det er ønskelig med noen mekanismer for å hindre forfattere i å stemme på egne endringer. En enkel mekanisme er at stemmer kun kan gis fra andre domener/masker enn det forfatteren bruker, og kanskje at det må gis fra flere forskjellige domener/masker.

### Rollen som reviewer

Det er flere aktuelle mekanismer som er aktuelle for å angi hvem som kan opptre i en rolle som reviewer. På Wikipedia er slike roller tildelt eksplisitt, men ønsket er ikke at noen får en slik rolle som en popularitetsmåling – den skal ideelt sett være et uttrykk for faglige evner. En faglig vurdering er imidlertid vanskelig å få til i praksis.

Hvis vi ser på hva vi er ute etter så ønsker vi å få et snitt mellom kunnskapen til flere brukere istedenfor at kun en enkelt forfatter formidler sin kunnskapsforståelse uimotsagt. Det gjør at vi ikke trenger å identifisere en persons faglige kunnskaper, vi trenger kun en person som kan tre inn i rollen og gjøre en noenlunde god jobb. Selvfølgelig vil det være ønskelig med en faglig sterk person, men modellen fungerer om reviewer er faglig svak – om enn ikke så godt som den kunne.

Dette gjør at vi identifiserer personen istedenfor de faglige evnene. Vi sier at brukere kan identifisere seg i systemet, de får da tilgang til å oppgi fullt navn. Samtidig får de tilgang til å merke artikler som fagfellevurdert, bare ikke de artiklene de selv har skrevet på.

Denne modellens sterke side er at reviewers vil bli veldig bevist sin egen rolle, ikke minst da deres navn vil være synlig. Dette gjør at de vil legge arbeid å gi en god og fullstendig vurdering.

### Forenkling

De som gjør review er igrunnen ikke noe annet enn andre personer enn forfatteren. Vi kan derfor tenke oss et system hvor noen blir gitt muligheten til å gjøre en forenklet fagfellevurdering (et review) når de ikke har bidratt på artikkelen. Det vi ønsker er å skape et snitt av kunnskaper, hvoretter andre lesere bringes inn for å løse opp tvetydigheter.

Flere kriterier må til i kombinasjon for å hindre brukere i å gi vurderinger på egne bidrag. Brukere kan tenkes å bytte IP-adresse, de kan slette lagrede cookies og så videre. En måte som er nokså effektiv er å introdusere en sperretid etter vesentlige bidrag før en anonym review kan gjøres, og deretter trekkes det tilfeldig en tillatelse til å gjøre et lite antall review hvis den anonyme har lest et gitt antall artikler og nettleseren har gjestet Wikipedia tilstrekkelig lenge. Resultatet er at det er uforutsigelig for skribenter å få tilgang til review-grensesnittet og det å forsøke å få slik tilgang vil komme med en kostnad.

Vi kan gjøre det enda bedre ved å begrense den forenklede fagfellevurderingen til å angi konkrete problempunkt i artikkelen. En forfatter skriver utfra egne kunnskaper og vil normalt ikke skrive inn noe han vet er feil. Han kan være usikker på hva som er riktig og kan da tenkes å ville bruke et slikt grensesnitt, men normalt vil han ikke ønske å angi feil i sin egen tekst.

I dette tilfellet kan vi lage en løsning som legger til kommentarer om uklarheter i teksten, vi underkjenner teksten med en kommentar og lar andre stemme over dens riktighet. Disse reviewerne kan bare utvide settet av underkjente tekstfragmenter, de kan ikke selv godkjenne teksten.

### Sammendrag

Ved å gjøre det enkelt og effektivt å godkjenne, underkjenne eller legge til kommentarer om deler av teksten så oppnår en å finne frem til snitt av kunnskap mellom en gruppe forfattere og en gruppe reviewers. Det virker endatil som en kan trekke leserne inn i en rolle som reviewers og dermed øke feilrettingen drastisk, og dette uten at den ordinære innholdsproduksjonen blir skadelidende.

Til forskjell fra andre systemer for kvalitetskontroll så er løsningen ikke basert på kunnskap om forfatteren og dennes kunnskaper, men på at grupper av involverte brukere skal ha samme kunnskapsforståelse. Fordi det er uvanlig at mange deler samme feilaktige kunnskapsforståelse så oppnås det en reduksjon av sannsynligheten for at feil overlever og at nye feil skrives inn.
