# Knihovny

* mají příponu .lib
* prvních 32 bajtů vždy zabírá [hlavička](/knihovny/hlavicka.md), na 12. bajtu \(0xC\) jsou 2 bajty obsahující ID knihovny
* od 32. bajtu \(0x20\) následuje [FAT oblast](/knihovny/fat.md) proměnlivé délky
* pak následují samotná data knihovny
* | ID knihovny | Typ knihovny | Délka FAT oblasti | Poznámka |
  | :--- | :--- | :--- | :--- |
  | **0x0001** | [Kurzory](/knihovny/kurzory.md) |  |  |
  | **0x0002** | [Fonty](/knihovny/fonty.md) |  |  |
  | **0x0003** | [Obrázky](/knihovny/obrazky.md) |  |  |
  | **0x0004** | [Zvuky](/knihovny/zvuky.md) |  |  |
  | **0x0005** | [Hudba](/knihovny/hudba.md) |  | Vydání \#00 - \#01 |
  | **0x0006** | [Videa](/knihovny/videa.md) |  |  |
  | **0x0007** | [Texty](/knihovny/texty.md), [Hudba](/knihovny/hudba.md) |  | Hudba ve vydání \#02 - \#42 |
  | **0x000A** | [Nápověda](/knihovny/napoveda.md) |  |  |
  | **0x001E** | [Popisky](/knihovny/popisky.md), [Spořič](/knihovny/sporic.md) |  |  |
  | **0x001F** | [Index](/knihovny/index.md) |  |  |
  |  | [arKLANoid](/knihovny/arklanoid.md) |  | Technicky nejde o knihovnu |



