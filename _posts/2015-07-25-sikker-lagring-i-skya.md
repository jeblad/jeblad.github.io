---
layout: post
language: nb
date: 2015-07-25 14:00:00 (CET)
title:  Sikker lagring i «skya»
tagline: er sikker lagring mulig på usikre skytjenester?
description: Skytjenester er attraktivt fordi det gir tilgang fra mange steder, men er en honningkrukke for de som ønsker å snoke.
authors:
  - jeblad
categories:
  - cloud storage
tags: security
licenses:
  - CC-BY-SA-4.0
---

Etter å ha skrevet på kode for [fillagring i nettskya](https://en.wikipedia.org/wiki/Cloud_storage) og funnet at dette er særdeles usikkert, ble det en diskusjon om hva som er mulig å få til. Skytjenester er på ene siden veldig attraktivt fordi en kan få tilgang til tjenester fra mange steder, samtidig er det en honningkrukke for de som ønsker å snoke i andres gjøren og laden. Det her ble ikke bare et attraktivt problem som trengte en løsning, det ble en utfordring. Det er mulig å få til sikker lagring i nettskya, men problemet er sammensatt og antakelig større enn det en kan nå over som et hobbyprosjekt. Dermed kommer tanken om dette er noe som er egnet for en [nettdugnad](https://en.wikipedia.org/wiki/Crowdsourcing).

<!--more-->

{% include nettdugnad.html source='http://nettdugnad.origo.no/-/bulletin/show/803826_sikker-lagring-i-skya' %}

Foranledningen til at undertegnede ble sittende å klø seg i hodet (jeg gjør ofte det) var at han (det vil si jeg) skrev på en løsning for å lage et versjonert fillager som enkelt kunne settes opp som repository for [File Explorer](https://en.wikipedia.org/wiki/File_Explorer) i Windows. File Explorer er filutforskeren til forskjell fra [Internett Explorer](https://en.wikipedia.org/wiki/Internet_Explorer) som er nettleseren du bruker på nettet.

Dette repoet fungerte omtrent slik mange er blitt vant med fra andre tjenester slik som Google Drive og Drop Box. En laster opp en fil til serveren og der beholdes det en eksakt kopi som er fullt lesbar bare en har de nødvendige credentials. Det betyr for eksempel at alle med tilgang til serveren kan se dine gamle bilder av mormor og farfar med lille gullungen, og også alle bildene du tok på Ibiza når du var utro. Det første er ikke så ille, men det siste kan bli et skikkelig «auda».

Etter at dette ørlille problemet ble påpekt gikk undertegnede (det vil si jeg) i tenkeboksen. Dette måtte da kunne løses på noe vis.

### Problemformulering

Problemet er at klienten har noe data som ønskes lagret på ett (eller flere) steder hvor klienten har tilgang til dem, uavhengig av hvilken maskin han bruker. Klienten vil typisk være laptoper, stasjonære PC'er, tablets og mobiler. Nesten alle av dem vil være basert på moderne operativsystem som kan utvides. Et fungerende system må som minimum tilby [konfidensialitet](https://en.wikipedia.org/wiki/Confidentiality) og [data integritet](https://en.wikipedia.org/wiki/Data_integrity). [Versjonering](https://en.wikipedia.org/wiki/Version_control) er ikke egentlig nødvendig, men vil være kjekt å ha.

Det vi ønsker oss er en [block-device](https://en.wikipedia.org/wiki/Device_file#BLOCKDEV) som sett fra filsystemet er som alle andre block-devices, men som lagrer sine data ute i nettskya, og som bruker [kryptering](https://en.wikipedia.org/wiki/Cryptography). Den samme block-device bør kunne sees fra flere enheter, selv om nok ikke alle filsystemer vil like at det tukles med blokker under kjøring. Nå er jo de fleste filsystemer lagd for å håndtere feil på en harddisk, og det som vil skje ved samtidig tilgang er jo nettopp at det vil oppstå «feil».

### Mulig løsning

Sikker lagring vil forutsette konfidensialitet, det vil i praksis si at ikke bare det som sendes er kryptert men at også det som lagres på serveren er kryptert. Ikke på noe tidspunkt må det som lagres bli dekryptert på veien fra klienten og til serveren, under lagring på serveren, eller på vei fra serveren og til klienten. Det må heller ikke finnes tilstrekkelig informasjon tilgjengelig om lagrede data, eller deres kryptering, slik at om noen fanger opp data underveis eller på serveren så skal de ikke kunne dekryptere innholdet. Det viktigste her er at alle klientens [private nøkler](https://en.wikipedia.org/wiki/Cloud_storage) skal finnes hos klienten og kun der. Det skal under ingen omstendigheter lagres private nøkler for klienten på serveren, den skal kun ha tilgang til brukerens offentlige nøkler. Her er det viktig å påpeke at serveren kan ha sine private nøkler og at de må finnes tilgjengelig på serveren.

Sikker lagring forutsetter også dataintegritet, det vil i praksis si at klienten signerer det som sendes til serveren. Når klienten signerer det som sendes til serveren så blir dette gjort med klientens private nøkkel. Serveren på sin side verifiserer at pakkens integritet er beholdt ved å sjekke med klientens offentlige nøkkel.

Fordi pakken med data ankommer serveren kryptert med serverens offentlige nøkkel så må pakken dekrypteres på serveren. For å unngå at pakkens egentlige innhold blir røpet så er pakkens innhold kryptert separat med en symmetrisk nøkkel som kun innehas av klienten. Vi oppnår på dette viset sikkerhet ved kryptering i flere lag, omtrent som en løk. En slik «onion» -struktur er det samme som brukes i [TOR-nettverket](https://en.wikipedia.org/wiki/Tor_(anonymity_network)).

På vei tilbake til klienten vil situasjonen være snudd, serveren signerer med sin private nøkkel og krypterer med klientens offentlige nøkkel.

Hvis vi signerer og krypterer på dette viset så vil vi fortsatt være utsatt for innbrudd via [public key infrastructure](https://en.wikipedia.org/wiki/Public_key_infrastructure) (PKI) som vi vil være avhengig av. Det vil imidlertid være lite å hente på et slikt innbrudd utover å angripe serverens data integritet, for dataene er fortsatt kryptert slik at kun klienten kan lese dem. Når dataene ankommer klienten så kan denne bruke sjekksummer for å verifisere dataenes integritet og da avvise en server som har vært utsatt for et vellykket angrep.

Pakkens innhold lagres på serveren med et «filnavn» som er en [universally unique identifier](https://en.wikipedia.org/wiki/Universally_unique_identifier) (UUID) som er kjent for både klient og server. Kommer det en ny pakke med et innhold som har samme UUID så vil den overskrive den gamle. Identifikatorene bærer ikke noen annen informasjon, de er kun et tilfeldig tall som identifiserer innholdet i en pakke.

Vi har nå et system som kan lagre datapakker med en key-value strategi. For å gjøre det enkelt for oss selv så antar vi at klienten snakker med serveren via et skjult [REST API](https://en.wikipedia.org/wiki/Representational_state_transfer) under første lag med kryptering hvor vi har enkle primitiver som PUT, GET og DEL. På utsiden av krypteringen har vi kun et helt enkelt API basert på et enkelt POST primitiv.

Vi ønsker å bruke eksterne skytjenester på et vis som gir oss høy sikkerhet også for dataoverlevelse. Det betyr at vi ønsker å spre data over flere skytjenester. Metoden er kjent fra [RAID](https://en.wikipedia.org/wiki/RAID), istedenfor å bruke en enkelt disk som kan feile så brukes to eller flere. Vi kan på samme viset bruke to eller flere skytjenester hvor vi sprer våre data. Vi bruker i praksis en nettbasert RAID 1, 5 eller 6 hvor vi splitter opp en blokk av data etter at vi har kryptert den med vår symmetriske cipher. Hver stripe for hver blokk vil også bli signert før vi lagrer den med en gitt UUID på serveren.

Fordi vi har striper lagret på forskjellige skytjenester så kan vi fortsette å bruke vår «skydisk» selv om en av skytjenestene er nede. Fordi vi også kan generere (og regenerere) en ny signatur for hver enkelt stripe så kan vi også forkaste striper det er tuklet med. I vårt system vil det være analogt med at vi har feil på en RAID disk. Bruker vi RAID 6 -konfigurasjon så kan to skytjenester samtidig være utilgjengelige på grunn av feil og systemet er fortsatt operativt.

Ved å splitte dataene så vil hver av blokkene vi lagrer være ufullstendig. Det vil vanskeliggjøre fiendtlig dekryptering av opplastede data. Vi vil eksponere noe metadata, det vil si at det er trafikk mellom klienter og serveren, og er serveren tatt over av en fiendtlig operatør så kan denne finne ut hvilken brukere som aksesserer de samme stripene på serveren. Uten tilgang på serveren er det kun mulig å se klienter som bruker samme eller lignende type tjeneste.

Når en stripe er lagret på serveren og den passerer en gitt alder så kan den automatisk bli merket som «gammel». Når det da blir lagret en ny stripe på samme UUID så blir den gamle lagret som en [sikkerhetskopi](https://en.wikipedia.org/wiki/Backup). Det samme kan skje om en tidligere stripe merkes manuelt som gammel. Etter slik automatisk eller manuell merking kan hele den eksterne disken rekonstrueres fra sikkerhetskopiene. Utdaterte sikkerhetskopier kan fjernes etter gitte regler, for eksempel hvis de er eldre enn ett år og det finnes nyere sikkerhetskopier.

Største problemet vi vil støte på med en slik block-device er samtidig skrivetilgang. Noen filsystemer mellomlagrer (caches) aggressivt data for å kunne optimalisere lesing og skriving, og i disse tilfellene må vi slå av dette slik at vi er sikret at de leser oppdaterte blokker. Det vil også være en fordel om vi kan lage hooks inn i mekanismer for [file locking](https://en.wikipedia.org/wiki/File_locking), men ikke alle programmer bruker file locks. Risikoen er at to programmer forsøker å skrive til filer som begge bruker samme blokk. En mulig løsning i disse tilfellene er å bruke en diff mellom blokkene, men det kan være nokså risikabelt. Det er neppe noen god løsning å sette blokker til read-only da filer allerede kan være åpnet for skriving. En mulighet som ikke er så gal som den først synes er kun å tillate en klient å åpne filer for skriving om gangen, og forsinke andres åpning av samme fila inntil den eventuelt får en time-out.

### Oppsummering

Det kan se ut som om det er mulig å lage et enkelt å effektivt skybasert datalager, om ikke annet så for personlig bruk. Samtidig tilgang for mange brukere er nok vanskeligere, muligens må en ha et spesialisert filsystem som gjør locking på blokk-nivå for å få det til å fungere tilfredsstillende. Som et personlig datalager kan det virke som løsningen vil fungere tilfredsstillende.

Koden for serveren vil i hovedsak være basert på PHP eller et annet programmeringsspråk som enkelt kan brukes på skytjenester, mens koden for klienten i hovedsak vil skrives med utgangspunkt i de språkene som brukes på de aktuelle plattformene. Programvaren for serveren er muligens enklere enn for klientene da de siste vil få større spredning på arkitektur.

Omfanget av kode for en slik løsning vil imidlertid bli nokså stor. Antakelig noe i overkant for en enkelt utvikler, men ikke mer enn at en liten gruppe av utviklere i en nettdugnad kan komme i mål.