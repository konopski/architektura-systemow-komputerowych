# Zestaw 08 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1001 (9)
+ 1011 (11)
------
 10100 (20)
```
- Wynik: **10100** (lub 0100)
- C: **1**
- Dziesiętnie: **20**

## Zadanie 1b) U2 Signed:
```
  0011 (+3)
+ 0111 (+7)
------
  1010
```
- Wynik: **1010**
- C: **0**
- V: **1** (OVERFLOW! (+)+(+) = (-))
- Prawidłowy: **01010** (potrzeba 5 bitów)
- Dziesiętnie: **10**
- **Overflow:** Bit znaku 0+0→1, niemożliwe!

## Zadanie 2:

### 1. XOR - tabelka prawdy:
```
A B | Y
----+---
0 0 | 0
0 1 | 1
1 0 | 1
1 1 | 0
```
Y=1 gdy wejścia **różne**

### 2. BREQ i BRNE:
- **BREQ**: Branch if Equal, sprawdza Z=1
- **BRNE**: Branch if Not Equal, sprawdza Z=0
- Używane po CP/CPI

### 3. Super skalarny:
Wykonuje **więcej niż 1 instrukcję na cykl**.
Przykład: Intel 80386 SX
Mechanizm: multiple execution units + pipelining

### 4. Floating Point - dodawanie (3 kroki):
1. **Wyrównaj wykładniki** (ten sam E)
2. **Dodaj mantisy**
3. **Znormalizuj wynik**

### 5. ARM - energooszczędność:
**RISC** (proste instrukcje)
Mniejszy chip → mniej tranzystorów
Niższe napięcie, mniej ciepła
Intel: CISC, 50× większy
