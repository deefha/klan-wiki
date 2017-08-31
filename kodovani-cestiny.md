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
| **32** | 0x20 | _mezera_ | SPACE | U+0020 |  |
| **33** | 0x21 | ! | EXCLAMATION MARK | U+0021 | Některé fonty tento znak nemají |
| **34** | 0x22 | " | QUOTATION MARK | U+0022 | Některé fonty tento znak nemají |
| **35** | 0x23 | \# | NUMBER SIGN | U+0023 | Některé fonty tento znak nemají |
| **36** | 0x24 | $ | DOLLAR SIGN | U+0024 | Některé fonty tento znak nemají |
| **37** | 0x25 | % | PERCENT SIGN | U+0025 | Některé fonty tento znak nemají |
| **38** | 0x26 | & | AMPERSAND | U+0026 | Některé fonty tento znak nemají |
| **39** | 0x27 | ' | APOSTROPHE | U+0027 | Některé fonty tento znak nemají |
| **40** | 0x28 | \( | LEFT PARENTHESIS | U+0028 | Některé fonty tento znak nemají |
| **41** | 0x29 | \) | RIGHT PARENTHESIS | U+0029 | Některé fonty tento znak nemají |
| **42** | 0x2a | \* | ASTERISK | U+002a | Některé fonty tento znak nemají |
| **43** | 0x2b | + | PLUS SIGN | U+002b | Některé fonty tento znak nemají |
| **44** | 0x2c | , | COMMA | U+002c | Některé fonty tento znak nemají |
| **45** | 0x2d | - | HYPHEN-MINUS | U+002d | Některé fonty tento znak nemají |
| **46** | 0x2e | . | FULL STOP | U+002e | Některé fonty tento znak nemají |
| **47** | 0x2f | / | SOLIDUS | U+002f | Některé fonty zde mají znak  \(92\) |
| **48** | 0x30 | 0 | DIGIT ZERO | U+0030 |  |
| **49** | 0x31 | 1 | DIGIT ONE | U+0031 |  |
| **50** | 0x32 | 2 | DIGIT TWO | U+0032 |  |
| **51** | 0x33 | 3 | DIGIT THREE | U+0033 |  |
| **52** | 0x34 | 4 | DIGIT FOUR | U+0034 |  |
| **53** | 0x35 | 5 | DIGIT FIVE | U+0035 |  |
| **54** | 0x36 | 6 | DIGIT SIX | U+0036 |  |
| **55** | 0x37 | 7 | DIGIT SEVEN | U+0037 |  |
| **56** | 0x38 | 8 | DIGIT EIGHT | U+0038 |  |
| **57** | 0x39 | 9 | DIGIT NINE | U+0039 |  |
| **58** | 0x3a | : | COLON | U+003a |  |
| **59** | 0x3b | ; | SEMICOLON | U+003b |  |
| **60** | 0x3c | &lt; | LESS-THAN SIGN | U+003c |  |
| **61** | 0x3d | = | EQUALS SIGN | U+003d |  |
| **62** | 0x3e | &gt; | GREATER-THAN SIGN | U+003e |  |
| **63** | 0x3f | ? | QUESTION MARK | U+003f |  |
| **64** | 0x40 | @ | COMMERCIAL AT | U+0040 |  |
| **65** | 0x41 | A | LATIN CAPITAL LETTER A | U+0041 |  |
| **66** | 0x42 | B | LATIN CAPITAL LETTER B | U+0042 |  |
| **67** | 0x43 | C | LATIN CAPITAL LETTER C | U+0043 |  |
| **68** | 0x44 | D | LATIN CAPITAL LETTER D | U+0044 |  |
| **69** | 0x45 | E | LATIN CAPITAL LETTER E | U+0045 |  |
| **70** | 0x46 | F | LATIN CAPITAL LETTER F | U+0046 |  |
| **71** | 0x47 | G | LATIN CAPITAL LETTER G | U+0047 |  |
| **72** | 0x48 | H | LATIN CAPITAL LETTER H | U+0048 |  |
| **73** | 0x49 | I | LATIN CAPITAL LETTER I | U+0049 |  |
| **74** | 0x4a | J | LATIN CAPITAL LETTER J | U+004a |  |
| **75** | 0x4b | K | LATIN CAPITAL LETTER K | U+004b |  |
| **76** | 0x4c | L | LATIN CAPITAL LETTER L | U+004c |  |
| **77** | 0x4d | M | LATIN CAPITAL LETTER M | U+004d |  |
| **78** | 0x4e | N | LATIN CAPITAL LETTER N | U+004e |  |
| **79** | 0x4f | O | LATIN CAPITAL LETTER O | U+004f |  |
| **80** | 0x50 | P | LATIN CAPITAL LETTER P | U+0050 |  |
| **81** | 0x51 | Q | LATIN CAPITAL LETTER Q | U+0051 |  |
| **82** | 0x52 | R | LATIN CAPITAL LETTER R | U+0052 |  |
| **83** | 0x53 | S | LATIN CAPITAL LETTER S | U+0053 |  |
| **84** | 0x54 | T | LATIN CAPITAL LETTER T | U+0054 |  |
| **85** | 0x55 | U | LATIN CAPITAL LETTER U | U+0055 |  |
| **86** | 0x56 | V | LATIN CAPITAL LETTER V | U+0056 |  |
| **87** | 0x57 | W | LATIN CAPITAL LETTER W | U+0057 |  |
| **88** | 0x58 | X | LATIN CAPITAL LETTER X | U+0058 |  |
| **89** | 0x59 | Y | LATIN CAPITAL LETTER Y | U+0059 |  |
| **90** | 0x5a | Z | LATIN CAPITAL LETTER Z | U+005a |  |
| **91** | 0x5b | \[ |  | U+005b |  |
| **92** | 0x5c | \ |  | U+005c |  |
| **93** | 0x5d | \] |  | U+005d |  |
| **94** | 0x5e | ^ |  | U+005e |  |
| **95** | 0x5f | \_ |  | U+005f |  |
| **96** | 0x60 | \` |  | U+0060 |  |
| **97** | 0x61 | a |  | U+0061 |  |
| **98** | 0x62 | b |  | U+0062 |  |
| **99** | 0x63 | c |  | U+0063 |  |
| **100** | 0x64 | d |  | U+0064 |  |
| **101** | 0x65 | e |  | U+0065 |  |
| **102** | 0x66 | f |  | U+0066 |  |
| **103** | 0x67 | g |  | U+0067 |  |
| **104** | 0x68 | h |  | U+0068 |  |
| **105** | 0x69 | i |  | U+0069 |  |
| **106** | 0x6a | j |  | U+006a |  |
| **107** | 0x6b | k |  | U+006b |  |
| **108** | 0x6c | l |  | U+006c |  |
| **109** | 0x6d | m |  | U+006d |  |
| **110** | 0x6e | n |  | U+006e |  |
| **111** | 0x6f | o |  | U+006f |  |
| **112** | 0x70 | p |  | U+0070 |  |
| **113** | 0x71 | q |  | U+0071 |  |
| **114** | 0x72 | r |  | U+0072 |  |
| **115** | 0x73 | s |  | U+0073 |  |
| **116** | 0x74 | t |  | U+0074 |  |
| **117** | 0x75 | u |  | U+0075 |  |
| **118** | 0x76 | v |  | U+0076 |  |
| **119** | 0x77 | w |  | U+0077 |  |
| **120** | 0x78 | x |  | U+0078 |  |
| **121** | 0x79 | y |  | U+0079 |  |
| **122** | 0x7a | z |  | U+007a |  |
| **123** | 0x7b | { |  | U+007b |  |
| **124** | 0x7c | \| |  | U+007c |  |
| **125** | 0x7d | } |  | U+007d |  |
| **126** | 0x7e | ~ |  | U+007e |  |

Znaky 128-??? bla bla bla...

| Dec | Hex | Znak | Unicode | UTF-8 | Poznámka |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **128** | 0x80 | Č | LATIN CAPITAL LETTER C WITH CARON | U+010c |  |
| **129** | 0x81 | ü | LATIN SMALL LETTER U WITH DIAERESIS | U+00fc |  |
| **130** | 0x82 | é | LATIN SMALL LETTER E WITH ACUTE | U+00e9 |  |
|  |  |  |  |  |  |

## Odkazy

* [Bratři Kameničtí: výsledné rozhodnutí jsme neučinili my, ale uživatelé](https://www.zive.cz/clanky/bratri-kamenicti-vysledne-rozhodnuti-jsme-neucinili-my-ale-uzivatele/sc-3-a-101337/default.aspx) \(www.zive.cz\)
* [Přehled kódování češtiny](https://www.gitbook.com/book/deefha/klan2016-wiki/edit#) \(www.cestina.cz\)
* [ASCII](https://cs.wikipedia.org/wiki/ASCII) \(cs.wikipedia.org\)
* [Kód Kamenických](https://cs.wikipedia.org/wiki/Kód_Kamenických) \(cs.wikipedia.org\)
* [Unicode](https://cs.wikipedia.org/wiki/Unicode) \(cs.wikipedia.org\)
* [Cstools](http://search.cpan.org/~janpaz/Cstools-3.42/) \(search.cpan.org\)



