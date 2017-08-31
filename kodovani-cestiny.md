# Kódování češtiny

Původní rozhraní KLANu běží v plně grafickém režimu a pro renderování textů z binárních souborů se zde používá vlastní sada rastrových fontů různých velikostí a barvy. Tento proces je zcela nezávislý na prostředí MS-DOS / OS Windows a čistě teoreticky je tedy vlastně jedno v jakém kódování texty jsou, protože se v samotném KLANu zobrazí vždy správně.

Existuje také několik čistě textových souborů \(např. [readme.txt](/soubory/readme.txt.md)\), které se tak jako tak dají zobrazit pouze samostatně. Právě na nich lze snadno zjistit, že **obsahují celou řadu nečitelných znaků**, u nichž nelze dosáhnout správného zobrazení ani při postupném zkoušení různých středo- a východoevropských znakových sad.

Chceme-li texty z binárních nebo textových souborů "vytáhnout" a dále používat například pro fulltextovou indexaci nebo prostě jen zobrazení mimo KLAN, musíme se kódováním češtiny v textech začít zabývat.

## MS-DOS, Československo a 90. léta

Když selžou všechny možnosti, je potřeba začít přemýšlet, na co se zapomnělo - lépe řečeno na co se už zapomnělo.

V textových i binárních souborech KLANu je totiž pro textové řetězce použit **Kód Kamenických** \(Bratři Kameničtí, KEYBCS2, nesprávně CP895\). Časopis KLAN začal vycházet v roce 1996 a tato znaková sada byla pro kódování češtiny / slovenštiny na počítačích s MS-DOS nejrozšířenější právě v 80.-90. letech 20. století, jde tedy o řešení naprosto odpovídající době vzniku i dostupným technologiím.

S nástupem OS Windows 95 byl ovšem Kód Kamenických postupně vytlačován znakovou sadou Windows-1250, naopak ve světě OS typu UN\*X byla pro češtinu a slovenštinu vždy používána znaková sada ISO 8859-2. Začátek 21. století pak konečně znamenal i začátek nahrazování všech lokálních znakových sad komplexní normou Unicode \(kódování UTF-8/16/32\).

Díky tomu zmizel Kód Kamenických v propadlišti dějin a práce s texty, které tuto znakovou sadu používají, není dnes po čtvrt století úplně jednoduchá. Řešení ale samozřejmě existuje.

## Konverze

Pro převod souborů v textovém módu lze s úspěchem použít utilitu `cstocs` \(Kód Kamenických zde má označení `kam`\), textové řetězce v binárních souborech je ale nutné zpracovávat "ručně" při samotném parsování. Kromě modulu `Cz::Cstocs` pro jazyk Perl totiž neexistuje oficiální podpora Kódu Kamenických v žádném programovacím jazyce, což je vlastně celkem logické.

Dalším problémem je **několik znaků a symbolů, které v původním Kódu Kamenických nejsou**, ale KLAN je ve svém rozhraní přesto zobrazuje. Běží totiž v plně grafickém režimu a pro renderování textů používá vlastní sadu rastrových fontů, které jsou zcela nezávislé na prostředí MS-DOS / OS Windows. Díky tomu lze na libovolné pozici znakové sady zobrazit jakýkoliv jiný znak nebo symbol, čehož KLAN využívá zejména v poslední čtvrtině znakové tabulky.

Tyto výjimky je opět nutné podchytit ad hoc, níže v tabulkách znaků jsou proto všechny případy uvedeny a okomentovány. Tato "drobnost" už celou situaci komplikuje jen málo a rozhodně jde o menší problém, než kdyby KLAN používal své vlastní kódování.

## Tabulka tisknutelných znaků

Znaky 0-127 odpovídají standardní ASCII tabulce. Znaky 0-31 a znak 127 nejsou tisknutelné, žádný font je neobsahuje.

| Dec | Hex | Znak | Unicode | UTF-8 | Poznámka |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **32** | 0x20 | _mezera_ | SPACE | 0x0020 |  |
| **33** | 0x21 | ! | EXCLAMATION MARK | 0x0021 | Některé fonty tento znak nemají |
| **34** | 0x22 | " | QUOTATION MARK | 0x0022 | Některé fonty tento znak nemají |
| **35** | 0x23 | \# | NUMBER SIGN | 0x0023 | Některé fonty tento znak nemají |
| **36** | 0x24 | $ | DOLLAR SIGN | 0x0024 | Některé fonty tento znak nemají |
| **37** | 0x25 | % | PERCENT SIGN | 0x0025 | Některé fonty tento znak nemají |
| **38** | 0x26 | & | AMPERSAND | 0x0026 | Některé fonty tento znak nemají |
| **39** | 0x27 | ' | APOSTROPHE | 0x0027 | Některé fonty tento znak nemají |
| **40** | 0x28 | \( | LEFT PARENTHESIS | 0x0028 | Některé fonty tento znak nemají |
| **41** | 0x29 | \) | RIGHT PARENTHESIS | 0x0029 | Některé fonty tento znak nemají |
| **42** | 0x2a | \* | ASTERISK | 0x002a | Některé fonty tento znak nemají |
| **43** | 0x2b | + | PLUS SIGN | 0x002b | Některé fonty tento znak nemají |
| **44** | 0x2c | , | COMMA | 0x002c | Některé fonty tento znak nemají |
| **45** | 0x2d | - | HYPHEN-MINUS | 0x002d | Některé fonty tento znak nemají |
| **46** | 0x2e | . | FULL STOP | 0x002e | Některé fonty tento znak nemají |
| **47** | 0x2f | / | SOLIDUS | 0x002f | Některé fonty zde mají znak  \(92\) |
| **48** | 0x30 | 0 | DIGIT ZERO | 0x0030 |  |
| **49** | 0x31 | 1 |  | 0x0031 |  |
| **50** | 0x32 | 2 |  | 0x0032 |  |
| **51** | 0x33 | 3 |  | 0x0033 |  |
| **52** | 0x34 | 4 |  | 0x0034 |  |
| **53** | 0x35 | 5 |  | 0x0035 |  |
| **54** | 0x36 | 6 |  | 0x0036 |  |
| **55** | 0x37 | 7 |  | 0x0037 |  |
| **56** | 0x38 | 8 |  | 0x0038 |  |
| **57** | 0x39 | 9 |  | 0x0039 |  |
| **58** | 0x3a | : |  | 0x003a |  |
| **59** | 0x3b | ; |  | 0x003b |  |
| **60** | 0x3c | &lt; |  | 0x003c |  |
| **61** | 0x3d | = |  | 0x003d |  |
| **62** | 0x3e | &gt; |  | 0x003e |  |
| **63** | 0x3f | ? |  | 0x003f |  |
| **64** | 0x40 | @ |  | 0x0040 |  |
| **65** | 0x41 | A |  | 0x0041 |  |
| **66** | 0x42 | B |  | 0x0042 |  |
| **67** | 0x43 | C |  | 0x0043 |  |
| **68** | 0x44 | D |  | 0x0044 |  |
| **69** | 0x45 | E |  | 0x0045 |  |
| **70** | 0x46 | F |  | 0x0046 |  |
| **71** | 0x47 | G |  | 0x0047 |  |
| **72** | 0x48 | H |  | 0x0048 |  |
| **73** | 0x49 | I |  | 0x0049 |  |
| **74** | 0x4a | J |  | 0x004a |  |
| **75** | 0x4b | K |  | 0x004b |  |
| **76** | 0x4c | L |  | 0x004c |  |
| **77** | 0x4d | M |  | 0x004d |  |
| **78** | 0x4e | N |  | 0x004e |  |
| **79** | 0x4f | O |  | 0x004f |  |
| **80** | 0x50 | P |  | 0x0050 |  |
| **81** | 0x51 | Q |  | 0x0051 |  |
| **82** | 0x52 | R |  | 0x0052 |  |
| **83** | 0x53 | S |  | 0x0053 |  |
| **84** | 0x54 | T |  | 0x0054 |  |
| **85** | 0x55 | U |  | 0x0055 |  |
| **86** | 0x56 | V |  | 0x0056 |  |
| **87** | 0x57 | W |  | 0x0057 |  |
| **88** | 0x58 | X |  | 0x0058 |  |
| **89** | 0x59 | Y |  | 0x0059 |  |
| **90** | 0x5a | Z |  | 0x005a |  |
| **91** | 0x5b | \[ |  | 0x005b |  |
| **92** | 0x5c | \ |  | 0x005c |  |
| **93** | 0x5d | \] |  | 0x005d |  |
| **94** | 0x5e | ^ |  | 0x005e |  |
| **95** | 0x5f | \_ |  | 0x005f |  |
| **96** | 0x60 | \` |  | 0x0060 |  |
| **97** | 0x61 | a |  | 0x0061 |  |
| **98** | 0x62 | b |  | 0x0062 |  |
| **99** | 0x63 | c |  | 0x0063 |  |
| **100** | 0x64 | d |  | 0x0064 |  |
| **101** | 0x65 | e |  | 0x0065 |  |
| **102** | 0x66 | f |  | 0x0066 |  |
| **103** | 0x67 | g |  | 0x0067 |  |
| **104** | 0x68 | h |  | 0x0068 |  |
| **105** | 0x69 | i |  | 0x0069 |  |
| **106** | 0x6a | j |  | 0x006a |  |
| **107** | 0x6b | k |  | 0x006b |  |
| **108** | 0x6c | l |  | 0x006c |  |
| **109** | 0x6d | m |  | 0x006d |  |
| **110** | 0x6e | n |  | 0x006e |  |
| **111** | 0x6f | o |  | 0x006f |  |
| **112** | 0x70 | p |  | 0x0070 |  |
| **113** | 0x71 | q |  | 0x0071 |  |
| **114** | 0x72 | r |  | 0x0072 |  |
| **115** | 0x73 | s |  | 0x0073 |  |
| **116** | 0x74 | t |  | 0x0074 |  |
| **117** | 0x75 | u |  | 0x0075 |  |
| **118** | 0x76 | v |  | 0x0076 |  |
| **119** | 0x77 | w |  | 0x0077 |  |
| **120** | 0x78 | x |  | 0x0078 |  |
| **121** | 0x79 | y |  | 0x0079 |  |
| **122** | 0x7a | z |  | 0x007a |  |
| **123** | 0x7b | { |  | 0x007b |  |
| **124** | 0x7c | \| |  | 0x007c |  |
| **125** | 0x7d | } |  | 0x007d |  |
| **126** | 0x7e | ~ |  | 0x007e |  |

Znaky 128-??? bla bla bla...

| Dec | Hex | Znak | Unicode | UTF-8 | Poznámka |
| :--- | :--- | :--- | :--- | :--- | :--- |
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



