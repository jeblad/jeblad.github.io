---
layout : post
language : nb
date: 2010-09-21 15:00:00 (CET)
title : Automatisk lenking til Wikipedia
tagline : og kanskje tagging, lenking og innbygging av lignende innhold
description: Automatisk lenking til bakgrunnsmateriale .
authors:
  - jeblad
categories : encyclopedia
tags : linking, tagging, lemmatizing, stemming, embedding, mashup
licenses:
  - CC-BY-NC-ND-4.0
---

Mange har sett de nokså fascinerende løsningene som har dukket opp som gjør det mulig å lenke opp en tekst automatisk eller halvautomatisk. Noen av de mest interessante systemene gjør det mulig å få til slik lenking ikke bare til Wikipedia, men til aktuelle artikler på nettet. Funksjonaliteten til de mest avanserte løsningene er det ikke så lett å gjenskape, men kanskje er det mulig å få til litt av dem. Og kanskje vi kan få til noen nye og spennende løsninger.

<!--more-->

Våren 2010 ble jeg spurt av et selskap om det var mulig å få til noe slikt. De ønsket seg en løsning som gjorde det mulig å lenke opp aktuelle fraser i en tekst slik at de pekte på riktig artikkel i Wikipedia. Tilsynelatende er problemet nokså enkelt, men det er en del [snags](http://en.wikipedia.org/wiki/Driftwood) i farevannet. Det er problemer med ord som er bøyd, noen ganger brukes det synonymer, det kan være flere artikler på Wikipedia med samme tittel, og så videre.

Under arbeidet med forprosjektet ble det klart at flere så på samme problemet. Litt morsomt er det at nesten samme løsning er lagd av en annen leverandør for det samme selskapet. Selv om lenkingen skulle gå til forskjellige typer dokumenter så var store deler av løsningen den samme. På noen punkt var den ene løsningen bedre, på noen punkt var den andre løsningen bedre. Samtidig så ble det kjent at andre selskaper hadde litt avvikende ønsker og behov, men i grove trekk var det grunnleggende problemet det samme; *hvordan [lenke](http://en.wikipedia.org/wiki/Hyperlink), [tagge](http://en.wikipedia.org/wiki/Tag_cloud) eller [bygge inn](http://en.wikipedia.org/wiki/Mashup_%28web_application_hybrid%29) informasjon fra oppslagsverk i en brødtekst*.

Det er flere problemer som må løses. På overflaten må det identifiseres hvilken termer som kan brukes, dernest må en finne ut hvilken oppføringer (artikler) disse relaterer til og så må en velge en presentasjonsform. Nede i koden blir dette en god del mer komplekst.

### Løsningen

Det er mange aktuelle teorier og resultater om hvordan det her kan løses. Disse er såpass veldokumentert at det er mulig å gjøre en implementasjon på bakgrunn av dem. Utfra hva som vurderes som viktig så kan implementasjonene gis litt forskjellig vinkling og betoning, slik at en får forskjellige resultater. En kan bruke [lemmatisering](http://en.wikipedia.org/wiki/Lemmatisation) eller [stemming](http://en.wikipedia.org/wiki/Stemming), en kan ranke alternative fraser for hvorvidt de skal lenkes eller ikke etter [entrofi](http://en.wikipedia.org/wiki/Entropy_%28information_theory%29) eller [tf-idf](http://en.wikipedia.org/wiki/Tf-idf) eller helt andre mål og en kan sjekke om konteksten til lenkene stemmer med innholdet til artikkelen det lenkes til med [korrelering](http://en.wikipedia.org/wiki/Correlation_function) eller andre mål for [coincidence](http://en.wikipedia.org/wiki/Coincidence).

Kanskje viktigere er hva en bruker lenkingen til. Diskusjonene med selskapet startet med et ønske om å påvise ord og fraser som kunne brukes som tags. Dette er et nokså enkelt problem hvor retting av feil hovedsakelig består i å godkjenne de valgte termene. Det er flere som leverer slike løsninger for bloggverktøy, og forskjellene er for en stor del drevet av krav til nøyaktighet og hvorvidt det underliggende systemet klarer å levere tilstrekkelig gode resultater. Hvis det underliggende systemet leverer for dårlige resultater så må brukergrensesnittet være effektivt å jobbe med for å rette feilene, hvis det underliggende systemet returnerer svært gode resultater så kan kanskje brukergrensesnittet forenkles eller fjernes helt.

[![Figuren viser en lenkedialog.](/assets/images/linking/automatic-linking_250x136.png "Skjermdump av lenkedialog")](/assets/images/linking/automatic-linking_1024x1024.png)

Det neste det ble sett på var om vi kunne få til lenker til de aktuelle artiklene. Et grafisk grensesnitt for å godkjenne slik lenking er noe mer kompleks, men i Wikipedia kan vi tenke oss at lenkedialogen i den nye [WikiEditor](http://www.mediawiki.org/wiki/Extension:UsabilityInitiative#WikiEditor) endres slik at det er mulig å velge i en liste av anbefalte lenker. Dette kan også utvides slik at en kan steppe forover og bakover i lista av anbefalte lenker. Hvis ord og fraser mangler lenkemerking så settes det på om brukeren trykker «Ok» etter at parametre er automatisk fylt ut. Samtidig så må systemet passe på at lenker plasseres første gang et ord eller frase brukes. Andre systemer enn Mediawiki vil måtte ha en litt annerledes editor. Dagens dialogboks er ikke spesielt hjelpsom med å sette på lenking, enig?

Det tredje kom fra en helt annen kant. Et annet firma ville vite om det var mulig å legge til små ingresser fra Wikipedia i en høyremarg ved siden av deres artikler. Problemet de har er at alt må være helautomatisk. Kvaliteten på utvalget må derfor være eksepsjonelt godt, feil må helst ikke forekomme men det er kanskje ikke nødvendig å ha fullt så mange lenker som i de tidligere utgavene. Vi kan ha mange false negatives (forkastede artikler som skulle vært med), men må ha få false positives (artikler som er feilaktig inkludert og som skulle vært kastet). Samtidig så må en kunne trekke ut ingresser for denne løsningen, ikke spesielt vanskelig men det øker den totale kompleksiteten.

### Redefinering av problemet og ny løsning

Så var det tilbake til første selskap. De hadde i mellomtiden kommet opp med et ønske om å kunne lenke til tekst som har definisjoner inne i artiklene. Problemet med slikt er dels å påvise definisjonene og dels at Wikipedia mangler interne ankere utover mellomtitler, slike finnes bare i begrenset grad på nettsteder. Resultatene som er oppnådd i forskningsarbeid er gjennomgående nokså dårlige så jeg sa at nei, noe slikt får vi ikke til for da må vi endre målartikkelen i Wikipedia. Så begynte jeg å tenke; vi får det ikke til nå men hva om vi gjør det samme som [Columbia Newsblaster](http://newsblaster.cs.columbia.edu/), vi kan lage en løsning som lager et sammendrag om samme temaet som omtales i den aktuelle setningen i kildeteksten. Vi har da et system som ikke peker direkte til et anker internt i målteksten, vi har et system som kan lage et sammendrag om samme omtalte tema. Dette sammendraget kan vi vise i kildeteksten, deretter overlater vi vurderingen av hvorvidt sammendraget understøtter kildeteksten til leseren. Er det en artikkel på Wikipedia med tilstrekkelig god ingress, fint, hvis ikke så lages et sammendrag on the fly.

### Hva nå?

Både tagging av en tekst og lenking er veldig likt hverandre, forskjellene består i hvordan resultatene av den underliggende algoritmen blir brukt. På engelsk er [OpenCalais](http://www.opencalais.com/) med forskjellige tilpasninger i verktøy slik som [Zemanta](http://www.zemanta.com/) det som er mest kjent. Bare synd at disse verktøyene fungerer såvidt dårlig på norsk.

Det som dukket opp når vi redefinerte problemet er langt mer spennende enn kun en litt dum lenking, men klarer vi å lage noe slikt? Det er allerede slike systemer på engelsk, men ingen har lagd noe slikt på norsk. Fordelene er mange, og spennende, samtidig som vi vet det er flere bruksområder.

Hver enkelt av løsningene kan brukes som de er, men det nære slektskapet mellom dem gjør det fristende å se på om flere selskaper og aktører er villig til å gå for en felles løsning. En aktør har kanskje behov for å lenke til Wikipedia, en annen til Store Norske, en tredje sitter med et spesialisert oppslagsverk i musikk og vil lenke til dette, mens en fjerde kanskje ønsker å bruke alle. Hvis vi får mange nok interessert så kan vi gå for det vanskelige problemet, automatiske sammendrag på norsk om aktuelle tema. Det hadde virkelig vært noe!

Kanskje løsningen er en helt annen enn den som ble skissert i forprosjektet. Problemet ble kanskje feilformulert i første omgang. Kanskje alle som trenger en slik løsning skal sette seg ned og diskutere hva vi ønsker. Det kan gjøre at en løsning blir mer generell og kan brukes av flere. Kanskje på tide å planlegge et seminar?
