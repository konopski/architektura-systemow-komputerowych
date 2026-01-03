# Zestaw 09 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1110 (14)
+ 0101 (5)
------
 10011 (19)
```
- Wynik: **10011** (lub 0011)
- C: **1**
- Dziesiętnie: **19**

## Zadanie 1b) U2 Signed:
```
  1010 (-6)
+ 1100 (-4)
------
 10110
```
- Wynik 4-bit: **0110**
- C: **1**
- V: **1** (OVERFLOW! (-)+(-) = (+))
- Prawidłowy: **10110** = -10
- Dziesiętnie: **-10** (-6-4=-10)
- **Overflow:** Znaki 1+1→0, niemożliwe!

## Zadanie 2:

### 1. Instruction Register (IR):
Rejestr przechowujący **aktualnie wykonywaną instrukcję**.
Rola: Po FETCH instrukcja trafia do IR → DECODE analizuje IR

### 2. Sumator 4-bitowy - schemat:
```
A3B3  A2B2  A1B1  A0B0
 │     │     │     │
[FA]─[FA]─[FA]─[FA]
 │     │     │     │
C4←──C3←──C2←──C1←C0(0)
 │     │     │     │
S3    S2    S1    S0
```
4 Full Addery, Cout→Cin następnego

### 3. Miedź vs aluminium:
**Miedź** ma niższy opór elektryczny.
Aluminium: max ~400 MHz
Miedź: 2-3 GHz możliwe!
Przełom: koniec lat 90

### 4. RISC-V:
Architektura **open-source RISC**.
"V" = piąta (V) wersja uniwersyteckiego projektu.
Wersje I-IV eksperymentalne, V skomercjalizowana.

### 5. Code Memory vs Data Memory:
**Code Memory**: instrukcje programu (`for`, `if`, `ADD`)
**Data Memory**: zmienne (`int i`, `x=10`)
W Harvard: osobne pamięcie!
Przykład ATmega: Flash 32KB (kod), SRAM 2KB (dane)
