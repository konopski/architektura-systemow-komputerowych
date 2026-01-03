# Zestaw 05 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1011 (11)
+ 1101 (13)
------
 11000 (24)
```
- Wynik: **11000** (lub 1000)
- C: **1**
- Dziesiętnie: **24**

## Zadanie 1b) U2 Signed:
```
  1110 (-2)
+ 0011 (+3)
------
 10001
```
- Wynik 4-bit: **0001**
- C: **1**
- V: **0** ((-) + (+) = (+) znaki różne, może być OK)
- Prawidłowy: **0001**
- Dziesiętnie: **+1** (-2+3=1) ✓

## Zadanie 2:

### 1. BREQ vs BRNE:
- **BREQ label**: Branch if Equal - skacze gdy Z=1 (wynik=0, równe)
- **BRNE label**: Branch if Not Equal - skacze gdy Z=0 (nierówne)
- Używane po CP/CPI do porównań

### 2. Mnożenie MUL vs MULS:
- **MUL**: unsigned × unsigned → R1:R0 (16-bit)
- **MULS**: signed × signed → R1:R0 (U2)
- MULS uwzględnia znaki (rozszerzenie znaku)

### 3. Adresowanie byte-oriented:
**1 adres = 1 bajt**
- int16 (2 bajty) zajmuje 2 adresy
- int32 (4 bajty) zajmuje 4 adresy
- Adres 0x100 → bajt 0, 0x101 → bajt 1, ...

### 4. XOR w parzystości:
XOR wszystkich bitów daje parzystość.
Parzystość parzysta: XOR=0
Zastosowanie: Ethernet (detekcja błędów)

### 5. ARM - energooszczędność:
- Architektura **RISC** (proste instrukcje)
- Mniejszy chip → mniej tranzystorów → mniej energii
- Smartfony, tablety preferują ARM nad Intel
