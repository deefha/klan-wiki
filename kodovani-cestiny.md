# Kódování češtiny

V textových i binárních souborech KLANu je pro textové řetězce použit **Kód Kamenických** \(Bratři Kameničtí, KEYBCS2, nesprávně CP895\). Tato znaková sada byla pro kódování češtiny a slovenštiny na počítačích s MS-DOS nejrozšířenější v 80.-90. letech 20. století. Časopis KLAN začal vycházet v roce 1996, jedná se tedy o řešení odpovídající době vzniku a dostupným technologiím.

S nástupem OS Windows 95 byl ovšem Kód Kamenických postupně vytlačován znakovou sadou Windows-1250, naopak ve světě OS typu UN\*X byla pro češtinu a slovenštinu vždy používána znaková sada ISO 8859-2. Začátek 21. století pak konečně znamenal i začátek nahrazování všech lokálních znakových sad komplexním kódováním - normou Unicode \(tedy UTF-8/16/32\). Díky tomu zmizel Kód Kamenických v propadlišti dějin a práce s texty, které tuto znakovou sadu používají, dnes není úplně jednoduchá.

## Konverze

Pro převod souborů v textovém módu lze s úspěchem použít utilitu `cstocs` \(Kód Kamenických zde má označení `kam`\), textové řetězce v binárních souborech je ale nutné zpracovávat "ručně" při samotném parsování. Kromě modulu `Cz::Cstocs` pro jazyk Perl totiž neexistuje oficiální podpora Kódu Kamenických v žádném programovacím jazyce, což je vlastně celkem logické.

Dalším drobným problémem je **několik znaků a symbolů, které v původním Kódu Kamenických nejsou**, ale KLAN je ve svém rozhraní přesto zobrazuje. Běží totiž v plně grafickém režimu a pro renderování textů používá vlastní sadu rastrových fontů, které jsou zcela nezávislé na prostředí MS-DOS / OS Windows. Díky tomu lze na libovolné pozici znakové sady zobrazit jakýkoliv jiný znak nebo symbol, čehož KLAN využívá zejména v poslední čtvrtině znakové tabulky. Tyto výjimky je opět nutné podchytit ad hoc.

## Tabulka tisknutelných znaků

Znaky 0-127 odpovídají standardní ASCII tabulce.

| Dec | Hex | Znak | Unicode | UTF-8 | Poznámka |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **32** | 0x20 | SP | SPACE | 0x0020 |  |
| **33** | 0x21 | ! | EXCLAMATION MARK | 0x0021 |  |
| **34** | 0x22 | " | QUOTATION MARK | 0x0022 |  |
| **35** | 0x23 | \# | NUMBER SIGN | 0x0023 |  |
| **36** | 0x24 | $ | DOLLAR SIGN | 0x0024 |  |
| **37** | 0x25 | % | PERCENT SIGN | 0x0025 |  |
| **38** | 0x26 | & | AMPERSAND | 0x0026 |  |
| **39** | 0x27 | ' | APOSTROPHE | 0x0027 |  |
| **40** | 0x28 | \( | LEFT PARENTHESIS | 0x0028 |  |
| **41** | 0x29 | \) | RIGHT PARENTHESIS | 0x0029 |  |
| **42** | 0x2a | \* | ASTERISK | 0x002a |  |
|  |  |  |  |  |  |
| **128** | 0x80 | Č | LATIN CAPITAL LETTER C WITH CARON | 0x010c |  |
| **129** | 0x81 | ü | LATIN SMALL LETTER U WITH DIAERESIS | 0x00fc |  |
| **130** | 0x82 | é | LATIN SMALL LETTER E WITH ACUTE | 0x00e9 |  |
|  |  |  |  |  |  |

## Odkazy

* [Bratři Kameničtí: výsledné rozhodnutí jsme neučinili my, ale uživatelé](https://www.zive.cz/clanky/bratri-kamenicti-vysledne-rozhodnuti-jsme-neucinili-my-ale-uzivatele/sc-3-a-101337/default.aspx) \(www.zive.cz\)
* [Přehled kódování češtiny](https://www.gitbook.com/book/deefha/klan2016-wiki/edit#) \(www.cestina.cz\)
* [ASCII](https://cs.wikipedia.org/wiki/ASCII) \(cs.wikipedia.org\)
* [Kód Kamenických](https://cs.wikipedia.org/wiki/Kód_Kamenických) \(cs.wikipedia.org\)
* [Unicode](https://cs.wikipedia.org/wiki/Unicode) \(cs.wikipedia.org\)
* [Cstools](http://search.cpan.org/~janpaz/Cstools-3.42/) \(search.cpan.org\)



