# Zestaw 06 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1100 (12)
+ 1011 (11)
------
 10111 (23)
```
- Wynik: **10111** (lub 0111)
- C: **1**
- Dziesiętnie: **23**

## Zadanie 1b) U2 Signed:
```
  0101 (+5)
+ 1010 (-6)
------
  1111
```
- Wynik: **1111**
- C: **0**
- V: **0** ((+)+(-) znaki różne, może być)
- Prawidłowy: **1111**
- Dziesiętnie: **-1** (5-6=-1) ✓

## Zadanie 2:

### 1. Bramka NAND:
```
A B | Y
----+---
0 0 | 1
0 1 | 1
1 0 | 1
1 1 | 0
```
Y = NOT(A AND B)
**Uniwersalna** - można zbudować wszystkie bramki

### 2. Instrukcje sterowania AVR:
- **RJMP**: Relative Jump (skok względny ±2K)
- **CALL**: Call Subroutine (wywołanie funkcji + push PC)
- **RET**: Return (powrót z funkcji + pop PC)

### 3. Super skalarny procesor:
**Wykonuje wiele instrukcji równocześnie** (więcej niż 1 na cykl).
Przykład: Intel 386 SX
Mechanizm: pipelining + multiple execution units

### 4. Floating Point - dodawanie:
1. **Wyrównaj wykładniki** (większy wykładnik)
2. **Dodaj mantisy**
3. **Znormalizuj wynik** (przesunięcie, korekta wykładnika)

### 5. ARM vs Intel x86:
ARM: RISC, małe chipy, energooszczędne, smartfony
Intel: CISC, duże chipy (50× większe), PC/serwery
ARM wygrywa w mobile, Intel w desktop
