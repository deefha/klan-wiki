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

### Znaky 0-127

Znaky 0-127 odpovídají standardní ASCII tabulce, ale ne každý font obsahuje všechny znaky. Znaky 0-31 a znak 127 nejsou tisknutelné, neobsahuje je tedy žádný font.

| Dec | Hex | Znak | Unicode | UTF-8 | Poznámka |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **32** | 0x20 | _mezera_ | SPACE | U+0020 |  |
| **33** | 0x21 | ! | EXCLAMATION MARK | U+0021 | Některé fonty tento znak neobsahují |
| **34** | 0x22 | " | QUOTATION MARK | U+0022 | Některé fonty tento znak neobsahují |
| **35** | 0x23 | \# | NUMBER SIGN | U+0023 | Některé fonty tento znak neobsahují |
| **36** | 0x24 | $ | DOLLAR SIGN | U+0024 | Některé fonty tento znak neobsahují |
| **37** | 0x25 | % | PERCENT SIGN | U+0025 | Některé fonty tento znak neobsahují |
| **38** | 0x26 | & | AMPERSAND | U+0026 | Některé fonty tento znak neobsahují |
| **39** | 0x27 | ' | APOSTROPHE | U+0027 | Některé fonty tento znak neobsahují |
| **40** | 0x28 | \( | LEFT PARENTHESIS | U+0028 | Některé fonty tento znak neobsahují |
| **41** | 0x29 | \) | RIGHT PARENTHESIS | U+0029 | Některé fonty tento znak neobsahují |
| **42** | 0x2a | \* | ASTERISK | U+002a | Některé fonty tento znak neobsahují |
| **43** | 0x2b | + | PLUS SIGN | U+002b | Některé fonty tento znak neobsahují |
| **44** | 0x2c | , | COMMA | U+002c | Některé fonty tento znak neobsahují |
| **45** | 0x2d | - | HYPHEN-MINUS | U+002d | Některé fonty tento znak neobsahují |
| **46** | 0x2e | . | FULL STOP | U+002e | Některé fonty tento znak neobsahují |
| **47** | 0x2f | / | SOLIDUS | U+002f | Některé fonty zde mají znak "\" \(92\) |
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
| **59** | 0x3b | ; | SEMICOLON | U+003b | Některé fonty tento znak neobsahují |
| **60** | 0x3c | &lt; | LESS-THAN SIGN | U+003c | Některé fonty tento znak neobsahují |
| **61** | 0x3d | = | EQUALS SIGN | U+003d | Některé fonty tento znak neobsahují |
| **62** | 0x3e | &gt; | GREATER-THAN SIGN | U+003e | Některé fonty tento znak neobsahují |
| **63** | 0x3f | ? | QUESTION MARK | U+003f | Některé fonty tento znak neobsahují |
| **64** | 0x40 | @ | COMMERCIAL AT | U+0040 | Některé fonty tento znak neobsahují |
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
| **91** | 0x5b | \[ | LEFT SQUARE BRACKET | U+005b | Některé fonty tento znak neobsahují |
| **92** | 0x5c | \ | REVERSE SOLIDUS | U+005c | Některé fonty tento znak neobsahují |
| **93** | 0x5d | \] | RIGHT SQUARE BRACKET | U+005d | Některé fonty tento znak neobsahují |
| **94** | 0x5e | ^ | CIRCUMFLEX ACCENT | U+005e | Některé fonty tento znak neobsahují |
| **95** | 0x5f | \_ | LOW LINE | U+005f | Některé fonty tento znak neobsahují |
| **96** | 0x60 | \` | GRAVE ACCENT | U+0060 | Některé fonty tento znak neobsahují |
| **97** | 0x61 | a | LATIN SMALL LETTER A | U+0061 | Některé fonty zde mají znak "A" \(65\) |
| **98** | 0x62 | b | LATIN SMALL LETTER B | U+0062 | Některé fonty zde mají znak "B" \(66\) |
| **99** | 0x63 | c | LATIN SMALL LETTER C | U+0063 | Některé fonty zde mají znak "C" \(67\) |
| **100** | 0x64 | d | LATIN SMALL LETTER D | U+0064 | Některé fonty zde mají znak "D" \(68\) |
| **101** | 0x65 | e | LATIN SMALL LETTER E | U+0065 | Některé fonty zde mají znak "E" \(69\) |
| **102** | 0x66 | f | LATIN SMALL LETTER F | U+0066 | Některé fonty zde mají znak "F" \(70\) |
| **103** | 0x67 | g | LATIN SMALL LETTER G | U+0067 | Některé fonty zde mají znak "G" \(71\) |
| **104** | 0x68 | h | LATIN SMALL LETTER H | U+0068 | Některé fonty zde mají znak "H" \(72\) |
| **105** | 0x69 | i | LATIN SMALL LETTER I | U+0069 | Některé fonty zde mají znak "I" \(73\) |
| **106** | 0x6a | j | LATIN SMALL LETTER J | U+006a | Některé fonty zde mají znak "J" \(74\) |
| **107** | 0x6b | k | LATIN SMALL LETTER K | U+006b | Některé fonty zde mají znak "K" \(75\) |
| **108** | 0x6c | l | LATIN SMALL LETTER L | U+006c | Některé fonty zde mají znak "L" \(76\) |
| **109** | 0x6d | m | LATIN SMALL LETTER M | U+006d | Některé fonty zde mají znak "M" \(77\) |
| **110** | 0x6e | n | LATIN SMALL LETTER N | U+006e | Některé fonty zde mají znak "N" \(78\) |
| **111** | 0x6f | o | LATIN SMALL LETTER O | U+006f | Některé fonty zde mají znak "O" \(79\) |
| **112** | 0x70 | p | LATIN SMALL LETTER P | U+0070 | Některé fonty zde mají znak "P" \(80\) |
| **113** | 0x71 | q | LATIN SMALL LETTER Q | U+0071 | Některé fonty zde mají znak "Q" \(81\) |
| **114** | 0x72 | r | LATIN SMALL LETTER R | U+0072 | Některé fonty zde mají znak "R" \(82\) |
| **115** | 0x73 | s | LATIN SMALL LETTER S | U+0073 | Některé fonty zde mají znak "S" \(83\) |
| **116** | 0x74 | t | LATIN SMALL LETTER T | U+0074 | Některé fonty zde mají znak "T" \(84\) |
| **117** | 0x75 | u | LATIN SMALL LETTER U | U+0075 | Některé fonty zde mají znak "U" \(85\) |
| **118** | 0x76 | v | LATIN SMALL LETTER V | U+0076 | Některé fonty zde mají znak "V" \(86\) |
| **119** | 0x77 | w | LATIN SMALL LETTER W | U+0077 | Některé fonty zde mají znak "W" \(87\) |
| **120** | 0x78 | x | LATIN SMALL LETTER X | U+0078 | Některé fonty zde mají znak "X" \(88\) |
| **121** | 0x79 | y | LATIN SMALL LETTER Y | U+0079 | Některé fonty zde mají znak "Y" \(89\) |
| **122** | 0x7a | z | LATIN SMALL LETTER Z | U+007a | Některé fonty zde mají znak "Z" \(90\) |
| **123** | 0x7b | { | LEFT CURLY BRACKET | U+007b | Některé fonty tento znak neobsahují |
| **124** | 0x7c | \| | VERTICAL LINE | U+007c | Některé fonty tento znak neobsahují |
| **125** | 0x7d | } | RIGHT CURLY BRACKET | U+007d | Některé fonty tento znak neobsahují |
| **126** | 0x7e | ~ | TILDE | U+007e | Některé fonty tento znak neobsahují |

### Znaky 128-175

Znaky 128-175 odpovídají tabulce Kódu Kamenických, ale ne každý font obsahuje všechny znaky. Některé znaky neobsahuje žádný font, v tabulce jsou ale pro úplnost přesto uvedeny.

| Dec | Hex | Znak | Unicode | UTF-8 | Poznámka |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **128** | 0x80 | Č | LATIN CAPITAL LETTER C WITH CARON | U+010c |  |
| **129** | 0x81 | ü | LATIN SMALL LETTER U WITH DIAERESIS | U+00fc | Některé fonty tento znak neobsahují |
| **130** | 0x82 | é | LATIN SMALL LETTER E WITH ACUTE | U+00e9 | Některé fonty zde mají znak "É" \(144\) |
| **131** | 0x83 | ď | LATIN SMALL LETTER D WITH CARON | U+010f | Některé fonty tento znak neobsahují |
| **132** | 0x84 | ä | LATIN SMALL LETTER A WITH DIAERESIS | U+00e4 | Některé fonty tento znak neobsahují |
| **133** | 0x85 | Ď | LATIN CAPITAL LETTER D WITH CARON | U+010e |  |
| **134** | 0x86 | Ť | LATIN CAPITAL LETTER T WITH CARON | U+0164 |  |
| **135** | 0x87 | č | LATIN SMALL LETTER C WITH CARON | U+010d | Některé fonty zde mají znak "Č" \(128\) |
| **136** | 0x88 | ě | LATIN SMALL LETTER E WITH CARON | U+011b | Některé fonty zde mají znak "Ě" \(138\) |
| **137** | 0x89 | Ě | LATIN CAPITAL LETTER E WITH CARON | U+011a |  |
| **138** | 0x8a | Ĺ | LATIN CAPITAL LETTER L WITH ACUTE | U+0139 | Žádný font tento znak neobsahuje |
| **139** | 0x8b | Í | LATIN CAPITAL LETTER I WITH ACUTE | U+00cd |  |
| **140** | 0x8c | ľ | LATIN SMALL LETTER L WITH CARON | U+013e | Žádný font tento znak neobsahuje |
| **141** | 0x8d | ĺ | LATIN SMALL LETTER L WITH ACUTE | U+013a | Žádný font tento znak neobsahuje |
| **142** | 0x8e | Ä | LATIN CAPITAL LETTER A WITH DIAERESIS | U+00c4 | Některé fonty tento znak neobsahují |
| **143** | 0x8f | Á | LATIN CAPITAL LETTER A WITH ACUTE | U+00c1 |  |
| **144** | 0x90 | É | LATIN CAPITAL LETTER E WITH ACUTE | U+00c9 |  |
| **145** | 0x91 | ž | LATIN SMALL LETTER Z WITH CARON | U+017e | Některé fonty zde mají znak "Ž" \(146\) |
| **146** | 0x92 | Ž | LATIN CAPITAL LETTER Z WITH CARON | U+017d |  |
| **147** | 0x93 | ô | LATIN SMALL LETTER O WITH CIRCUMFLEX | U+00f4 | Některé fonty tento znak neobsahují |
| **148** | 0x94 | ö | LATIN SMALL LETTER O WITH DIAERESIS | U+00f6 | Některé fonty tento znak neobsahují |
| **149** | 0x95 | Ó | LATIN CAPITAL LETTER O WITH ACUTE | U+00d3 |  |
| **150** | 0x96 | ů | LATIN SMALL LETTER U WITH RING ABOVE | U+016f | Některé fonty zde mají znak "Ů" \(\) |
| **151** | 0x97 |  |  |  |  |
| **152** | 0x98 |  |  |  |  |
| **153** | 0x99 |  |  |  |  |
| **154** | 0x9a |  |  |  |  |
| **155** | 0x9b |  |  |  |  |
| **156** | 0x9c |  |  |  |  |
| **157** | 0x9d |  |  |  |  |
| **158** | 0x9e |  |  |  |  |
| **159** | 0x9f |  |  |  |  |
| **160** | 0xa0 |  |  |  |  |
| **161** | 0xa1 |  |  |  |  |
| **162** | 0xa2 |  |  |  |  |
| **163** | 0xa3 |  |  |  |  |
| **164** | 0xa4 |  |  |  |  |
| **165** | 0xa5 |  |  |  |  |
| **166** | 0xa6 |  |  |  |  |
| **167** | 0xa7 |  |  |  |  |
| **168** | 0xa8 |  |  |  |  |
| **169** | 0xa9 |  |  |  |  |
| **170** | 0xaa |  |  |  |  |
| **171** | 0xab |  |  |  |  |
| **172** | 0xac |  |  |  |  |
| **173** | 0xad |  |  |  |  |
| **174** | 0xae |  |  |  |  |
| **175** | 0xaf |  |  |  |  |

### Znaky 176-255

Znaky 176-255 buďto nejsou vůbec použity, nebo neodpovídají tabulce Kódu Kamenických. Ne každý font obsahuje všechny znaky.

| Dec | Hex | Znak | Unicode | UTF-8 | Poznámka |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **203** | 0xcb |  |  |  |  |

## Odkazy

* [Bratři Kameničtí: výsledné rozhodnutí jsme neučinili my, ale uživatelé](https://www.zive.cz/clanky/bratri-kamenicti-vysledne-rozhodnuti-jsme-neucinili-my-ale-uzivatele/sc-3-a-101337/default.aspx) \(www.zive.cz\)
* [Přehled kódování češtiny](https://www.gitbook.com/book/deefha/klan2016-wiki/edit#) \(www.cestina.cz\)
* [ASCII](https://cs.wikipedia.org/wiki/ASCII) \(cs.wikipedia.org\)
* [Kód Kamenických](https://cs.wikipedia.org/wiki/Kód_Kamenických) \(cs.wikipedia.org\)
* [Unicode](https://cs.wikipedia.org/wiki/Unicode) \(cs.wikipedia.org\)
* [Cstools](http://search.cpan.org/~janpaz/Cstools-3.42/) \(search.cpan.org\)



