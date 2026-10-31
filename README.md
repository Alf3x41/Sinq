# Sinq

**Zálohuje vaše herné pozície.**

**Verzia 0.2.29 · Windows · Predbežné vydanie**

Sinq je aplikácia pre Windows, ktorá automaticky zálohuje uložené pozície hier a synchronizuje ich medzi počítačmi. Bez účtu, e-mailu a hesla.

Pridaj hru, prepoj svoje PC a pokračuj tam, kde si skončil.

[Stiahnuť Sinq 0.2.29](dist/Sinq-Setup-0.2.29.exe) · [Kontrolný súčet SHA256](dist/Sinq-Setup-0.2.29.exe.sha256) · [Poznámky k vydaniu](RELEASE_README.md)

## Novinky vo verzii 0.2.29

- **Nové detaily chyby** — panel podľa vybranej témy, zrozumiteľné zhrnutie a samostatné rolovateľné technické podrobnosti. Celý výpis možno označiť a skopírovať; panel sa zatvára tlačidlom alebo klávesom Escape.
- **Vycentrovaný úvod** — logo, názov Sinq a podnázov sú usporiadané pod sebou na spoločnej osi. Krátka úvodná animácia plynulo prejde do aplikácie a pri obmedzených animáciách sa preskočí.
- **Čistejšie zobrazenie chyby** — spodné oznámenie sa počas otvorených detailov skryje, takže sa neprekrývajú dve sady ovládacích prvkov.

## Ukážky aplikácie

![Knižnica, pripojené zariadenia, nastavenia a párovanie v štyroch témach Sinq](https://raw.githubusercontent.com/Alf3x41/Sinq/main/prehlad.png)

Snímky sú zachytené priamo z aplikácie s ukážkovými údajmi. Každá používa inú tému; nadpisy a vonkajšie pozadie sú prezentačnou úpravou.

[Samostatné screenshoty a pôvodné snímky](docs/screenshots/0.2.29/README.md) · [32-sekundové video ovládania vo Full HD](docs/video/Sinq-0.2.29-showcase.mp4)

## Čo Sinq dokáže

- **Automatické zálohovanie** — sleduje vybrané priečinky a zálohuje zmenené savy. Zálohu môžeš spustiť aj ručne.
- **Sinq Pair** — prepojí počítače pomocou jednorazového šesťmiestneho kódu.
- **Sinq Cloud** — automaticky prenáša šifrované zálohy medzi pripojenými PC a po výpadku pripojenia skúša synchronizáciu znova.
- **História verzií** — lokálne zachováva staršie savy; cloud uchováva päť posledných verzií každej hry a vždy aktuálnu verziu.
- **Novší save automaticky** — pri rozdielnych verziách tej istej hry použije novšiu celú verziu podľa času zmeny súborov. Staršiu kópiu zachová v histórii.
- **Viac zariadení** — zobrazí pripojené PC a umožní odobrať ich prístup.
- **Beh na pozadí** — zálohovanie pokračuje aj po zatvorení hlavného okna.
- **Prispôsobenie** — animované vzhľady, obmedzenie animácií a podpora viacerých jazykov vrátane slovenčiny a češtiny.
- **Nastavenia jednotlivých hier** — nenápadné tri bodky otvoria nastavenia ochrany a zmenu obalu hry.
- **Prehľadný stav záloh** — pri hre vidíš existujúcu alebo chýbajúcu zálohu, priebeh práce, čakanie, pozastavenie či chybu. Počas zálohovania a prenosu sa zobrazuje kruhový indikátor.

## Začíname

1. Stiahni `Sinq-Setup-0.2.29.exe` a príslušný súbor `.sha256` z aktuálneho vydania. Lokálne zostavenia sú v priečinku [dist](dist/).
2. Vyhľadaj hru v katalógu a pridaj nájdený priečinok so savmi alebo vyber priečinok ručne.
3. Ak chceš synchronizovať druhé PC, vyber **Add PC**. Tento krok môžeš preskočiť cez **Later**.
4. Na druhom počítači nainštaluj rovnakú aktuálnu verziu a pridaj tú istú hru.

**Aktuálny inštalátor pri dokončení prvého kroku vymaže predchádzajúce lokálne údaje Sinq vrátane nastavení, lokálnych záloh a párovacích kľúčov. Pôvodné herné savy zostávajú zachované.** Po opätovnej inštalácii pridaj hry a prepoj PC nanovo. Predchádzajúce cloudové dáta sa tým automaticky neodstránia.

## Prepojenie počítačov

1. Na prvom PC otvor **Devices → Show code**.
2. Na druhom PC vyber **Enter code** a zadaj zobrazených šesť číslic.
3. Nechaj Devices otvorené na oboch počítačoch. Po zadaní poslednej číslice sa pripojenie dokončí automaticky.

Kód sa generuje automaticky, platí **20 minút** a je jednorazový. Kliknutím na zobrazený kód môžeš vytvoriť nový. Zdieľaj ho iba s PC, ktoré chceš pripojiť.

Spodná šípka v Devices otvorí zoznam pripojených zariadení. Odobraté PC sa môže znovu pripojiť pomocou nového kódu.

## Ako funguje synchronizácia

Sinq zálohuje vybraný priečinok so savmi a pri dostupnom pripojení synchronizuje jeho obsah cez cloud. Na všetkých PC pridaj hru pod rovnakým názvom, aby sa jej zálohy priradili k sebe.

Keď sa verzie líšia, rozhoduje najnovší čas zmeny súborov vo vybranom priečinku. Sinq vyberá celú verziu savu; nespája vnútorný obsah herných súborov ani jednotlivé sloty z rôznych verzií. Pred použitím novšieho vzdialeného savu zachová aktuálnu miestnu kópiu v histórii.

Pri rozdielnom obsahu s úplne rovnakým časom zostanú obe verzie zachované ako konflikt. Správny dátum a čas na počítačoch sú preto dôležité. Staršie zálohy bez času zmeny súborov používajú ako náhradný údaj čas vytvorenia zálohy.

Ak má hra save otvorený na zápis, výmena sa odloží. Pre dokončenie synchronizácie hru zatvor a pred spustením na druhom PC over stav zálohy.

## Súkromie a prístup

Savy sa šifrujú na klientskom zariadení pred odoslaním. Server uchováva šifrovaný obsah; súkromné kľúče zostávajú na PC a lokálne poverenia chráni Windows DPAPI.

Sinq nevyžaduje registráciu. Prístup je viazaný na zariadenia a ich kľúče. Odobratie zariadenia zablokuje jeho ďalší prístup k službe; už stiahnuté miestne kópie tým nezmiznú.

Lokálne zálohy fungujú aj bez internetu. Párovanie a cloudový prenos vyžadujú dostupné pripojenie a službu. Cloud má kapacitné limity; pri ich dosiahnutí zápis zlyhá namiesto automatického rozširovania úložiska.

## Obnova a riešenie problémov

V **Settings** môžeš spustiť zálohu, otvoriť priečinok záloh alebo obnoviť vybranú verziu do nového priečinka.

Chybové hlásenia obsahujú vysvetlenie a otvoriteľné úplné podrobnosti s možnosťou kopírovania. Pri chybe pod hrou klikni na jej stav. Používateľské vysvetlenia chýb sú dostupné v 19 jazykoch; pôvodný technický výpis systému alebo servera zostáva nezmenený.

Pri hlásení problému uveď verziu Sinq, verziu Windows, názov hry, postup a podrobnosti chyby. Nezverejňuj párovací kód, obnovovací kľúč ani súkromné kľúče.

## Stav projektu

Sinq je vo fáze **pre-release**. Niektoré časti rozhrania používajú anglický náhradný text. Aktuálne zostavenie je bez digitálneho podpisu a Windows môže zobraziť upozornenie SmartScreen. [Informácie o podpisovaní](docs/windows-signing.md).

Mierka rozhrania sa prispôsobuje pracovnej ploche a DPI pri spustení. Pri presune na monitor s odlišnou mierkou môže byť potrebné aplikáciu znova otvoriť.

Projekt obsahuje Oracle backend aj alternatívne nasadenie cez Cloudflare Workers, R2 a D1. Prevádzkové postupy sú v dokumentácii nižšie.

- [Poznámky k aktuálnemu predbežnému vydaniu](RELEASE_README.md)
- [Prevádzka Oracle backendu](docs/oracle-deployment.md)
- [Nasadenie Cloudflare backendu](docs/cloud-deployment.md)

## Overenie vydania 0.2.29

Prešlo **69 Rust testov**, **6 testov serverového protokolu**, kontroly dlhých chybových hlásení v 19 jazykoch a 10 profilov rozlíšenia a DPI. Úvod bol skontrolovaný aj pri menšom okne; detaily chyby pri rozlíšení 720 × 480.

Výsledný inštalátor prešiel izolovanými kontrolami zálohovania, ochrany pred duplicitným spustením a manuálneho zálohovania pri pozastavených automatických zálohách. Overená bola verzia EXE a SHA256. V tomto vydaní neprebehlo overenie živej cloudovej služby. [Podrobná správa vydania](docs/release-0.2.29.md).

## Vývoj

Projekt používa **Rust** a **Slint**. Na zostavenie potrebuješ Windows, Rust s MSVC nástrojmi a Node.js 24 alebo novší na protokolové testy.

```powershell
cargo test --workspace --locked
node --test cloud/oracle.test.mjs cloud/worker.test.mjs
cargo run -p sinq --locked
```

Nový inštalátor vytvoríš existujúcim release skriptom:

```powershell
./scripts/release.ps1
```

Skript spustí testy, zostaví aplikáciu a vytvorí nový `Sinq-Setup-x.x.x.exe` s kontrolným súčtom SHA256. Existujúce vydania neprepisuje. Ďalšie kontroly rozhrania a zálohovania sú v priečinku [scripts](scripts/).

## Licencia

Sinq je dostupný pod licenciou [MIT](LICENSE).
