# Klarspråk

Svensk motsvarighet till Hemingway Editor. En enda fil, `index.html` — öppna den i webbläsaren,
ingen server och ingen installation. Texten sparas lokalt i webbläsaren mellan besöken.

**Live:** https://alovio-klarsprak.vercel.app

Vill du ha en lokal adress: `python3 -m http.server 4173` i den här mappen.

## Vad den mäter

Hemingways betyg bygger på engelsk stavelseräkning och går inte att översätta. Klarspråk kör
**LIX** (Björnsson) istället: meningslängd plus andel ord längre än sex tecken.
Under 30 är mycket lätt, 30–40 lätt, 40–50 medel, 50–60 svår, över 60 byråkrati.

Enskilda meningar bedöms däremot **bara på längd**. Det var ett medvetet byte. Först vägdes
andelen långa ord in också, men mätt på 344 000 meningar avgjorde den bara 0,1 procent av fallen —
och till priset av att en gul mening kunde betyda två olika saker utan att säga vilken. Nu betyder
gult exakt en sak: meningen är lång. Ordrikedomen syns i stället som andelen långa ord i måtten
och som krångelord ute i texten.

**Var gränsen går, och varför.** Hemingway publicerar inga trösklar; deras hjälpsida säger bara
att gult är svårt och rött svårare. Uppmätt på deras egen app lämnas en mening på 33 ord med
enkla ord helt omarkerad, gult kommer runt 36 ord och rött runt 44. Svenska ord är längre än
engelska, så gränserna här är satta lägre: **25 ord för gult, 35 för rött**. Det färgar 17 procent
av meningarna i eget verkligt material. Tidigare låg gult på 20 ord, vilket färgade var tredje
mening och gjorde färgen meningslös.

## Sju markeringar

| Färg | Vad |
|---|---|
| Röd | Mycket lång mening: 35 ord och uppåt |
| Gul | Lång mening: 25 ord och uppåt |
| Lila | Krångelord och anglicismer. De som går att byta rakt av får ett förslag (`erhålla → få`, `insight → insikt`); de vars ersättning skulle bryta meningen (`dock`, `omfatta`, `i samband med`) märks bara ut med "skriv om" |
| Blå | Adverb och försvagande fraser — `-ligen`, `-vis`, `-mässigt` plus en lista |
| Grön | Passiv form — s-passiv och `bli` + perfektparticip |
| Rosa | Upprepningar och pleonasmer (`helt och hållet`, dubblerade ord) |
| Orange | Negationer. Avstängd som default, `inte` är för vanligt för att markeras hela tiden |

Klicka i listan för att stänga av eller sätta på en färg. Valet sparas. Adverb och passiv form
har ett måltal som skalar med textens längd — en text på tjugo meningar tåler fler adverb än en
på fyra. Ligger du över blir siffran orange.

## Vid markören

Ställ markören i texten så visar panelen överst varför just det stället är markerat: vilket ord
det gäller, varför det är ett problem och vad du kan skriva i stället. Är meningen färgad står det
också vad som utlöste färgen — antal ord eller andel långa ord. En färg utan förklaring är bara
en tillsägelse, och det var det som skilde mest mot Hemingway.

Två sätt att byta ord. **Byt bara den här** i markörrutan ändrar exakt den förekomsten.
**Byt alla** i listan längre ner ändrar hela texten på en gång, vilket går fort men bara är
säkert för ord som betyder samma sak överallt.

Panelen "Nio regler för bra text" följer Alex Hormozis skrivregler
([källa](https://www.youtube.com/watch?v=qe6A9wsZxGM)): enkla ord, presens, aktiv form, inga adverb,
korta meningar, max ett komma, positivt språk, inga upprepningar, låg läsbarhetströskel.

## Träffsäkerhet

Passiv form och adverb hittas med ändelsemönster och ordlistor, inte med grammatisk analys.
Två kända gränsfall är hanterade: deponensverb (`hoppas`, `trivs`, `umgås`) markeras inte som
passiv, och supinum (`-ats`, `-its`) kräver ett hjälpverb i närheten så att substantiv som
`insats` och genitiv som `resultats` inte fastnar. Enstaka fel finns ändå kvar — markeringen är
ett förslag, inte en dom.

Testat med 54 passivfall, 14 fall av meningsdelning och 33 presens-passiver, alla rätt. Varje
ordpar i `KRANGEL` är dessutom provat som faktiskt utbyte i en riktig mening: de tjugotre som gav
ogrammatisk text flyttades till `KRANGEL_FLAGGA`, där ordet märks ut men ingen knapp erbjuds. Motorn klarar
17 000 ord på 7 ms, så den hinner alltid med skrivandet.

**Där den är osäker.** Adverb på -t går inte att skilja från neutrumadjektiv utan grammatisk
analys. Listan tar med de vanligaste försvagande orden ändå (`väldigt`, `totalt`, `fullständigt`),
vilket betyder att `ett totalt haveri` märks ut trots att ordet där är ett adjektiv. Detsamma
gäller ändelsen -mässigt: `affärsmässigt` fastnar oavsett funktion. Stäng av den blå färgen i
nyckeln om det stör mer än det hjälper.

`är` + perfektparticip (`rapporten är skriven`) märks inte som passiv, eftersom `är` följt av
adjektiv är så vanligt att markeringen skulle bli brus. Omskriven passiv med `bli` fångas däremot.

**En regel som togs bort.** Meningar med två eller fler kommatecken färgades först gula. Mätt på
423 000 meningar ur eget material blev 8,4 procent gula enbart på den regeln, med medianpoäng 21
mot tröskeln 43 — den träffade uppräkningar, inte tunga meningar. Kommadisciplinen har kvar sin
egen rad bland de nio reglerna.

Ordlistorna ligger överst i `index.html` under `KRANGEL`, `KRANGEL_FLAGGA`, `ADVERB`,
`PASSIV_ORD`, `NEGATION` och `UPPREPNING`. Vill du tysta en felmarkering går du istället till
`INTE_PASSIV`, `INTE_PARTICIP` eller `GENITIV_FORE`. Lägg till ord där när du hittar något som saknas.
