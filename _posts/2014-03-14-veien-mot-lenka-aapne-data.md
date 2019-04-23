---
layout: post
language: nb
date: 2014-03-14 22:00:00 (CET)
title: Bruk lenka åpne data
tagline: semantiske data the web way
description: En gjennomgang av hvordan og hvorfor en bør bruke lenkede semantiske data, og noen tips for å gjøre dette enklest mulig.
authors: [ jeblad ]
categories :
  - semantic web
  - crowdsourcing
tags: Wikipedia, Wikidata, linked data, open data, semantic web
license: cc-by-sa
---

De fleste som er litt aktive på tekniske sider på nettet har nok fått med seg frasene [åpne data](https://en.wikipedia.org/wiki/Open_data) og [lenkede data](https://en.wikipedia.org/wiki/Linked_data), og kanskje også [semantisk web](https://en.wikipedia.org/wiki/Semantic_Web). Disse begrepene er sentrale i en stille revolusjon på nettet. Data som før levde «inni» maskiner og kun ble gjort tilgjengelig i en tekstgraut blir nå gjort tilgjengelig på et vis som er velstrukturert og gjenbrukbart. Hvem er involvert og hvordan skjer dette?

<!--more-->

{% include nettdugnad.html source='http://nettdugnad.origo.no/-/bulletin/show/826336_veien-mot-lenka-aapne-data' %}

### eXtensible Markup Language

Noen år etter at [World Wide Web](http://en.wikipedia.org/wiki/World_Wide_Web) tok av så begynte [W3C](http://en.wikipedia.org/wiki/World_Wide_Web_Consortium) å se på muligheten for å bake inn mer semantikk. Dette var allerede påtenkt fra starten av, men det gikk en stund før dette sank inn hos de litt tyngre brukerne på nettet. De første viktige stegene var [eXtensible Markup Language](http://en.wikipedia.org/wiki/XML) (påbegynt 1996, recomendation 1998 [¹](http://www.w3.org/TR/1998/REC-xml-19980210)) og [XML Schema](http://en.wikipedia.org/wiki/XML_Schema_(W3C)) (recomendation 2001 [²](http://www.w3.org/TR/2001/REC-xmlschema-0-20010502/)). Den første av disse var viktig for den definerte en enhetlig måte å formidle strukturerte data. Den andre er viktig for den definerte hvordan de strukturerte dataene gis semantikk. Da får dataene betydning som er felles på tvers av nettstedene hvor de brukes.

Helt sentralt i denne semantikken er at en har et trippel som består av [subjekt](http://en.wikipedia.org/wiki/Subject_(grammar)), [predikat](http://en.wikipedia.org/wiki/Predicat_(grammar)) og [objekt](http://en.wikipedia.org/wiki/Object_(grammar)). Subjektene er entiteten vi beskriver, predikatet er sammenhengen og objektet er det som relateres til entiteten. For eksempel kan subjektet være «Haakon Magnus», predikatet kan være «far», og objektet kan være «Harald V».

Selv om det fantes standarder så var det fortsatt mange som holdt på sine egne proprietære løsninger. Microsofts [XDR Schema](http://en.wikipedia.org/wiki/XDR_Schema) er en proprietær løsning som forsvant, mens "Document Type Definition" fortsatt finnes og brukes i enkelte sammenhenger.

Vanligste bruksområde for slike strukturerte data var i leverandørenes egne systemer, men litt etter hvert ble det en økende fokus på hvordan en kunne gjenbruke på tvers av domener. Det trigget også en interesse for hva som er forutsetningen for slikt gjenbruk. Ikke bare må dataene publiseres med en forståelig semantikk, eller [ontologi](http://en.wikipedia.org/wiki/Ontology_(information_science)), de må også publiseres slik at det er lov å bruke dem. Ved at det ble et fokus på å åpne opp datasiloene, og å lisensiere dataene slik at de kan gjenbrukes i flere sammenhenger, ikke minst utenfor domenet til opprinnelig dataeier, så økte interessen fra de som ønsket å gjenbruke og en fikk en fremvekst av [mashups](http://en.wikipedia.org/wiki/Mashup_(web_application_hybrid)). Dette er små webapps som gjenbruker data fra forskjellige kilder for å lage en ny grafisk representasjon.

### Resource Description Framework

Det var også et par andre standarder som kom som gjorde det mulig å relatere data i en beskrivelse til tilsvarende data i andre beskrivelser. Den første som kom var [Resource Description Framework](http://en.wikipedia.org/wiki/Resource_Description_Framework) (recomendation 1999 [³](http://www.w3.org/TR/1999/REC-rdf-syntax-19990222/)) og [RDF Schema](http://en.wikipedia.org/wiki/RDF_Schema) (recomendation 2004 [⁴](http://www.w3.org/TR/2004/REC-rdf-schema-20040210/)). Noe av det viktigste med disse standardene var at de gjorde det mulig å identifisere entiteter og bruke disse identifikasjonene til å skape relasjoner mellom dem. Dette hadde vært mulig tidligere, men det var noe ustrukturert og også litt tilfeldig hvordan det ble gjort på nettsteder.

### Cool URI

Nå begynner et mantra å få gjennomslag, «bruk URI-er som identifikatorer». Blant annet formulerer Tim Barners Lee dette i et notat om linked data [⁵](http://www.w3.org/DesignIssues/LinkedData.html) hvor han setter opp fire kriterier.

1. Use URIs as names for things
2. Use HTTP URIs so that people can look up those names.
3. When someone looks up a URI, provide useful information, using the standards (RDF\*, SPARQL)
4. Include links to other URIs, so that they can discover more things.

Tilsammen har dette som effekt at en kan referere til entiteter på tvers av domener og koble dem sammen. For eksempel kan jeg identifisere Haakon Magnus, Harald V og Olav V med en URI. Hvis alle disse har en RDF som beskriver hvem som er deres fedre, og hvis jeg laster ned og følger relasjonene så vil jeg finne at Harald V er Haakon Magnus sin far, og Olav V er Harald V sin far. Samtidig kan jeg si at Olav V er far til Haakon Magnus sin far, eller litt enklere at Olav V er Haakon Magnus sin bestefar. Selvfølgelig forutsetter dette at disse dataene blir publisert, og det er ikke helt opplagt.

En ekstra ting må til for å få dette til å fungere sømløst. Vi trenger det som kalles «Cool URIs» [⁶](http://www.w3.org/TR/cooluris/). Det disse gjør er at vi kan lenke til en virkelig entitet og få en «oops, kan ikke overføre denne tingen på digital form -- men jeg har en alternativ URI» tilbake. Når vi så følger denne så kan vi få et nytt svar som sier noe ala «jeg har både HTML og RDF, hva vil du ha?» En maskin vil da svare «RDF» for det er noe den kan lese. For å gjøre det enklere å finne feil så kan en ofte overstyre hva som blir sendt tilbake. For eksempel blir Oslo identifisert med URIen <http://sws.geonames.org/6453366/> som så blir omdirigert til <http://sws.geonames.org/6453366/about.rdf> hvis siden blir lest av maskiner (RDF) <http://www.geonames.org/6453366/oslo.html> hvis siden blir lest av mennesker (HTML).

### Lenka åpne data

Med disse verktøyene er vi fremme ved det sentrale i lenka åpne data; vi har fått et nett av resurser som lenker til andre resurser og disse lenkene kan krysse domenegrenser. Når en (smart) maskin begynner å nøste i dette nettet så kan den finne ut hvem som er far og bestefar (og bestemor) og så videre.

Når maskiner skal finne frem i slike sammenhenger så er det de samme metodene som gjenbrukes gang på gang. For dem er «Haakon Magnus sin fars far er en bestefar» det samme som «Anne sin mors mor er en bestemor». Faktisk er det slik at svært komplekse spørringer bygger på de samme primitivene brukt om og om igjen.

### Hvem er disse folka

De virkelig store aktørene på dette feltet har svært store datasett, de teller sine relasjoner eller tripler som de ofte kalles, i *milliarder* eller mer. Slike lagre av tripler blir kalt [triplestore](http://en.wikipedia.org/wiki/Triplestore). Selv middels store aktører teller slike i millioner. En av de større åpne nettstedene som har slike beskrivelser av entiteter er [DBpedia](http://en.wikipedia.org/wiki/DBpedia). De henter data fra blant annet Wikipedia for å bygge sitt nettverk av lenkede entiteter, eller det som kalles en graf. Wikipedia selv er iferd med å bygge opp sitt eget trippelstore i prosjektet [Wikidata](http://en.wikipedia.org/wiki/Wikidata).

I Norge så har vi en del middels store aktører som publiserer semantiske data. Flere av disse ønsker å skifte til lenka åpne data for å utnytte synergieffektene på nett. Noen av dem publiserer til Norvegiana, som er et semantisk datalager som aggregerer literal data, og som så publiserer videre til Europeana, som også er et semantisk datalager som aggregerer literal data men med litt mer fokus på bruk av URI-er. Literal data er alt det som ikke er lenker til andre ressurser, eksempel navnet «Oslo» eller «Haakon Magnus» eller «Anne».

### Oppsummering

Hvis vi skal gjøre alt riktig så er kanskje ikke aggregering av semantiske data veien å gå, vi trenger punkt fire på Tim Barners Lee's liste «Include links to other URIs, so that they can discover more things.» Vi trenger en form for katalogtjenester som samler aktuelle URI-er og som inneholder akkurat nok literal data til at maskiner kan begynne å nøste. Vi trenger ikke å samle absolutt alt av data om hver entitet i et kjempelager, men vi trenger nok til at interesserte kan begynne.

Den største hindringen for å få et velfungerende nett av lenka åpne data er at vi for en stor del mangler stabile URI-er som kan beskrive helt sentrale entiteter. Vi har for eksempel ikke slike for helt sentrale administrative enheter som kommuner og fylker. Vi har heller ikke slike for historiske personer. Vi har en delvis løsning for forfatter og etter hvert for kunstnere. Vi har ikke noe for musikere.

Faktisk er det slik at noen av de største aktørene som beskriver Norge som lenka data er Wikidata, DBpedia og Geonames. Det synes i alle fall jeg er litt kewlt, men også litt trist.