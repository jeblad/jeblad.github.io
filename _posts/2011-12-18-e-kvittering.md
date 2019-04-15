---
layout: post
language: nb
date: 2010-06-16 12:00:00 (CET)
title: e-kvittering, er det mulig?
tagline: en mulig løsning som er enkel og billig
description: Er det mulig å lage et enkelt og effektivt system for å endre dagens enkle papirkvitteringer til et effektivt leveringssystem for digitale bilag?
authors:
  - '[John Erling Blad](/authors/jeblad/)'
categories : encyklopedia
tags: wikipedia, pending changes, stable versions, flagged revisions, quality, patrolling, reviewer
license: cc-by-sa
---

Under en diskusjon om e-faktura for noen år siden ble det påpekt at det største volumet av regnskapsunderlag ikke var fakturaer, men kvitteringer fra alle mulige småkjøp. SVT Rapport mener det årlig skrives ut 1.500.000.000 kvitteringer i Sverige og at dette representerer 60.000 felte trær. Disse kvitteringene er tidkrevende å legge inn i regnskapssystemene, og under den manuelle inntastingen er også lett å gjøre feil. I tillegg er bruk av personlige regnskapssystemer vanskeliggjort ved at systemene er så arbeidskrevende. Hvis dette tilsynelatende trivielle problemet kan løses som en felles dugnad så vil det gi svært store tidsbesparelser for både privatkunder, bedrifter og offentlige organisasjoner.

<!--more-->

{% include nettdugnad.html source='http://nettdugnad.origo.no/-/bulletin/show/710173_e-kvittering-er-det-mulig' %}

Problemet og løsningen er basert på relativt enkle og velkjente tekniske løsninger. De er ikke begrenset til noen bestemt teknologi, og som det vises i artikkelen så fungerer det med en ordinær papirkvittering som felles medium.

### Bakgrunn

Problemet vi står ovenfor er ikke helt trivielt, men likevel nokså enkelt. Noen går i en butikk for å kjøpe noe, ofte er personen helt anonym for butikken, og på et senere tidspunkt skal informasjon fra dette kjøpet inn i et regnskapssystem. Som oftest er det eneste som er felles selve kvitteringen, men denne har ikke plass til all informasjon vi ønsker om kjøpet samtidig som vi helst ikke vil punche for mange tall og koder. Det gjør at all nødvendig informasjon fra kjøpet må overføres via kvitteringen, og på noe vis må denne gjøres «elektronisk», men samtidig sikker nok til at ikke andre kan hente ut informasjon om kjøp og salg på illegitimt vis.

Omformulert så kan vi si at vi ønsker å skape forutsetninger for å kunne bruke kassalappen for [autorisasjon](http://en.wikipedia.org/wiki/Authorization) av tilgang til en fullstendig spesifisert kvittering, vi ønsker [autentisering](http://en.wikipedia.org/wiki/Authentication) av kassalappen samtidig som vi ikke vil at den skal kunne brukes for [identifisering](http://en.wikipedia.org/wiki/Identification_%28information%29) av kunden. Autorisasjon skjer ved at kassalappen blir et ihendehaverdokument, uten at den inneholder noen identifiserende opplysninger. Ytterligere identifisering og informasjonslekkasje må vi unngå fordi det ikke er gitt at de som senere får tilgang til kassalappen skal ha informasjon om kunden.

Vi ønsker heller ikke å lage ekstra elektroniske dingser som inkluderer [RFID-brikker](http://en.wikipedia.org/wiki/Radio-frequency_identification) eller lignende. Slike løsninger er fine på tegnebrettet, men blir i praksis veldig dyre både i implementasjon og drift. Vi ønsker noe som er [KISS](http://en.wikipedia.org/wiki/KISS_principle) og fungerer i den eksisterende infrastrukturen.

Mange har stiftet kjennskap med en liten sak på mobilene for å overføre informasjon om kontakter fra en mobil til en annen, såkalte [vCard](http://en.wikipedia.org/wiki/VCard). Dette er spesielt formaterte tekstmeldinger som inneholder en serie identifiserte felt. En avsender formaterer en slik melding og mottakeren kan så dekode den.

Hva mer er, slike vCard kan kodes inn i 2-dimensjonale maskinlesbare grafiske koder slik som [QR-koder](http://en.wikipedia.org/wiki/QR_code). Dette er interessant fordi den nødvendige infrastrukturen for å produsere kodene allerede finnes, faktisk er det slik at svært mange kvitteringer allerede har maskinlesbare [bar-koder](http://en.wikipedia.org/wiki/Barcode).

### e-kvittering

Anta nå at vi utvider standarden for vCard, den er egentlig laget for å identifisere en person, organisasjon eller bedrift, slik at den kan identifisere en spesifikk kvittering. I praksis utvider vi standarden med ekstra identifikatorer for *TYPE*, *URL*, *kvitteringsnummer* (*UID*) og en hemmelig kode *SECRET*. Den siste skal vi komme tilbake til om litt. Det hele pakkes inn i feltet for *NOTE* som tilhører vCard-standarden.

Litt forenklet så har vi da noe som kan minne om dette

```
BEGIN:VCARD
VERSION:4.0
FN:REPA3000
NOTE:TYPE=receipt;URL=protocol://some.where.com;UID=num;SECRET=num
END:VCARD
```

![](/images/blank.png "output"){#el_14zu04ij_1kvj width="98" height="98"}[![](http://media1.origo.no/-/cache/image/2011070_h57a62ac55be2c85bb203_v1324221298_98x450.png "output"){.image .bordered_photo .right_aligned width="98" height="98"}](#)

Dette vil bli dekodet som en helt legitim vCard for den imaginære butikken *REPA3000*, om enn med et vCard som har et noe merkelig tillegg. Dette tillegget er våre ekstra data som gjør det mulig å få til en e-kvittering, og som lar et enkelt tilleggsprogram effektivisere hele innhentingen av den fullstendige kvitteringen.

Bildet til høyre viser eksempelet kodet som en helt legitim utgave av et QR-bilde.

Merk at det også finnes andre måter å kode inn den nødvendige informasjonen for å få en slik løsning til å fungere.

### Selger

Når butikken skriver ut kvitteringen så genererer kassa et tilfeldig og veldig stort tall. Slike tall blir gjerne omtalt som en [UUID](http://en.wikipedia.org/wiki/Universally_unique_identifier) eller [GUID](http://en.wikipedia.org/wiki/Globally_unique_identifier) og brukes idag til veldig mye som skal identifiseres. For eksempel brukes de til å identifisere harddisker i en PC. Vi bruker de til å identifisere en kvittering. Kassaapparatet sender så denne til butikkens server som oppretter en kvittering med denne identifikatoren. Hvis den allerede er i bruk så ber serveren kassa om å lage en ny, men som oftest vil det gå bra.

Kassa forteller serveren alle opplysningene den har om varekjøpet eller varekjøpene og serveren lagrer dette under merkelappen den har blitt enig med kassa om å bruke. Denne merkelappen er den tidligere omtalte UUID/GUID, eller UID slik vi har skrevet i eksempelet.

Hvis det bare var et passende og tilfeldig tall som identifiserer kvitteringen så kan vi tenke oss at noen ville forsøke å spørre om alle mulige slike numre og dermed få tilgang til alle kjøp i butikken. For å unngå dette så kan kassa og serveren bli enige om en felles hemmelighet, en såkalt [Diffie--Hellman key exchange](http://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange). Kassa skriver så den delte hemmeligheten på kassalappen.

Til slutt må vi ha en URL som kunden senere kan bruke for å hente ut informasjonen fra serveren. Dette trenger ikke være den samme serveren som butikken bruker som sin nettside, denne serveren vil typisk være dedikert for den her typen bruk og det kan også være en felles server for en leverandør av kassasystemer.

Alle disse dataene pakkes ned i en vCard og kodes som en QR-kode og trykkes på kvitteringen.

### Kjøper

Vel hjemme eller på kontoret holdes kvitteringen opp foran et webkamera (eller mobilkamera) og med nødvendig programvare leses QR-koden og vCard-infoen dekodes. Når programvaren oppdager at det finnes tilleggsinformasjon i NOTE-feltet så går den til URL-feltet som angir serveren og ber om en oppkobling for å få overført alle lagrede data om kjøpet.

Serveren lager nå et tilfeldig tall som sendes til kunden. Denne svarer med å kryptere tallet med den hemmelige nøkkelen som står skrevet på kvitteringen, og fordi denne er scannet og tilgjengelig i programvaren så kan programmet svare serveren med det dekrypterte tallet uten å involvere kunden overhodet. Serveren på sin side sammenligner med sin egen kopi av det krypterte tallet og er de like så sendes den lagrede kvitteringen fra kjøpet til kunden.

Formatet på selve kvitteringen som går fra serveren til kunden er ikke lengre begrenset av kvitteringens formfaktorer, og kan dermed inneholde langt mer detaljert informasjon enn det som er vanlig idag. For eksempel kan merverdiavgift for enkeltvarer skilles ut, eller det kan angis hva som er normal kontering i henhold til Norsk Standard for regnskap.

Et problem er da at mange regnskapssystemer rett og slett ikke er innrettet på å håndtere elektronisk regnskapsunderlag.

### Sikkerhet

For å redusere mulighetene for angrep på serveren så kan det legges til flere sikkerhetsmekanismer. Tallet som serveren lager kan settes opp slik at det kun er gyldig en begrenset tid, det kan settes inn ekstra bits som gjør at en enkelt kan beregne sjekksummer, det kan settes begrensinger på hvor mange utestående spørringer som kan finnes for en bestemt UID, og det kan legges til forsinkelser som skal overholdes. Slike begrensinger kan til sammen gjøre det svært vanskelig å gjøre metodiske angrep på en server i systemet.

Merk at for UUID/GUID er det versjon 4 som skal brukes. Spesielt versjon 1 har en del problemer ved at identifikatoren drar med seg en del identifiserende informasjon for selgerstedet.

Merk også at kunden kan bli identifisert via IP-adressen han bruker når det hentes data fra serveren. I tillegg kan kunden spores ved alle de vanlige metodene for cookies og supercookies av forskjellig slag.

### Effektivisering

For at noen skal få tak i underlaget for kjøpet er det en enkelt felles faktor; papirkvitteringen. Samtidig som det begrenser andres innsyn så gjør det også innsyn fra de som gjør bokettersyn langt enklere enn idag. En vil ikke lengre måtte ha fysisk tilgang til både salgssted og kjøpers regnskap for å gjennomføre en kontroll, det vil holde med tilgang til kjøpers regnskapsunderlag.

Samtidig så er papirkvitteringen alt som trengs for å få tilgang til hele regnskapsunderlaget, og hele prosessen med å legge dette datagrunnlaget inn i regnskapssystemene er dermed tilstede. Hva mer er, dette gjør det mulig å lage enkle regnskapssystemer for personøkonomi som kjører som en mobilapp fordi behovet for punching av enkeltkjøp er borte -- det er jo bare å scanne QR-koden med mobilkameraet.