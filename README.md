# Sinq

![Verzia](https://img.shields.io/badge/verzia-0.2.4-blue) ![Platforma](https://img.shields.io/badge/platforma-Windows_10%20%7C%2011-0078D4)

Sinq je natívna aplikácia pre Windows na automatické zálohovanie uložených pozícií hier a ich prenos medzi počítačmi. Sleduje vybrané priečinky, uchováva históriu záloh a umožňuje obnoviť zvolenú verziu do nového priečinka.

> [!NOTE]
> **Verzia 0.2.4 je vývojová ukážka.** Aplikácia aj inštalátor sú zatiaľ bez digitálneho podpisu.

## Čo Sinq dokáže

- **Automatické zálohy:** zmeny v sledovanom priečinku spustia zálohovanie po krátkom ustálení zápisu. Zálohu možno vytvoriť aj ručne.
- **História verzií:** rovnaký obsah sa ukladá iba raz; dokončené revízie zostávajú dostupné aj po odstránení pôvodného súboru.
- **Bezpečná obnova:** pred obnovou overí kontrolné súčty a vytvorí nový priečinok `Sinq-restored-<id>`. Existujúce herné súbory neprepisuje.
- **Knižnica hier:** vyhľadávanie v pribalenom katalógu, zisťovanie podporovaných umiestnení uložených pozícií a ručný výber priečinka.
- **Sinq Pair:** spárovanie počítačov pomocou šesťmiestneho kódu a schválenia na existujúcom počítači.
- **Sinq Cloud:** šifrovaný prenos záloh; vzdialené a konfliktné verzie sa ukladajú do histórie na vedomú obnovu.
- **Beh na pozadí:** po zatvorení okna pokračuje samostatný proces bez vykresľovania rozhrania.
- **Prispôsobenie:** štyri animované vzhľady, obmedzenie pohybu a jazykové katalógy vrátane slovenčiny a češtiny. Nedokončené preklady používajú anglický náhradný text.

## Inštalácia a prvé spustenie

1. Spusti `Sinq-Setup-0.2.4.exe` z priečinka [dist](dist/).
2. Vyber jazyk a dokonči inštaláciu. Predvolené umiestnenie je `%LOCALAPPDATA%\Programs\Sinq`; administrátorské oprávnenia nie sú potrebné.
3. Vyhľadaj hru a pridaj nájdený priečinok s uloženými pozíciami alebo ho vyber ručne.
4. Voliteľne pripoj ďalší počítač. Tento krok môžeš preskočiť cez **Later**.

Inštalátor vytvorí odkazy v ponuke Štart a na ploche a nastaví spúšťanie pri prihlásení. Spúšťanie aj automatické zálohovanie možno upraviť v nastaveniach. Vypnutie automatického zálohovania ponecháva dostupnú ručnú zálohu.

Opätovná inštalácia obnoví predvolené nastavenia a vyprázdni zoznam pridaných hier pri zachovaní zvoleného jazyka. Herné súbory aj existujúce zálohy zostávajú zachované. Odinštalovanie ponechá nastavenia, lokálne zálohy aj herné priečinky.

## Spárovanie počítačov

1. Na existujúcom počítači otvor **Devices → Show code**.
2. Na druhom počítači vyber **Enter code** a zadaj šesťmiestny kód. Po zadaní poslednej číslice sa požiadavka odošle automaticky.
3. Na existujúcom počítači porovnaj odtlačky zariadení a potvrď pripojenie.

Kód platí 20 minút, po uplynutí platnosti sa obnoví a kliknutím na číslice možno vytvoriť nový. Správa zariadení a obnova prístupu sú dostupné v nastaveniach.

Klient predvolene používa službu opísanú v [prevádzkovej dokumentácii Oracle](docs/oracle-deployment.md). Používateľ nezadáva adresu služby, účet ani administrátorské prihlasovacie údaje. Lokálne kľúče chráni Windows DPAPI. Prenos vzdialenej zálohy neprepisuje živé uložené pozície hry.

## Spustenie zo zdrojového kódu

### Požiadavky

- Windows 10 alebo 11.
- Stabilný Rust s nástrojmi MSVC a podporou edície 2024.
- Visual Studio C++ Build Tools a Windows SDK.
- Node.js 24 alebo novší pre integračné a protokolové testy.
- npm pre vývoj a nasadenie voliteľného Cloudflare backendu.

Nasledujúce príkazy spusti v koreňovom priečinku projektu:

```powershell
cargo build --release -p sinq --locked
.\target\release\sinq.exe
```

Na vývojové spustenie:

```powershell
cargo run -p sinq --locked
```

Ak systém nenájde `cargo`, skontroluj, či je `%USERPROFILE%\.cargo\bin` v premennej `PATH`.

### Režimy aplikácie

Jeden spustiteľný súbor poskytuje rozhranie, proces na pozadí aj inštaláciu:

```powershell
.\target\release\sinq.exe --install
.\target\release\sinq.exe --daemon
.\target\release\sinq.exe --uninstall
```

Súbor pomenovaný `Sinq-Setup-<verzia>.exe` otvorí inštaláciu automaticky. Zámky procesov bránia súbežnému spusteniu viacerých bežných okien alebo viacerých procesov zálohovania nad rovnakými dátami.

## Dáta a obnova

Predvolené dátové umiestnenie:

```text
%LOCALAPPDATA%\Sinq\data\
├── settings.json       # nastavenia aplikácie
└── backups\
    ├── objects\        # obsah súborov identifikovaný SHA-256
    └── manifests\      # popisy jednotlivých revízií
```

Pre izolované testovanie možno nastaviť absolútnu cestu cez `SINQ_DATA_DIR`:

```powershell
$env:SINQ_DATA_DIR = Join-Path $PWD 'target\sinq-local-data'
cargo run -p sinq --locked
```

> [!IMPORTANT]
> Dátový priečinok Sinq nikdy nenastavuj na priečinok s hernými pozíciami.

Po testovaní premennú v aktuálnom termináli zrušíš príkazom `Remove-Item Env:SINQ_DATA_DIR`.

Zálohy používajú nemenné objekty a atómové publikovanie dokončených revízií. Ak sa súbor počas kontroly zmení alebo ho nemožno prečítať, pokus zlyhá a neskôr sa zopakuje s rastúcim odstupom.

## Štruktúra projektu

| Cesta | Obsah |
| --- | --- |
| `crates/core/` | Konfigurácia, sledovanie súborov, zálohy, obnova a cloudový klient |
| `crates/desktop/` | Rozhranie Slint, katalóg hier, obrázky, inštalátor a integrácia s Windows |
| `crates/service/` | Starší prototyp služby s odlišným párovaním a bezpečnostným modelom |
| `cloud/` | Spoločný protokol, Oracle adaptér, voliteľný Cloudflare Worker, migrácie a testy |
| `locales/` | Preklady vo formáte Fluent |
| `scripts/` | Zostavenie vydania a overovacie skripty |
| `docs/` | Technická dokumentácia, prevádzka a správy z overovania |
| `dist/` | Inštalátory a kontrolné súčty vydaní |

Desktop používa **Rust, Slint a Tokio**. Aktuálny Oracle backend používa Node.js, SQLite a súborové úložisko šifrovaných objektov. Voliteľné nasadenie na Cloudflare používa Worker, D1 a R2.

## Overovanie a vydanie

Základné kontroly:

```powershell
cargo fmt --all -- --check
cargo test --workspace --locked
node --test cloud/oracle.test.mjs cloud/worker.test.mjs
```

Testy workspace vyžadujú Node.js pre lokálny HTTP integračný test. Test produkčnej služby je predvolene ignorovaný; postup jeho samostatného spustenia opisuje [dokumentácia Oracle](docs/oracle-deployment.md).

Overenie rozhrania po vytvorení vývojovej zostavy:

```powershell
cargo build -p sinq --locked
.\scripts\verify-layout.ps1
.\scripts\verify-onboarding.ps1
.\scripts\verify-pairing.ps1
```

Skripty vytvárajú izolované dáta a zachytené snímky v `target/`. Ďalšie kontroly sú opísané v [dokumentácii overovania](docs/verification.md).

Vytvorenie distribučného inštalátora:

```powershell
.\scripts\release.ps1
```

Skript spustí testy, zostaví aplikáciu a do `dist/` uloží inštalátor aj súbor `.sha256`. Verziu preberá z koreňového `Cargo.toml`. Ak rovnaké vydanie už existuje, skončí bez jeho prepísania. Vydavateľa možno nastaviť parametrom `-Publisher`; pri samostatnom zostavení sa používa premenná `SINQ_PUBLISHER`.

## Obmedzenia vývojovej verzie

- Sledovanie súborov nezaručuje transakčnú snímku celej hry počas zápisu viacerých súborov. Pri citlivých uložených pozíciách vytváraj zálohu po ukončení hry.
- Katalóg nezaručuje úplné pokrytie každej hry. Nepodporované vzory ciest a pozície uložené iba v registri vyžadujú iný postup; pri dostupných súboroch možno vybrať presný priečinok ručne.
- Lokálna história záloh sa automaticky nečistí a môže postupne zaberať viac miesta.
- Cloudová služba má limity úložiska a prenosu. Aktuálne nasadenie nemá nezávislú zálohu mimo servera; zachovaj si lokálne kópie. Konkrétne limity uvádza [prevádzková dokumentácia](docs/oracle-deployment.md).
- Inštalátory nie sú digitálne podpísané. Overenie rozloženia rozhrania nepotvrdzuje výkon na konkrétnom handhelde ani natívne ovládanie gamepadom.

## Ďalšia dokumentácia

- [Overenie vydania 0.2.4](docs/release-0.2.4.md)
- [Prevádzka aktuálneho Oracle backendu](docs/oracle-deployment.md)
- [Voliteľné nasadenie na Cloudflare](docs/cloud-deployment.md)
- [Overovacie postupy](docs/verification.md)
- [Architektúra a bezpečnostné hranice](docs/architecture.md) — obsahuje aj historický opis staršieho prototypu; pre aktuálny cloud použi prevádzkovú dokumentáciu a správu k vydaniu 0.2.4.

## Licencia

Zdrojový kód Sinq je dostupný pod licenciou [MIT](LICENSE). Závislosti si ponechávajú vlastné licencie. Oznámenie k pribalenému katalógu je v [catalog-LICENSE.txt](crates/desktop/assets/catalog-LICENSE.txt). Pred verejnou distribúciou skontroluj licenčné podmienky Slint.

