# Zestaw 07 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1010 (10)
+ 0111 (7)
------
 10001 (17)
```
- Wynik: **10001** (lub 0001)
- C: **1**
- Dziesiętnie: **17**

## Zadanie 1b) U2 Signed:
```
  1101 (-3)
+ 1111 (-1)
------
 11100
```
- Wynik 4-bit: **1100**
- C: **1**
- V: **0** ((-)+(-) = (-), znaki OK: 1+1→1)
- Prawidłowy: **1100**
- Dziesiętnie: **-4** (-3-1=-4) ✓

## Zadanie 2:

### 1. Flagi procesora - 4 różne:
- **C (Carry)**: Przeniesienie z najstarszego bitu
- **Z (Zero)**: Wynik = 0
- **V (Overflow)**: Przepełnienie (błędny znak w U2)
- **N (Negative)**: Bit znaku (1=ujemny)

### 2. Alignment:
**Adres podzielny przez rozmiar danych**.
- 32-bit: adres ÷ 4 = int (0x00, 0x04, 0x08...)
- Not aligned: błąd/wolniejszy dostęp
- Motorola 68k: wyjątek! Intel: 2 cykle zamiast 1

### 3. Harvard - dlaczego szybsza:
**Osobne magistrale** dla kodu i danych.
FETCH + EXECUTE równolegle (brak konfliktu).
von Neumann: jedna magistrala → bottleneck

### 4. Cache memory:
Szybka pamięć między CPU a RAM.
L1 (najmniejszy, najszybszy) → L2 → L3 → RAM
Przechowuje często używane dane (locality)

### 5. Dzielenie binarne:
Algorytm **sekwencyjny** (bit po bicie, jak "długie" dzielenie).
Wolniejsze niż mnożenie.
Optymalizacja: przesunięcia dla ÷2^n
