# Zestaw 04 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1110 (14)
+ 1010 (10)
------
 11000 (24)
```
- Wynik: **11000** (lub 1000)
- C: **1**
- Dziesiętnie: **24**

## Zadanie 1b) U2 Signed:
```
  1001 (-7)
+ 1011 (-5)
------
 10100
```
- Wynik: **10100** (lub 0100)
- C: **1**
- V: **0** ((-)+(-) = (-) sign bit 1→1→0, ale to OK, wynik dodatni przez overflow... CZEKAJ)

**Poprawna analiza:**
1001=-7, 1011=-5
Wynik 4-bit: 0100
- A znak: 1 (-)
- B znak: 1 (-)
- Wynik znak: 0 (+)
- **V=1** bo (-)+(-) dało (+) - OVERFLOW!
- Prawidłowy wynik: **10100** = -12
- Dziesiętnie: **-12**

## Zadanie 2:

### 1. Multiplexer (MUX):
Przełącznik cyfrowy wybierający jedno z N wejść na podstawie sygnału Select.
MUX 4:1: 4 wejścia (I0-I3), 2 select (S1,S0), 1 wyjście Y

### 2. CALL vs RET:
- **CALL addr**: Push PC na stos, PC=addr (wywołanie funkcji)
- **RET**: Pop PC ze stosu (powrót z funkcji)

### 3. Systemy liczbowe - 0xFA:
- **Binarnie**: F=1111, A=1010 → **11111010**
- **Dziesiętnie**: 15×16 + 10 = 240 + 10 = **250**
- **Ósemkowo**: 11 111 010 → 3 7 2 = **372₈**

### 4. BCD (Binary Coded Decimal):
Każda cyfra dziesiętna kodowana osobno w 4 bitach.
Przykład: 194 → 0001 1001 0100
Zastosowanie: wyświetlacze 7-segmentowe, kalkulatory

### 5. Half Adder vs Full Adder:
- **HA**: 2 wejścia (A, B) → S, C
- **FA**: 3 wejścia (A, B, Cin) → S, Cout
- FA = 2×HA + OR (do budowy sumatorów n-bitowych)
