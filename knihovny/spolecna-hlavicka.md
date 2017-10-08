# Společná hlavička

Všechny knihovna začínají hlavičkou v délce 32 bajtů. Její struktura je pro všechny společná:

```
@Dec   @Hex    Délka Typ

                              HEADER (délka 32 bajtů)
                              -----------------------

0      0x0     8     char     Signatura, vždy "SNOPSoft"
8      0x8     4     byte     ? vždy "00 1A 00 01"
                              Podle FileHdrT z FILES.C je to "Verze"
12     0xC     2     word     Typ knihovny, vždy "00 02"
14     0xE     4     dword    Délka souboru v bajtech
18     0x12    2     word     Čas vytvoření souboru (MS DOS date)
                              Viz http://www.delorie.com/djgpp/doc/rbinter/it/66/16.html
20     0x14    2     word     Datum vytvoření souboru (MS DOS time)
                              Viz http://www.delorie.com/djgpp/doc/rbinter/it/65/16.html
22     0x16    4     dword    ? vždy "00 00 00 00"
                              Podle FileHdrT z FILES.C je to "rez1"
26     0x1A    4     dword    ? vždy "00 00 00 00"
                              Podle FileHdrT z FILES.C je to "rez2"
30     0x1E    2     word     ? kontrolní součet
                              Podle FileHdrT z FILES.C je to "CRC16"
                              Neodpovídá ani jedna varianta výpočtu CRC16 různých částí souboru
```



