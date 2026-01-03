# Zestaw 03 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1010 (10)
+ 1001 (9)
------
 10011 (19)
```
- Wynik: **10011** (lub 0011)
- C: **1**
- Dziesiętnie: **19**

## Zadanie 1b) U2 Signed:
```
  0111 (+7)
+ 0110 (+6)
------
  1101
```
- Wynik: **1101**
- C: **0**
- V: **1** (OVERFLOW!)
- Prawidłowy: **10011** (potrzeba 5 bitów)
- Dziesiętnie: **13**
- **Komentarz:** TAK, overflow! **(+)+(+)=(-)** - niemożliwe! Bit znaku: 0+0→1 błąd

## Zadanie 2:

### 1. Program Counter (PC):
Rejestr wskazujący adres **następnej instrukcji** do wykonania.
- FETCH: pobiera instrukcję z Code Memory[PC]
- Automatyczna inkrementacja: PC++
- Skoki (JMP/CALL) zmieniają PC

### 2. Instrukcje INC vs ADD:
- **INC Rd**: Rd = Rd + 1, NIE aktualizuje flagi **C**
- **ADD Rd, Rr**: Rd = Rd + Rr, aktualizuje wszystkie flagi (C, Z, V, N, H, S)
- INC szybsze, ale bez Carry!

### 3. Sumator 4-bitowy:
Schemat: 4× Full Adder połączone kaskadowo
```
[FA3] ← [FA2] ← [FA1] ← [FA0]
 Cout←─ Cout←─ Cout←─ Cout
```
Każdy FA: A + B + Cin → Sum, Cout

### 4. Liczby zmiennoprzecinkowe (Floating Point):
- **Mantisa** - liczba znormalizowana
- **Wykładnik** - potęga 2
- Format: (-1)^S × M × 2^E
- Operacje ~3× wolniejsze niż integer

### 5. Motorola 68k:
Przegrała z Intelem w latach 90 (rynek PC).
Atari/Amiga/Commodore z 68k upadły.
ARM przejął rynek embedded.
