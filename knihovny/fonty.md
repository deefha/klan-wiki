# Fonty

```
@Dec   @Hex    Délka Typ

                              HEADER (délka 32 bajtů)
                              -----------------------

0      0x0     8     char     Signatura, vždy "SNOPsoft"
8      0x8     4     byte     ? vždy "00 1A 00 01", podle FileHdrT z FILES.C je to "Verze"
12     0xC     2     word     Typ knihovny, vždy "00 02"
14     0xE     4     dword    Délka souboru
18     0x12    2     word     Čas vytvoření souboru (MS DOS date)
                              Viz http://www.delorie.com/djgpp/doc/rbinter/it/66/16.html
20     0x14    2     word     Datum vytvoření souboru (MS DOS time)
                              Viz http://www.delorie.com/djgpp/doc/rbinter/it/65/16.html
22     0x16    4     dword    ? vždy "00 00 00 00", podle FileHdrT z FILES.C je to "rez1"
26     0x1A    4     dword    ? vždy "00 00 00 00", podle FileHdrT z FILES.C je to "rez2"
30     0x1E    2     word     ? kontrolní součet, podle FileHdrT z FILES.C je to "CRC16"
                              Neodpovídá ani jedna varianta výpočtu CRC16 různých částí souboru

                              FAT (délka 256 bajtů)
                              -------------------

32     0x20    2     word     Počet fontů
34     0x22    18    byte     ?
52     0x34    236   dword    Offsety fontů

                              DATA (délka @14 - 256 - 32 bajtů)
                              ---------------------------------

288    0x120                  Zde začínají fonty, viz dále sekce FONT 1-N

                              FONT 1
                              ------

?      0x?                    1. offset (viz @52), teoreticky vždy @288
+0     +0x0    4     dword    Délka bloku dat (viz @+1800)
+4     +0x4    4     dword    Výška fontu
+8     +0x8    768   byte     Barevná paleta (256 * 3 RGB)
+776   +0x308  1024  dword    Offsety a šířka jednotlivých znaků v bloku dat (pro 256 znaků)
                              Např. "8C 22 00 08" => "8C 22 00" (offset), "08" (šířka)
                              Pokud je offset "00 00 00 00", tak font znak neobsahuje
+1800  +0x708  ?     byte     Blok dat (délka viz @+0), obsahuje indexy barevné palety
                              Indexy se čtou od offsetů jednotlivých znaků stylem:
                              X (šířka znaku, viz @+776) * Y (výška fontu, viz @+4)
                              Přičemž X0,Y0 = levý horní roh matice znaku

                              FONT 2
                              ------

?      0x?                    2. offset (viz @52)
...    ...     ...   ...      ...
...    ...     ...   ...      ...

                              FONT N
                              ------

?      0x?                    N. offset (viz @52)
...    ...     ...   ...      ...
...    ...     ...   ...      ...

?      0x?                    Konec souboru (viz @14)
```



