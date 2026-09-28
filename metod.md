# Metod

Så här gjordes studien *Google Ads i Enköping: lokala företag syns sällan i annonserna*.
Rapporten finns på [adsbyråenköping.se](https://adsbyråenköping.se/blogg/lokala-foretag-syns-sallan-i-google-ads).

## Insamling

Sökresultaten hämtades via en kommersiell tjänst som samlar in Googles sökresultat, riktade mot
kommunen, alltså som om sökningen gjordes där. Aldrig via ett eget Google-konto eller en egen
uppkoppling. Varje sökning gjordes på svenska Google (`gl=se`, `hl=sv`) med tjänstens
annonsoptimerade hämtning påslagen, eftersom tjänsten annars missar en del annonser. Tjänstens
namn anges inte här men uppges på förfrågan.

49 branscher söktes i fem varianter: "elektriker enköping", "elektriker i enköping", "bästa
elektriker enköping", "akut elektriker enköping" och "elektriker nära mig". Varje sökning
gjordes på mobil och dator, vid tre tillfällen per kommun den 4–7 september 2026: en vardag
mitt på dagen, en vardagskväll och en helgförmiddag. Totalt 2 940 sökresultatsidor.

Falkenberg mättes på samma sätt som jämförelse. Kommunen är lika stor som Enköping men har
Göteborg och Halmstad som närmaste storstäder, i stället för Stockholm, Uppsala och Västerås.

Före insamlingen testades tjänsten på tio sökord där annonser nästan alltid visas. I ett av tre
test kom två av de tio tillbaka utan annonser, så en del sökningar utan annonser i datan kan
vara missade annonser. Huvudsiffran räknas bara på sökningar där annonser visades.

## Kontroll mot Google

Eftersom insamlingen gjordes via en enda tjänst kontrollerades den direkt mot Google den 28
september 2026. 30 av sökningarna, sex branscher i alla fem varianter, gjordes på dator i en
vanlig webbläsare på en internetuppkoppling i Enköping, utan inloggning och med cookies avvisade.
Samma sökningar hämtades via tjänsten inom samma minuter.

- **Lokalt företag bland de fyra översta:** samma svar i 28 av 30 sökningar. I båda fallen där
  svaren skilde sig såg tjänsten ett lokalt företag som webbläsaren inte såg, så tjänsten verkar
  inte missa lokala företag.
- **Samma annonsör överst:** i 9 av de 16 sökningar där båda visade annonser. Förstaplatsen
  skiftar dock från sökning till sökning. När tio av sökningarna gjordes om fem minuter senare
  hade tjänsten samma annonsör överst i 3 av 8 fall och webbläsaren i 7 av 8. Därför är det
  utfallet huvudsiffran bygger på, lokalt företag eller inte, som jämförs.
- **Missade annonser:** tjänsten hittade inga annonser överst i 9 sökningar där webbläsaren
  visade annonser, oftast "nära mig" och "bästa". Andelen sökningar med annonser är därför
  troligen högre än datan visar. Huvudsiffran räknas bara på sökningar där annonser visades,
  och ingen av de nio hade ett lokalt företag bland de fyra översta annonserna.

## Vad som räknas

De fyra översta textannonserna, alltså annonsblocket ovanför de vanliga sökresultaten,
inklusive Googles annonser för lokala företag när de visas där. Annonser längre ner på sidan
och shoppingannonser räknas inte.

## Finns det lokala företag?

Antalet lokala företag per bransch kommer från SCB:s företagsregister: aktiva arbetsställen
med adress i kommunen, där "aktiv" är SCB:s egen definition. Antalen hämtades med SCB:s
Antalsräknare, och varje antal har ett RäkningsId som låter SCB återskapa exakt samma fråga.
Räknaren ger hellre för låga än för höga antal, och det är den säkra riktningen här: det räcker
att veta att det finns minst ett lokalt företag.

En bransch räknas bara med i huvudsiffran om registret säkert visar minst ett lokalt företag.
37 av 49 branscher klarade det. I några av dem visades inga annonser alls, så huvudsiffran
bygger på 33 branscher i Enköping och 32 i Falkenberg.

Inga personuppgifter sparas. En enskild firma har ägarens personnummer som
organisationsnummer, så organisationsnummer kastas när registret läses in.

## Klassificering

Varje annonsör bedömdes en gång, utifrån var företaget faktiskt har verksamhet:

- **Lokalt företag:** har sin bas i kommunen.
- **Kedja med lokalt kontor:** huvudkontor någon annanstans, men bemannat kontor eller butik i
  kommunen.
- **Förmedlingstjänst:** offertsajter och liknande.
- **Externt företag som nämner orten**, och **externt företag som inte nämner orten:** ingen
  verksamhet i kommunen.

Först kontrollerades annonsörens webbplats automatiskt efter en postadress i kommunen, skriven
som svenska adresser skrivs ("745 31 Enköping"). Ett ortnamn i en lista över
verksamhetsområden räknas inte som närvaro. Sedan granskades de 100 största annonsörerna för
hand, liksom de flesta som kunde vara lokala. Varje bedömning sparades med sitt underlag.
Samma företag räknas en gång även om det syns i olika annonsformat. 1,0 % av annonserna i
Enköping kom från annonsörer som inte gick att klassa.

## Så anges siffrorna

Andelarna räknas på sökningar där det visades annonser. En sökresultatsida utan annonser har
inget klick att förlora, och att räkna med den skulle blåsa upp siffran. Huvudsiffran lyder
därför: i N % av sökningarna där det visades annonser, och där det finns ett lokalt företag i
branschen, fanns inget lokalt företag bland de fyra översta annonserna. Datasetet innehåller
också en strängare variant som räknar med sökningar utan annonser.

Osäkerheten anges som 95-procentiga konfidensintervall med branschen som enhet, eftersom samma
sökning mäts flera gånger och sökningar inom samma bransch hänger ihop. Intervallen tas fram
genom att branscherna där annonser visades dras om slumpvis med återläggning många gånger och
andelen räknas om varje gång, en så kallad bootstrap.

## Datasetet

Det publicerade datasetet är sammanställt per kommun, bransch, sökvariant och enhet, och
innehåller inga företagsnamn, domäner eller adresser. Rådatan finns sparad hos oss.
