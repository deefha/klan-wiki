# font.lib

```
@Dec        @Hex    Délka    Typ

                                        Header
                                        ------

0           0x0     8        char       "SNOPsoft"
8           0x8     4        byte       ? vždy "00 1A 00 01"
12          0xc     2        word       Typ knihovny
14          0xe     4        dword      Délka souboru
18          0x12    2        word       Čas vytvoření souboru (MS DOS date)
                                        Viz http://www.delorie.com/djgpp/doc/rbinter/it/66/16.html
20          0x14    2        word       Datum vytvoření souboru (MS DOS time)
                                        Viz http://www.delorie.com/djgpp/doc/rbinter/it/65/16.html
22          0x16    10       byte       ?
32          0x20    2        word       Počet fontů
34          0x22    18       byte       ?
52          0x34    236      dword      Offsety fontů
288         0x120                       Zde by měly začínat fonty

                                        Font
                                        ----

?           0x?                         1. offset (viz @52), teoreticky @288
+0          +0x0    4        dword      Délka bloku dat (viz @+1800)
+4          +0x4    4        dword      Výška řádku
+8          +0x8    768      byte       Barevná paleta (256*3 RGB)
+776        +0x308  1024     dword      Offsety a šířka znaků v bloku dat (256 znaků)
                                        Např. "8C 22 00 08" => "8C 22 00" (offset), "08" (šířka)
+1800       +0x708  ?        byte       Blok dat (délka viz @+0), obsahuje indexy barevné palety

                                        Font
                                        ----

?           0x?                         2. offset (viz @52)
...         ...     ...      ...        ...
...         ...     ...      ...        ...

                                        Font
                                        ----

?           0x?                         N. offset (viz @52)
...         ...     ...      ...        ...
...         ...     ...      ...        ...

?           0x?                         Konec souboru (viz @14)
```



