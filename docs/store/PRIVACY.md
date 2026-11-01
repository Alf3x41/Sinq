# Sinq — zásady ochrany súkromia / Privacy policy

Aktualizované / Updated: 31 October 2026

[![Made with Slint](https://raw.githubusercontent.com/slint-ui/slint/master/logo/MadeWithSlint-logo-whitebg.png)](https://slint.dev)

## Slovensky

Sinq vydáva Alex Polák. Kontakt na podporu a žiadosti týkajúce sa osobných údajov: **alfexxx@proton.me**.

**Lokálne údaje.** Sinq ukladá nastavenia, vybrané cesty k herným pozíciám, zálohy, históriu revízií, obrázky hier a diagnostické súbory na vašom počítači. Obsah lokálnych záloh nie je šifrovaný šifrovaním Sinq Cloud. Citlivé párovacie kľúče uložené v lokálnom profile sú vo Windows chránené pomocou DPAPI. Nevkladajte do priečinka na zálohovanie súbory, ktoré nechcete spracúvať.

**Sinq Cloud a Pair.** Cloudová služba prijíma šifrovaný obsah záloh a šifrované manifesty, identifikátory priestoru, hry a revízie, verejné kľúče zariadení, názvy zariadení, čas posledného spojenia, veľkosti a identifikátory uložených objektov. Pri párovaní spracúva dočasný kód a žiadosť o schválenie zariadenia. Šifrovací kľúč priestoru vzniká na zariadení a server ho nedostáva v otvorenej podobe. Používateľský účet s menom a heslom sa nevyžaduje.

**Sieť a prevádzka.** Služba používa HTTPS. Server pri spojení vidí IP adresu a používa ju na obmedzenie počtu požiadaviek. Hosting a prevádzkové záznamy môžu obsahovať sieťové a chybové údaje. Produkčná služba beží na Oracle Cloud Infrastructure. Poskytovateľ hostingu môže spracúvať technické údaje podľa vlastných podmienok. Tento dokument nesľubuje konkrétne geografické umiestnenie ani nepretržitú dostupnosť služby.

**Obrázky hier.** Automatické vyhľadávanie obalov používa SteamGridDB a jeho distribučné servery. Týmto službám sa môže odoslať vyhľadávaný názov hry alebo jej Steam identifikátor; ako pri bežnom webovom spojení uvidia aj IP adresu. Herné pozície sa na tieto služby neposielajú. Vlastný obrázok môžete vybrať lokálne.

**Uchovávanie a vymazanie.** Lokálne údaje zostávajú v profile aplikácie do odstránenia. Odinštalovanie Store aplikácie spravuje Windows; samostatné priečinky pôvodných herných pozícií sa tým nemažú. Odinštalovanie ani odobratie zariadenia automaticky nevymaže cloudovú históriu. Cloudová história môže byť uchovávaná do vymazania prevádzkovateľom; nepoužívané objekty a dočasné párovacie údaje sa čistia pri údržbe. O vymazanie cloudového priestoru alebo informácie o údajoch požiadajte na uvedenom e-maile. Na bezpečné vybavenie žiadosti môže byť potrebné overiť oprávnenie k priestoru. Nikdy neposielajte súkromné kľúče, recovery súbor ani obsah pozícií do verejného GitHub issue.

**Microsoft Store.** Microsoft spracúva údaje o distribúcii, inštalácii a prípadnej diagnostike podľa svojich podmienok a nastavení Windows. Tieto údaje nie sú totožné s obsahom cloudových záloh Sinq.

Pri podpore posielajte len údaje potrebné na vyriešenie problému. Ak máte otázku k prístupu, oprave alebo odstráneniu svojich údajov, kontaktujte vydavateľa. Podstatné zmeny týchto zásad budú uvedené v aktualizovanej verzii dokumentu.

## English

Sinq is published by Alex Polák. Contact for support and privacy requests: **alfexxx@proton.me**.

**Local data.** Sinq stores preferences, selected game save paths, backups, revision history, game images and diagnostic files on your PC. Local backup contents are not encrypted by Sinq Cloud encryption. Sensitive pairing credentials stored in the Windows profile are protected with DPAPI. Only select folders whose contents you intend Sinq to process.

**Sinq Cloud and Pair.** The service receives encrypted save contents and encrypted manifests, space, game and revision identifiers, device public keys and names, last-connection times, and stored object identifiers and sizes. Pairing processes a temporary code and a device approval request. The space encryption key is generated on the device and is not sent to the server in plaintext. A username/password account is not required.

**Network and operations.** Connections use HTTPS. The server sees the connecting IP address and uses it for request limiting. Hosting and operational logs may contain network and error data. The production service runs on Oracle Cloud Infrastructure, whose provider may process technical data under its own terms. This policy does not promise a particular hosting region or uninterrupted availability.

**Game images.** Automatic cover lookup uses SteamGridDB and its distribution servers. A game name or Steam ID may be sent to them, and they see the connecting IP address. Game saves are not sent to those image services. You can select a local image instead.

**Retention and deletion.** Local data remains in the application profile until removed. Windows manages Store app removal; original game save folders outside the app profile are not removed by Sinq. Uninstalling or revoking a device does not automatically delete cloud history. Cloud history may remain until removed by the operator; maintenance cleans unused objects and temporary pairing data. Request cloud-space deletion or information about your data by email. Verification of authority over the space may be necessary. Never post private keys, recovery files or save contents in public GitHub issues.

**Microsoft Store.** Microsoft processes distribution, installation and possible diagnostics under its own terms and Windows settings. These are separate from Sinq cloud backup contents.

Send only information necessary for support. Contact the publisher about access, correction or deletion requests. Material policy changes will appear in an updated document.
