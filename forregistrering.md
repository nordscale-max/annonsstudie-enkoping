# Förregistrering: studie av lokal synlighet i sökannonser, Enköping

Svensk version av förregistreringen. Avsedd för publicering tillsammans med datasetet.

**Status:** skriven före all betald datainsamling. Tidpunkten för git-incheckningen är
registreringstidpunkten. Ingenting nedan redigeras efter att insamlingen börjat; ändringar
läggs till som daterade tillägg längst ned.

**Ansvarig:** Nordscale (lokalt under namnet Adsbyrå Enköping).

## Redovisad intressekonflikt

Nordscale säljer söknannonsering. Företaget säljer alltså lösningen på det problem studien
mäter. Det hanteras med öppenhet, inte genom att utelämnas: den här förregistreringen, den
publicerade metoden, de publicerade antagandena, ett exporterbart aggregerat dataset och en
öppen inbjudan att göra om mätningen. Läsaren bör väga in det.

## Hypotes

För sökningar efter lokala tjänster i Enköpings kommun köps de översta textannonserna i Google
till övervägande del av annonsörer utan fysisk närvaro i kommunen, även i branscher där minst
ett aktivt lokalt företag bevisligen finns.

## Huvudpåståendet som prövas

> I N % av sökningarna efter lokala tjänster, där minst ett aktivt lokalt företag finns i
> branschen, tillhör ingen av de fyra översta textannonserna ett företag med fysisk närvaro i
> Enköpings kommun.

## Mått, definierade före insamling

Nämnarreglerna anges här så att de inte kan väljas efter att datan setts.

- **M1: lokal synlighet.** Andel observationer där textannonsen på position 1 i det översta
  blocket är klassad `local_town` eller `local_kommun`. *Nämnare: observationer som returnerade
  minst en textannons i det översta blocket.* Observationer utan annonser redovisas separat som
  `no_ads_rate`.
- **M2: onödigt läckage (huvudsiffra).** *Nämnare: observationer där (a) sökningens bransch
  har minst ett aktivt lokalt företag i nämnarregistret och (b) minst en textannons i det
  översta blocket returnerades.* Täljare: de där ingen av positionerna 1–4 är lokal. Villkor
  (b) är medvetet: en sökresultatsida utan annonser har inget klick att förlora, och att räkna
  den som läckage skulle blåsa upp huvudsiffran. Den strängare varianten utan villkor (b)
  beräknas och publiceras vid sidan av som `m2_leakage_all_serps`.
- **M3: geografisk maskering.** Andel textannonser i det översta blocket som är klassade
  `external_geo_targeted`, alltså nämner orten i rubrik eller beskrivning utan att ha fysisk
  närvaro.
- **M4: uppskattad omdirigerad efterfrågan.** Publiceras bara som ett intervall med låg,
  central och hög nivå, aldrig som en punktskattning. Varje ingångsvärde finns i
  `docs/assumptions.md`, genererad från studiens konfiguration. En siffra vars ingångsvärden
  inte finns där publiceras inte. Ett klick är inte en förlorad affär, och rapporten säger det
  bredvid siffran.
- **M5: stabilitet.** Andel celler av typen sökning × enhet där annonsören på position 1 är
  identisk i samtliga mätrundor. Redovisas som ett mått på hur mycket M1–M3 bör vägas.
- **M6: skillnad mot kontrollkommun.** M1, M2 och M3 för kontrollkommunen minus samma mått
  för Enköping.

Alla mått beräknas per bransch, frågemönster, enhet, runda och kommun, samt sammanslaget.
De sammanslagna siffrorna är huvudsiffror; de uppdelade hamnar i bilagan.

### Varför de två frågetyperna mäter olika saker

Google Ads har **"närvaro eller intresse"** som standardinställning för geografisk inriktning.
En annonsör som riktar mot Enköping visas därför för någon som befinner sig fysiskt i Stockholm
och skriver "tandläkare enköping", eftersom själva sökningen uttrycker intresse för Enköping.
Det är dokumenterat standardbeteende, inte en annonsör som utnyttjar något, och studien säger
det rakt ut.

Två följder, båda deklarerade före insamlingen:

1. **På sökningar med ortsnamn spelar sökarens fysiska plats nästan ingen roll.** Vår egen
   mätplats är därmed oviktig för det segmentet, vilket är skälet till att inriktning på
   kommunnivå räcker där. Förkontrollen bekräftade det empiriskt: samma sökning från Enköping
   och från Stockholm delade tre av fyra annonsörer.
2. **På `{tjänst} nära mig` är den fysiska platsen den enda geografiska signalen.** Det är den
   metodmässigt renaste mätningen av vem som syns för någon som faktiskt befinner sig i
   Enköping, och den deklareras i förväg som ett eget segment. Förkontrollen bekräftade att
   platsen förändrar resultatet (två av två branscher skilde sig mellan Enköping och
   Stockholm), vilket är beviset för att vår förfrågans plats alls når auktionen.

Det begränsar också hur M3 får tolkas. Ett Västeråsföretag som dyker upp på "elektriker
enköping" är standardinställningen som fungerar precis som den ska. Slutsatsen studien kan bära
handlar om **vem som saknas i auktionen**, inte om att externa annonsörer beter sig felaktigt,
och rapporten får inte antyda något annat.

## Klassificeringstaxonomi

`local_town`, `local_kommun`, `external_geo_targeted`, `external_generic`, `aggregator`,
`unknown`. Definitionerna finns i `studies/enkoping.ts` och skrivs ut av `npm run assumptions`.

Bestämt i förväg:
- Ett registrerat säte i Enköping med all verksamhet någon annanstans är **inte** lokalt.
  Närvaro betyder operativ närvaro.
- En franchise klassas efter var tjänsten levereras ifrån, och flaggas separat.
- Ett verksamhetsområde som täcker Enköping utan adress är `external_*`. **Verksamhetsområde
  är inte närvaro.** Det är just den skillnaden studien finns till för att mäta.
- Förmedlare är en egen kategori och slås aldrig ihop med `external_*`.

## Gränsvärden deklarerade i förväg

| Utfall | Tolkning |
|---|---|
| M2 ≥ 0,60 | Hypotesen stöds |
| M2 0,40–0,60 | Blandat; redovisas som blandat, inte tillrättalagt |
| M2 ≤ 0,40 | Hypotesen stöds inte. Publiceras ändå. |
| M6 (kontroll − Enköping) liten | Fyndet gäller mellanstora svenska kommuner i allmänhet, vilket är en större sak än Enköping |
| M6 stor | Enköping är ovanligt, och rapporten säger det |

## Publiceringsspärrar

Studien publiceras inte om någon av dessa brister (`publishGate` kontrollerar dem i koden):
- `unknown` utgör minst 5 % av annonsvisningarna
- ett antagande som matar en publicerad siffra saknar angiven källa
- någon av de 100 största domänerna mätt i visningar saknar manuell klassificering
- ingen sökning har mätts i mer än en runda

## Urvalsplan

Cirka 490 sökningar (49 branscher × 5 frågemönster × 2 kommuner), 2 enheter, 3 rundor spridda
över minst två olika veckodagar och täckande en vardagsförmiddag, en vardagskväll och en
helgdag. (Ändrat 2026-09-04: den ursprungliga texten sa "minst fem kalenderdagar". Det som
spelar roll är spridningen över veckodagar och tider på dygnet, vilket är det auktionen
faktiskt varierar med; ett fast spann på fem dagar var godtyckligt.)
Exakt UTC-tidpunkt sparas per anrop. Leverantörens obehandlade svar sparas ordagrant för varje
anrop och ändras aldrig.

## Kända begränsningar, angivna innan resultaten setts

1. **Insamlingen sker mot kommunen, inte mot en koordinat.** Leverantören accepterar bara ett
   kanoniskt geo-target-namn för Google-motorn. Varje observation sparar leverantörens egen
   audit-URL som bevis på vad som faktiskt skickades.
2. **Andelen falska negativa är instabil.** Över tre förkontroller returnerade samma tio
   svenska kontrollsökningar med hög konkurrens 0 %, 20 % och 0 % tomma annonsblock, utan att
   någon sökning var konsekvent tom. En enstaka mätning av den här golvnivån är därför
   opålitlig, och den mäts upprepade gånger och publiceras som ett intervall i stället för som
   en punkt.
3. **Local Services Ads observerades inte i Sverige** i förkontrollerna, så de är sannolikt
   ingen faktor. De samlas ändå in och lagras separat ifall det ändras.
4. **Ingen av leverantörerna garanterar att annonser fångas.** Båda dokumenterar det. Varje
   anrop görs med annonsoptimerad hämtning påslagen. Före insamlingen mäter en kontrollmängd
   av svenska kommersiella sökord med hög konkurrens hur ofta varje leverantör returnerar noll
   annonser där annonser är nästintill säkra. Den andelen falska negativa publiceras, och den
   är golvet under varje nolla i datasetet.
5. **SNI-koder registreras av företagen själva**, så nämnaren är brusig för enmansbranscher. En
   manuell genomgång av kandidatlistan ingår i protokollet.
6. **Annonser roterar.** En enstaka mätning är en ögonblicksbild. Tre rundor och M5 finns för
   att kvantifiera det i stället för att dölja det.
7. Shoppingannonser samlas in men ingår inte i huvudmåtten.

## Tillägg

**2026-09-04: studien använder en enda insamlingskälla.** Beslutat innan någon analys kördes.
Vad som ersätter en andra källa står i `docs/metod.md`.

**2026-09-04: kravet på spridning mellan rundor mjukades upp.** Från "minst fem kalenderdagar"
till "minst två olika veckodagar, täckande en vardagsförmiddag, en vardagskväll och en
helgdag". Runda 2 och 3 var inte insamlade vid tillägget. Kravet som ersattes var godtyckligt;
kravet som infördes är det designen faktiskt vilar på.

**2026-09-04: taxonomin utökades, före all manuell klassificering.** Lade till nivån
`chain_local_branch`: en filial, franchise eller butik som tillhör ett företag med huvudkontor
utanför kommunen men som är bemannad på en fysisk adress inne i kommunen (Specsavers Enköping,
Carglass Enköping, Ludvig & Co Enköping). Tidigare tvingades sådana in antingen i `local_*`,
vilket överdriver lokalt ägande, eller i `external_*`, vilket förnekar att en invånare kan gå
in genom dörren. Den räknas **inte** in i `localCategories`. M1 och M2 publiceras därför i två
läsningar: huvudsiffran exkluderar filialer, medan `m1_local_visibility_incl_branches` och
`m2_leakage_incl_branches` inkluderar dem. Den andra läsningen är den som försvagar studiens
hypotes, vilket är skälet till att den publiceras och inte bara nämns.

En valfri andra dimension lades till, `reach` (`independent`, `national`, `international`), som
anges per annonsör där granskaren fastställer den och lämnas tom annars. Tomt redovisas som
`unresearched` och fylls aldrig i på gissning. `reach` beskriver företagets utbredning;
`category` beskriver fysiskt avstånd till sökaren. Ingen av dem härleds ur den andra.

**2026-09-04: M4 nedgraderades från resultat till räkneexempel.** Före all manuell
klassificering. M4 (omdirigerad efterfrågan i kronor) redovisas inte längre som ett resultat av
studien. Ingångsvärdena är externa jämförelsetal, två av dem amerikanska, och det finns inget
försvarbart enhetligt ordervärde över 49 branscher som spänner från en klippning till ett tak.
Den publiceras nu bara som ett uttryckligen märkt räkneexempel i storleksordning: ett intervall,
aldrig en punktskattning, med en fast brasklapp ("NOT A FINDING") i koden som producerar den,
och uttryckt per 1 000 sökningar eftersom studien inte samlar in sökvolymer. Antaganden utan
källa blockerar inte längre publiceringen av studien, bara räkneexemplet. De uppmätta resultaten
är M1, M2, M3, M5 och, med en kontrollkommun, M6.

**2026-09-04: kontrollkommunen valdes till Falkenberg.** Förregistreringen namngav Sala som
tänkt kontroll. Falkenberg valdes i stället, före all insamling i kontrollkommunen, av två skäl:
folkmängden ligger närmare Enköpings (47 337 mot 48 591, SCB 2024, mot Salas 39 000 i
Google-räckvidd), och Falkenberg ligger i en helt annan annonsörsmarknad (Göteborg och Halmstad
i stället för Stockholm, Uppsala och Västerås). En kontroll i samma annonsörsmarknad kan bara
visa om Enköping är ovanligt; en i en annan marknad prövar om mönstret är nationellt.

**2026-09-12: två analysvarianter tillagda efter manuell klassificering, båda redovisade.**
Redovisas eftersom båda beslutades efter att datan setts, vilket är precis när en variant
behöver redovisas.

1. *Endast vanliga annonser.* Google visar en lokal företagsenhet inuti annonsblocket, med
   företagsnamn, betyg och ingen domän. `m1_local_visibility_standard_ads` och
   `m2_leakage_standard_ads` utesluter den och räknar bara de fyra vanliga textannonserna.
   Redovisas **vid sidan av** huvudsiffran, aldrig i stället för den: enheten är en del av det
   sökaren ser, och den är oproportionerligt ofta lokal, så att ta bort den flyttar
   huvudsiffran åt det håll som gynnar studiens hypotes. Den uppmätta effekten är liten,
   Enköping 92,3 % till 93,2 % och Falkenberg 81,3 % till 81,2 %, vilket i sig är värt att
   publicera.

2. *Förmedlare tillskrivs ingen.* Nationella förmedlingstjänster behåller sin egen kategori och
   räknas aldrig som lokala. Vem som till slut vinner jobbet bakom en förmedlare går inte att se
   från en sökresultatsida, och rapporten måste säga det i stället för att anta att uppdraget
   lämnar kommunen.

**2026-09-12: närvaro per kommun är en mänsklig bedömning, och försöket att automatisera den
misslyckades.** En annonsör bär en klassificering, men en kedja kan ha ett bemannat kontor i en
av studiens kommuner och inte i nästa. `advertiser_market` låter en bedömning per kommun ta över
den studieövergripande; en sådan är registrerad (Hemfrid är en filial i Enköping men inte i
Falkenberg).

En automatisk kontroll skrevs och **dess resultat kasserades**. Körd mot Enköping nedgraderade
den 13 annonsörer vars Enköpingsadresser den mänskliga granskaren redan hade läst av på samma
webbplatser, eftersom nationella kedjor lägger filialadresser på undersidor per ort eller bakom
en butikssökare i JavaScript som en hämtning av rå HTML aldrig ser. Ingenting den producerade
hamnade i databasen.

Följd för rapporten: de 23 annonsörer som förekommer i **båda** kommunerna granskades mot en
Enköpingsadress. `m2_leakage_incl_branches` är därför rimlig för Enköping men **osäker för
Falkenberg**, där det sanna värdet ligger mellan 43,2 % (som klassificerat) och 73,7 % (om
ingen av de 18 overifierade kedjorna har en filial i Falkenberg). Jämförelsen av det
filialinkluderande måttet mellan kommunerna får inte publiceras utan den verifieringen.
Huvudmåtten M1 och M2 påverkas inte: en filial är inte lokal i någon av läsningarna.
