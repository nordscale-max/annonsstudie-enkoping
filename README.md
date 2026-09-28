# Lokala företag i Googles annonser, Enköping och Falkenberg

Data och metod till studien *Google Ads i Enköping: lokala företag syns sällan i annonserna* av
Max-William Björklund, Adsbyrå Enköping. Läs rapporten på
[adsbyråenköping.se](https://adsbyråenköping.se/blogg/lokala-foretag-syns-sallan-i-google-ads).

- **Insamlat:** 4–7 september 2026
- **Licens:** CC BY 4.0. Använd fritt, men ange källa.

## Kort om studien

Vi sökte på Google efter 49 lokala tjänster i fem varianter, som "elektriker enköping" och
"elektriker nära mig", på mobil och dator vid tre tillfällen. Samma sökningar gjordes i
Falkenberg som jämförelse. Totalt blev det 2 940 sökresultatsidor. För varje annons bland de fyra
översta avgjorde vi om företaget har sin bas i kommunen.

I 92,3 % av sökningarna i Enköping där det visades annonser, och där det finns lokala företag i
branschen, fanns inget lokalt företag bland de fyra översta. I Falkenberg var siffran 81,3 %.

Hur det gick till står i [metod.md](metod.md).

## Filer

| Fil | Innehåll |
|---|---|
| `branschtabell.csv` | Vilka typer av annonsörer som syns, per kommun och bransch. Underlaget till diagrammen i rapporten. |
| `dataset.csv` | Alla mått per kommun, bransch, sökvariant och enhet. 1 800 rader. |
| `metod.md` | Hur studien gjordes. |
| `forregistrering.md` | Det vi skrev ned innan insamlingen. |

## Kolumner i `branschtabell.csv`

En rad per kommun och bransch. Andelarna gäller de fyra översta annonserna och summerar till 1.
Branscher med få annonser är med här, men diagrammen i rapporten visar bara branscher med minst
15 annonser.

| Kolumn | Betydelse |
|---|---|
| `annonser_topp4` | Antal annonser som raden bygger på |
| `andel_lokalt` | Företag med sin bas i kommunen |
| `andel_kedja_lokalt_kontor` | Kedjor med huvudkontor någon annanstans, men kontor eller butik i kommunen |
| `andel_formedlare` | Offertsajter och förmedlingstjänster |
| `andel_externt_namner_orten` | Företag utan verksamhet i kommunen som ändå skriver ortsnamnet i annonsen |
| `andel_externt_namner_inte_orten` | Företag utan verksamhet i kommunen som inte nämner orten |
| `andel_oklassat` | Gick inte att avgöra |
| `andel_internationella` | Annonsörer från andra länder. Inte helt undersökt, så siffran är snarare för låg |

## Kolumner i `dataset.csv`

Rader med `alla` är sammanslagna, så raden `enkoping, alla, alla, alla` är Enköpings totalsiffror.
Andelar anges som tal mellan 0 och 1.

| Kolumn | Betydelse |
|---|---|
| `kommun` | `enkoping` eller `falkenberg` |
| `bransch` | Bransch, eller `alla` |
| `sokvariant` | `ort` ("elektriker enköping"), `i_ort` ("elektriker i enköping"), `basta` ("bästa elektriker enköping"), `akut` ("akut elektriker enköping"), `nara_mig` ("elektriker nära mig"), eller `alla` |
| `enhet` | `mobil`, `dator` eller `alla` |
| `sokresultatsidor` | Antal sökresultatsidor |
| `sidor_med_annonser` | Hur många av dem som visade annonser överst |
| `andel_utan_annonser` | Andel sidor utan annonser överst |
| `andel_lokalt_forst` | Andel av sidorna med annonser där ett lokalt företag låg först |
| `andel_utan_lokalt_foretag` | **Huvudsiffran.** Andel av sidorna med annonser, i branscher där det finns lokala företag, där inget lokalt företag fanns bland de fyra översta |
| `underlag` | Antal sidor som huvudsiffran räknas på |
| `andel_utan_lokalt_foretag_alla_sidor` | Samma, men sidor utan annonser räknas också. En strängare variant |
| `andel_lokalt_forst_inkl_kedjor` | Som `andel_lokalt_forst`, men kedjor med kontor i kommunen räknas som lokala |
| `andel_utan_lokalt_inkl_kedjor` | Som huvudsiffran, men kedjor med kontor i kommunen räknas som lokala |
| `andel_externa_som_namner_orten` | Andel av annonserna från företag utan verksamhet i kommunen som ändå skriver ortsnamnet |
| `andel_oklassat` | Andel av annonserna från annonsörer som inte gick att klassa |

## Bra att veta

- Två kommuner säger något om Enköping och Falkenberg, inte om hela Sverige.
- Annonserna byts ut hela tiden. Gör du om sökningarna får du andra annonsörer, men andelen utan
  lokala företag var stabil vid alla tre tillfällena.
- Kedjorna kontrollerades mot adresser i Enköping, så kolumnerna som räknar in kedjor är osäkra
  för Falkenberg.

## Vem som gjort studien

Max-William Björklund driver Nordscale och dess lokala byrå Adsbyrå Enköping, som säljer hjälp med
Google Ads, alltså det studien visar att många lokala företag saknar. Därför är metod och data
öppna, så att vem som helst kan kontrollera siffrorna.

Registerdata från SCB:s företagsregister, egen bearbetning.
