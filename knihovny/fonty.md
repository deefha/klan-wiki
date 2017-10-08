# Fonty

* [společná hlavička](/knihovny/spolecna-hlavicka.md)

```
@Dec   @Hex    Délka Typ

                              HEADER (délka 32 bajtů)
                              -----------------------

0      0x0     32             Společná hlavička

                              FAT (délka 256 bajtů)
                              -------------------

32     0x20    4     dword    Počet fontů
36     0x24    252   dword    Offsety fontů (63)

                              DATA (délka @14 - 32 - 256 bajtů)
                              ---------------------------------

288    0x120                  Zde začínají fonty, viz dále sekce FONT 1-N

                              FONT 1
                              ------

?      0x?                    1. offset (viz @36), teoreticky vždy @288
+0     +0x0    4     dword    Délka bloku dat (viz @+1800)
+4     +0x4    4     dword    Výška fontu
+8     +0x8    768   byte     Barevná paleta (256 * 3 RGB)
+776   +0x308  1024  dword    Offsety a šířka jednotlivých znaků v bloku dat (pro 256 znaků)
                              Např. "8C 22 00 08" => "8C 22 00" (offset), "08" (šířka)
                              První offset je 0, jde o pozici v bloku dat (viz @+1800), ne v souboru
                              Pokud je šířka 0, tak font znak neobsahuje
+1800  +0x708  ?     byte     Blok dat (délka viz @+0), obsahuje indexy barevné palety
                              Indexy se čtou od offsetů jednotlivých znaků stylem:
                              X (šířka znaku, viz @+776) * Y (výška fontu, viz @+4)
                              Přičemž X0,Y0 = levý horní roh matice znaku

                              FONT 2
                              ------

?      0x?                    2. offset (viz @36)
...    ...     ...   ...      ...
...    ...     ...   ...      ...

                              FONT N
                              ------

?      0x?                    N. offset (viz @36)
...    ...     ...   ...      ...
...    ...     ...   ...      ...

?      0x?                    Konec souboru (viz @14)
```



