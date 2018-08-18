Kódování češtiny
================

.. toctree::
   :glob:
   :maxdepth: 3
   :caption: Contents:

   kodovani-cestiny/**

Původní rozhraní KLANu běží v plně grafickém režimu a pro renderování textů z binárních souborů se zde používá vlastní sada rastrových fontů různých velikostí a barvy. Tento proces je zcela nezávislý na prostředí MS-DOS / OS Windows a čistě teoreticky je tedy vlastně jedno v jakém kódování texty jsou, protože se v samotném KLANu zobrazí vždy správně.

Existuje také několik čistě textových souborů (např. readme.txt), které se tak jako tak dají zobrazit pouze samostatně. Právě na nich lze snadno zjistit, že **obsahují celou řadu nečitelných znaků**, u nichž nelze dosáhnout správného zobrazení ani při postupném zkoušení různých středo- a východoevropských znakových sad.

Chceme-li texty z binárních nebo textových souborů "vytáhnout" a dále používat například pro fulltextovou indexaci nebo prostě jen zobrazení mimo KLAN, musíme se kódováním češtiny v textech začít zabývat.

MS-DOS, Československo a 90. léta
---------------------------------

Když selžou všechny možnosti, je potřeba začít přemýšlet, na co se zapomnělo - lépe řečeno na co se **už** zapomnělo.

V textových i binárních souborech KLANu je totiž pro textové řetězce použit **Kód Kamenických** (Bratři Kameničtí, KEYBCS2, nesprávně CP895). Časopis KLAN začal vycházet v roce 1996 a tato znaková sada byla pro kódování češtiny / slovenštiny na počítačích s MS-DOS nejrozšířenější právě v 80.-90. letech 20. století, jde tedy o řešení naprosto odpovídající době vzniku i dostupným technologiím.

S nástupem OS Windows 95 byl ovšem Kód Kamenických postupně vytlačován znakovou sadou Windows-1250, naopak ve světě OS typu UN\*X byla pro češtinu a slovenštinu vždy používána znaková sada ISO 8859-2. Začátek 21. století pak konečně znamenal i začátek nahrazování všech lokálních znakových sad komplexní normou Unicode (kódování UTF-8/16/32).

Díky tomu zmizel Kód Kamenických v propadlišti dějin a práce s texty, které tuto znakovou sadu používají, není dnes po čtvrt století úplně jednoduchá. Řešení ale samozřejmě existuje.

Konverze
--------

Pro převod souborů v textovém módu lze s úspěchem použít utilitu `cstocs` (Kód Kamenických zde má označení `kam`), textové řetězce v binárních souborech je ale nutné zpracovávat "ručně" při samotném parsování. Kromě modulu `Cz::Cstocs` pro jazyk Perl totiž neexistuje oficiální podpora Kódu Kamenických v žádném programovacím jazyce, což je vlastně celkem logické.

Dalším problémem je **několik znaků a symbolů, které v původním Kódu Kamenických nejsou**, ale KLAN je ve svém rozhraní přesto zobrazuje. Běží totiž v plně grafickém režimu a pro renderování textů používá vlastní sadu rastrových fontů, které jsou zcela nezávislé na prostředí MS-DOS / OS Windows. Díky tomu lze na libovolné pozici znakové sady zobrazit jakýkoliv jiný znak nebo symbol, čehož KLAN využívá zejména v poslední čtvrtině znakové tabulky.

Tyto výjimky je opět nutné podchytit ad hoc, níže v tabulkách znaků jsou proto všechny případy uvedeny a okomentovány. Tato "drobnost" už celou situaci komplikuje jen málo a rozhodně jde o menší problém, než kdyby KLAN používal své vlastní kódování.

Tabulka tisknutelných znaků
---------------------------

Odkazy
------

* `Bratři Kameničtí: výsledné rozhodnutí jsme neučinili my, ale uživatelé <https://www.zive.cz/clanky/bratri-kamenicti-vysledne-rozhodnuti-jsme-neucinili-my-ale-uzivatele/sc-3-a-101337/default.aspx>`_ (www.zive.cz)
* `Přehled kódování češtiny <http://www.cestina.cz/kodovani/>`_ (www.cestina.cz)
* `ASCII <https://cs.wikipedia.org/wiki/ASCII>`_ (cs.wikipedia.org)
* `Kód Kamenických <https://cs.wikipedia.org/wiki/Kód_Kamenických>`_ (cs.wikipedia.org)
* `Unicode <https://cs.wikipedia.org/wiki/Unicode>`_ (cs.wikipedia.org)
* `Cstools <http://search.cpan.org/~janpaz/Cstools-3.42/>`_ (search.cpan.org)
