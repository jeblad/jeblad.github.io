---
layout: post
language: nb
date: 2011-04-28 06:00:00 (CET)
title: Feilretting på Wikipedia og SNL
tagline: feil overlever, hvordan motvirke det
description: Feilretting i leksikon som Wikipedia og SNL drives av både vilje til å rette feil og hvorvidt feil er synlige.
authors:
  - jeblad
categories:
  - encyclopedia
  - crowdsourcing
tags: social media, wikipedia, social cost, quality assurance, document control, error correction, norsk nettleksikon, store norske leksikon
licenses:
  - CC-BY-SA-4.0
---

Utfra den allment brukte (og aksepterte) forklaringen så skal feil forsvinne over tid på Wikipedia og i litt mindre grad på Store Norske Leksikon, eller det som også kalles Norsk Nettleksikon. Dette skjer ikke, feil overlever på Wikipedia, og de overlever mye lengre enn en skulle tro var mulig. Samtidig er mengden feil urovekkende høy. Det er mulig å vise hva som skjer ved å modellere prosessen uten bruk av alt for avanserte teknikker.

<!--more-->

{% include nettdugnad.html source='https://web.archive.org/web/20100824001252/http://nettdugnad.origo.no:80/-/bulletin/show/589117_feilretting-paa-wikipedia' %}
{% include popular.html %}
{% include reworked.html %}

Wikipedia består av et stort datalager med informasjon, og denne informasjonsbasen blir vedlikeholdt og kontrollert av gatekeepers som har varierende kunnskaper om innholdet i informasjonsbasen. Deler av informasjonen i datalageret har i tillegg referanser til annen informasjon som understøtter denne, men la oss se bort fra disse. På Wikipedia er det hovedsakelig patrollers og administratorer som opptrer som gatekeepers, i Store Norske er rollen i stor grad overlatt til forfatterne selv.

På utsiden av datalageret finnes det andre som besitter kunnskaper om det som befinner seg inne i datalageret. Disse har i Wikipedia direkte tilgang til å endre innholdet, men bare så lenge aktiviteten blir funnet akseptabel av de som opptrer som gatekeepers. De som er gatekeepers forsøker å skille gode bidrag fra dårlige og tildels uønskede bidrag, de gode beholdes og de dårlige og uønskede forkastes.

### Feilretting

I noen tilfeller observerer en aktør på utsiden at det er en feil i datalageret, og han eller hun retter feilen. Hvis rettingen overlever møtet med gatekeepers og oppfattes som korrekt så beholdes informasjonen. Hvis informasjonen strider mot gatekeepers kunnskap så kan gatekeeper fjerne endringen, korrekt informasjon vil da erstatte feil informasjon. Gatekeeper kan også besitte feil kunnskaper, og dermed beholde feilaktig informasjon. I det første tilfellet fungerer prosessen, mens i det siste tilfellet feiler prosessen.

Når forfatter og gatekeeper har motstridende oppfatning av hva som er riktig kan det oppstå tildels svært heftige diskusjoner, og på Wikipedia kan de utarte til redigeringskriger med svært høy temperatur.

Hvis feilaktig informasjon ble beholdt så kan den likevel bli påvist og fjernet, men dette forutsetter at noen av gatekeeperne har kunnskaper som identifiserer informasjonen som feilaktig. Hvis antallet gatekeepers er begrenset så har de ikke kunnskaper som representerer hele kunnskapsfeltet, og deler av feltet kan mangle dekning eller kun bli dekt av én gatekeeper. Samtidig så kan kunnskapene de har representere en allmenn oppfatning som ikke er riktig. For å rette feil må det skapes et trykk innenfra av gatekeepers for å rette opp en feil, men hvis det er for få gatekeepers så kan trykket utenfra bli for stort.

For eksempel middelalderens oppfatning av at jorden var flat deles av ganske få, slik at tilsvarende få gatekeepers trengs for å motstå trykket.

Hvis korrekt informasjon blir fjernet så må den legges inn på nytt hvis den skal komme inn i datalageret. Hvis ingen av gatekeeperne har korrekt kunnskap så vil den bli fjernet på nytt. Det er et påtrykk utenfra for å få korrekt informasjon inn og et mottrykk innenfra for å holde informasjonen ute. Påtrykket utenfra og mottrykk innenfra skjer med gitte sannsynligheter og disse kan modelleres.

Hvis påtrykket utenfra er større enn mottrykket innenfra, og kun skjer feilretting, så vil alle feil bli rettet over tid. Hvis det skjer mer enn bare feilretting så vil ikke alle feil bli borte, mengden feil faller asymptotisk til en grenseverdi.

### De fire prosessene

Tilsvarende mekanismer driver fire forskjellige kontinuerlige prosesser som balanserer hverandre og som summerer til 1. Underliggende parametre kan endres for å forskyve resultatet.

<table class="table table-bordered">
<tr>
<th colspan="2" rowspan="2">&nbsp;</th>
<th colspan="2">Author has…</th>
</tr>
<tr>
<th>right<sup title="Better authors">&dagger;</sup></th>
<th>wrong</th>
</tr>
<tr>
<th rowspan="2">Gatekeeper has…</th>
<th>right<sup title="Better gatekeepers">&Dagger;</sup></th>
<td>P(X|korrekt,beholdt)</td>
<td><em>P(X|feil,fjernet)</em></td>
</tr>
<tr>
<th>wrong</th>
<td><em>P(X|korrekt,fjernet)</em></td>
<td>P(X|feil,beholdt)</td>
</tr>
</table>

- <sup>&dagger;</sup>Gode skribenter gir god tekstkvalitet, for teksten skrives med få feil.
- <sup>&Dagger;</sup>Gode gatekeepers gir god tekstkvalitet, for teksten rettes over tid.

Prosessene i kursiv på antidiagonalen er prosesser hvor feil blir gjort, men hvor resultatet er at teksten forblir uforandret. Prosessen i øvre venstre hjørne gir ny korrekt tekst, mens i nedre høyre hjørne akkumulerer teksten feilaktig innhold.

Det er verd å merke seg at den uheldige oppføringen i nedre høyre hjørne er en seriesannsynlighet

$$
\begin{equation}
P \left ( X \mid _{\text{feil},\text{beholdt}} \right ) = \prod_{k} P \left ( X_{k} \mid _{\text{feil},\text{beholdt}} \right )
\end{equation}
$$

Produktsummen kan enten ha én aktør som gjør veldig få feil, eller flere aktører som hver gjør litt flere feil. Det vesentlige er produktsummen på venstreside i uttrykket, og en produktsum av selv moderate bidrag gir en veldig liten verdi.

I systemer slik som Wikipedia er gatekeeper og forfatter to forskjellige (eller endatil flere forskjellige) personer. Da har de forskjellige kunnskaper, og selv om de besitter mindre kunnskap så er sjansen for at de begge (alle) begår samme feilen liten. Alle prosessene i matrisen er da aktive. Feilretting vil da skje så lenge sannsynligheten for at gatekeeper *og* forfatter innehar korrekt kunnskap er større enn sjansen for at begge innehar feilaktig kunnskap. Denne prosessen vedvarer så lenge artikkelen kan redigeres.

I systemer slik som Store Norske Leksikon er gatekeeper og forfatter gjerne den samme personen. Vedkommende som besitter begge disse rollene har samme kunnskap, og en feil begått i den ene rollen vil også begås i andre rollen. Kun to av prosessene i matrisen er da aktive. Igjen vil feilretting skje så lenge sannsynligheten for å inneha korrekt kunnskap er større enn sjansen for å inneha feilaktig kunnskap. Denne prosessen vil stoppe opp når forfatteren forlater artikkelen.

<p class="note">Store Norske Leksikon har endret produksjonsmodellen slik at de nå har en redaksjon som ettergår de fagansvarlige, men kun hvorvidt de følger opp innspill fra lesere. Det virker ikke som redaksjonen har noen reell rolle som gatekeepers.</p>

Wikipedia kan selvfølgelig kvalitetssikre teksten gjennom å kvalitetssikre skribentene, selv om den nåværende prosessen ikke legger opp til det. Norsk Nettleksikon kan tilsvarende kvalitetssikre teksten gjennom å legge på dokumentkontroll, og ikke som nå med kvalitetssikring av skribentene. Hver av dem er da over på «motstandenderens banehalvdel» når det gelder kvalitetssikring.

Hvis det er flere som er involvert i rollen som gatekeepers så vil en få en hypercube hvor hjørnene på diagonalen er felles for alle aktørene, mens hver av gatekeepers har egne hjørner på antidiagonalen. Med økende antall gatekeepers blir sjansen for at feil vil overleve veldig liten, gitt at gatekeepers ikke deler feiloppfatninger.

### Peer review

Hva en kaller personen eller personene som opptrer som gatekeepers spiller liten rolle for hva som rent faktisk skjer, men det spiller en stor rolle for hvordan prosessen oppfattes. Personene kan være del av et åpent nettsamfunn, med et flatt rollehierarki, og det kan være dugnadsbasert. Det samme skjer ved at forfatter og gatekeeper er forskjellige personer. Personene kan være journalister som opptrer som forfattere, og gatekeepers som er del av en redaksjon. Det samme skjer igjen ved at ved forfatter og gatekeeper er forskjellige personer. Personene kan være forskere som opptrer som forfattere, og reviewers som gjør peer review. Det samme skjer igjen ved at forskere og reviewers er forskjellige personer.

Kun i tilfeller hvor gatekeeper og forfatter er samme person en får den uheldige situasjonen i nedre høyre hjørne (lign. 1) hvor feil skrevet av forfatter overlever gatekeepers review.

### Livvaktmodellen

Grunnlaget for en endring som er spesielt interessant kommer fra et helt annet domene enn kvalitetssikring av dokumenter. Livvakter for VIPs er kommet en lang vei siden den gang det eneste som betydde noe var muskler. Nå modelleres og analyseres hva som gir økt sikkerhet med stor nøyaktighet. Etter hvert som antall livvakter øker så minker problemet med angripere utenfra, men problemet med VIPs som blir skutt av egne livvakter løses ikke. For å gå rundt problemet brukes det ekstra ubevæpnede livvakter i et ytre skjold som kun observerer.

Det samme kan brukes for gatekeepers. Istedenfor å ha gatekeepers som sitter med absolutt makt over hva som legges til og fjernes så har en mange små ubevæpnede gatekeepers. I praksis så kan en la leserne markere hva de mener er trøblete, og deretter la skribentene bevise hvorvidt det de har skrevet er riktig. Istedenfor en kunnskapsbase representert av gatekeeperne så spiller en direkte på kunnskapsbasen til leserne, og istedenfor absolutt sletting eller behold fra en liten gruppe gatekeepers så bruker en dialog med en stor mengde brukere.

Det som ligger under er et ønske om økt *sannsynlighet for oppdagelse* ([probability of detection](https://en.wikipedia.org/wiki/Probability_of_Detection)), mens en ikke i samme grad trenger økt evne til handling etter oppdagelse. Redusert arbeidsbyrde under oppdagelse kan tas ut som økt handlingsrom ved oppfølging av det oppdagede hvis det er nødvendig.

### Pending changes

«Livvaktmodellen» er i praksis det samme som eksperimentene med «pending changes» på Wikipedia, hvor endringene er synlige og skilles ut, og ikke forsvinner i mengden. Kun det som er klar vandalisme blir fjernet uten diskusjon. Endringer vil stadig lage grener i et tre som leserne så klipper av når de diskuterer seg frem til hva som er riktig. Fordi det kan finnes flere grener så må det finnes effektive metoder for å reintegrere disse på hovedstammen når det er avklart om de er korrekte.

En ren avstemming er ikke bare av det gode, idéelt sett burde løsningen legge opp til at en ikke bare stemmer men også angir hva som er riktig og hvorfor. Noe slikt vil imidlertid øke sjansen for at en får introdusert vandalisme, som igjen vil spise av gatekeepernes begrensede arbeidskapasitet. Her kan en hente en mulig løsning fra Slashdot, ikke bare lar man slike reviewers (moderatorer) av innholdet kommentere, man introduserer også metareviewers (metamoderatorer) som rater reviewerene (moderatorene). En kan også bruke en annen kostfaktor hvor en sier at reviewers maksimalt kan bevege seg vekk fra konsensus med et gitt nivå før metareviewers må kvalitetssikre deres arbeid. Når de er innenfor dette nivået så kan de kommentere, kommer de utenfor så mister de muligheten til å kommentere men beholder muligheten til å stemme.

Løsningen øker ikke tilveksten av riktig innhold i nevneverdig grad, men den sikrer at feilaktig materiale i større grad blir fjernet mens korrekt materiale som strider med de interne skribentenes etablerte konsensus blir beholdt. Hvis disse prosessene kan utføres med større presisjon så vil innholdet konvergere mot slutt-tilstander som er mer korrekte.

### Sammendrag

Feilretting i Wikipedia er helt grunnleggende basert på samme mekanismer som i andre tekster. En kan anta at forfatterne og gatekeepers individuelt har noe mindre kunnskaper, men at disses kunnskaper kombineres i en felles bidragsprosess. Når innhold skapes er forfatteren alene, og manglende kunnskaper hos en forfatter kan gjøre at artikkelen utvikler seg langsomt, men under feilretting blir flere involvert og disses kombinerte kunnskaper slår gjennom. Resultatet er at sannsynligheten for at feil overlever er liten.

Dette er imidlertid et idealisert stabilt tilfelle. I virkeligheten har forfattere bidrag over tid og gatekeepers har feilretting over tid. Bidragenes synlighet vil påvirke sannsynligheten for at feil oppdages, og dette vil gjøre at feil akkumulerer om de kommer raskt. Dette er vanlig på Wikipedia, en forfatter får motivasjon til å jobbe med en artikkel, og over kort tid kan det lages mange bidrag. Vedvarende feilretting drive feilene ned, og når gatekeepers retting er større enn forfatters bidrag vil feilraten gå asymptotisk til forfatters og gatekeepers kombinerte feilrate. Hvis forfatterens bidrag over tid derimot er større enn gatekeepers retting vil andel feil i materialet gå asymptotisk til forfatterens feilrate.

Det kan legges til metoder som øker synlighet av forfatterens og gatekeepers aktiviteter, og dermed påvirkes feil i materialet over tid. Slike mekanismer er for eksempel spesialsiden «siste endringer» på Wikipedia. Materialet vil da få en andel feil som påvirkes av eksponeringstid, og feil lagt til av forfatter og fjernet av gatekeeper. Slike mekanismer kan gjøre at andel feil blir annerledes enn forfatters vs forfatter og gatekeepers kombinerte feilrater.
