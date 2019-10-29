---
layout: post
language: nb
date: 2011-04-28 06:00:00 (CET)
title: Feilretting på Wikipedia og SNL
tagline: – feil overlever, hvordan motvirke det
description: Feilretting i leksikon som Wikipedia og SNL drives av både vilje til å rette feil og hvorvidt feil er synlige.
authors:
  - jeblad
categories:
  - encyclopedia
  - crowdsourcing
tags: social media, wikipedia, social cost, quality assurance, document control, error correction, norsk nettleksikon, store norske leksikon
license: cc-by-sa
---

Utfra den allment brukte forklaringen så skal feil forsvinne over tid på Wikipedia og i litt mindre grad på Store Norske, eller det som nå kalles Norsk Nettleksikon. Dette skjer ikke, feil overlever på Wikipedia, og de overlever mye lengre enn en skulle tro var mulig. Samtidig er mengden feil urovekkende høy. Det er mulig å vise hva som skjer ved å modellere prosessen, men det er også mulig å forklare det hele uten å henfalle til veldig avanserte modeller.

<!--more-->

{% include nettdugnad.html source='https://web.archive.org/web/20100824001252/http://nettdugnad.origo.no:80/-/bulletin/show/589117_feilretting-paa-wikipedia' %}

Wikipedia består av et stort repository av informasjon, og denne informasjonsbasen blir vedlikeholdt og kontrollert av gatekeepers som har varierende kunnskaper om innholdet i informasjonsbasen. Deler av informasjonen i repositoryet har i tillegg referanser til annen informasjon som understøtter informasjonen, men la oss se bort fra disse. På Wikipedia er det hovedsakelig patrollers og administratorer som opptrer som gatekeepers, i Store Norske er rollen i stor grad overlatt til forfatterne selv.

På utsiden av repositoryet finnes det andre som besitter kunnskaper om det som befinner seg inne i repositoryet. Disse har i Wikipedia direkte tilgang til å endre innholdet, men bare så lenge aktiviteten blir funnet akseptabel av de som opptrer som gatekeepers. De som er gatekeepers forsøker å skille gode bidrag fra dårlige og uønskede bidrag, de gode beholdes og de dårlige og feilaktige forkastes.

### Feilretting i repositoryet

I noen tilfeller så observerer en aktør på utsiden at det er en feil i repositoryet, og han eller hun retter feilen. Hvis rettingen overlever og er korrekt så er korrekt informasjon lagt til i repositoryet. Hvis informasjonen strider mot kunnskapen gatekeeper har ervervet så kan gatekeeper fjerne endringen, korrekt informasjon er da fjernet feilaktig. Gatekeeper kan også ha feil kunnskaper og derfor beholde feilaktig informasjon. Spesielt når forfatter og gatekeeper er en og samme person kan det oppstå problemer og tildels heftige diskusjoner, og på Wikipedia kan slikt utarte til redigeringskriger med svært høy temperatur.

Hvis feilaktig informasjon ble beholdt så kan den likevel bli påvist og fjernet, men dette forutsetter at noen av gatekeeperne har kunnskaper som identifiserer informasjonen som feilaktig. Fordi antallet gatekeepers er begrenset så har de ikke kunnskaper som representerer hele kunnskapsfeltet. Samtidig så kan kunnskapene de har representere en allmenn oppfatning som ikke er riktig. For eksempel middelalderens oppfatning av at jorden er flat. Vi får et trykk innenfra for å rette opp en feil. Om ikke dette var nok så vil typisk bare en eller noen ganske få gatekeepers vurdere hvorvidt informasjon skal beholdes eller forkastes.

Hvis korrekt informasjon ble fjernet så må informasjonen bli forsøkt lagt inn på nytt hvis den skal komme inn i repositoryet. Hvis ingen av gatekeeperne vet at informasjonen er korrekt så vil den bli fjernet på nytt, vi har et påtrykk utenfra for å få informasjon inn og et mottrykk innenfra for å holde informasjonen ute. Påtrykket utenfra og mottrykk innenfra skjer med gitte sannsynligheter og disse kan vi modellere selv om vi skal avstå fra dette nå. Hvis påtrykket utenfra er større enn mottrykket innenfra, og vi kun har feilretting, så vil alle feil bli rettet over tid.

### De fire prosessene

Tilsvarende mekanismer driver fire forskjellige kontinuerlige prosesser som balanserer hverandre og som summerer til 1. Vi kan skru på en del underliggende parametre for å forskyve resultatet.

{:class="table table-bordered"}
|             |**korrekt**              |**feil**
|-------------|-------------------------|----------------------
| **beholdt** |  P(X\|korrekt,beholdt)<sup title="Feil rettes">&dagger;</sup>  | *P(X\|feil,beholdt)*<sup title="Feil propagerer">&Dagger;</sup>
| **fjernet** | *P(X\|korrekt,fjernet)*<sup title="Feil propagerer">&Dagger;</sup> |  P(X\|feil,fjernet)<sup title="Feil rettes">&dagger;</sup>

- <sup>&dagger;</sup>Færre feil på grunn av høyere utdanning (bedre skribentkvalitet) gir høyere tekstkvalitet.
- <sup>&Dagger;</sup>Feilkorrigering i fellesskap gir kvalitetsheving via vedvarende feilretting over lang tid.

De i kursiv (merket med &dagger;) er kvalitetssikring gjennom feilrettingsprosesser (feil har en tendens til å bli bragt videre til nye revisjoner), mens de som ikke er i kursiv (merket med &Dagger;) gir feilretting gjennom å sikre gode skribenter (feil blir fanget opp raskt). De viktigste for systemer som Wikipedia er prosessene som er gitt med kursiv, mens de viktigste for systemer slik som Norsk Nettleksikon er de som er diagonalen og som ikke er i kursiv. Wikipedia kan selvfølgelig kvalitetssikre teksten gjennom å kvalitetssikre skribentene, selv om det ikke legges opp til det nå for nå skjer kvalitetssikring gjennom feilretting av dokumentet. Norsk Nettleksikon kan tilsvarende kvalitetssikre teksten gjennom å legge på dokumentkontroll, og ikke som nå med kvalitetssikring av skribentene. Hver av dem er da over på motstandenderens banehalvdel når det gelder kvalitetssikring.

### Livvaktmodellen

Grunnlaget for en endring som er spesielt interessant kommer fra et helt annet domene enn kvalitetssikring av dokumenter. Livvakter for VIPs er kommet en lang vei siden den gang det eneste som betydde noe var muskler. Nå modelleres og analyseres hva som gir økt sikkerhet med stor nøyaktighet. Etter hvert som antall livvakter øker så løses problemet med angripere utenfra, men problemet med VIPs som blir skutt av egne livvakter øker også. For å gå rundt problemet brukes det ekstra livvakter i et ytre skjold som er ubevæpnet.

Det samme kan brukes for gatekeepers. Istedenfor å ha gatekeepers som sitter med absolutt makt over hva som legges til og fjernes så har en mange små ubevæpnede gatekeepers. I praksis så lar en leserne markere hva de mener er trøblete, og lar skribentene få en mulighet til å bevise hvorvidt noe er riktig. Istedenfor en kunnskapsbase representert av gatekeeperne så spiller en direkte på kunnskapsbasen til leserne, og istedenfor absolutt sletting eller behold fra en liten gruppe gatekeepers så bruker en dialog med en stor mengde brukere.

Det som ligger under er et ønske om økt sannsynlighet for oppdagelse, mens en ikke trenger økt evne til handling etter oppdagelse. Redusert arbeidsbyrde under oppdagelse kan tas ut som økt handlingsrom ved oppfølging av det oppdagede.

### Konsekvenser og sammendrag

Noe slikt er i praksis det samme som eksperimentene på Wikipedia med «stabile versjoner», men hvor endringene er synlige og ikke skjult og hvor kun det som er klar vandalisme blir fjernet uten diskusjon. Endringer vil stadig lage grener i et tre som leserne så klipper av når de stemmer over stoffets riktighet. Fordi det kan finnes flere grener så må det finnes effektive metoder for å reintegrere disse i hovedstammen når det er avklart om de er korrekte.

En ren avstemming er ikke bare av det gode, idéelt sett burde løsningen legge opp til at en ikke bare stemmer men også angir hva som er riktig og hvorfor. Noe slikt vil imidlertid øke sjansen for at en får introdusert vandalisme, som igjen vil spise av gatekeepernes begrensede arbeidskapasitet. Her kan en hente en mulig løsning fra Slashdot, ikke bare lar man slike reviewers (moderatorer) av innholdet kommentere, man introduserer også metareviewers (metamoderatorer) som rater reviewerene (moderatorene). En kan også bruke en annen kostfaktor hvor en sier at reviewers maksimalt kan bevege seg vekk fra konsensus med et gitt nivå før metareviewers må kvalitetssikre deres arbeid. Når de er innenfor dette nivået så kan de kommentere, kommer de utenfor så mister de muligheten til å kommentere men beholder muligheten til å stemme.

Løsningen øker ikke tilveksten av riktig innhold i nevneverdig grad, men den sikrer at feilaktig materiale i større grad blir fjernet mens korrekt materiale som strider med de interne skribentenes etablerte konsensus blir beholdt. Hvis disse prosessene kan utføres med større presisjon så vil innholdet konvergere mot slutt-tilstander som er mer korrekte.