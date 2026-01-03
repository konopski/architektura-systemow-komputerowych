# Zestaw 10 - ROZWIĄZANIA

## Zadanie 1a) Unsigned:
```
  1101 (13)
+ 1011 (11)
------
 11000 (24)
```
- Wynik: **11000** (lub 1000)
- C: **1**
- Dziesiętnie: **24**

## Zadanie 1b) U2 Signed:
```
  0100 (+4)
+ 1101 (-3)
------
 10001
```
- Wynik 4-bit: **0001**
- C: **1**
- V: **0** ((+)+(-) znaki różne, OK)
- Prawidłowy: **0001**
- Dziesiętnie: **+1** (4-3=1) ✓

## Zadanie 2:

### 1. Wielordzeniowość - limit:
**Problem: magistrala pamięci (bottleneck)**
Powyżej 20-32 rdzeni: wszystkie konkurują o RAM.
Ograniczona przepustowość, cache coherency.
Kolejne rdzenie czekają na pamięć → brak przyspieszenia.

### 2. RJMP vs CALL vs RET:
- **RJMP label**: Relative Jump, skok względny ±2K, 1 cykl
- **CALL addr**: Push PC, PC=addr, wywołanie funkcji
- **RET**: Pop PC, powrót z funkcji

### 3. GPU vs CPU:
**GPU:**
- Tysiące prostych rdzeni (1000+)
- Proste operacje równolegle
- Mała cache, niska moc per rdzeń

**CPU:**
- Kilka mocnych rdzeni (4-32)
- Złożone zadania
- Duża cache

GPU szybkie w grafice/AI przez masywną równoległość.

### 4. Maszyna Turinga - 3 elementy:
1. **Taśma** (nieskończona pamięć, komórki)
2. **Głowica** (czyta/pisze, przesuwa się)
3. **Stan** (aktualne "myślenie" maszyny)
(+ Tabela przejść - instrukcje)

### 5. Flaga S (Sign):
**S = N XOR V**
Koryguje znak przy overflow.
- Jeśli V=1 (overflow), znak N jest błędny
- S daje **prawdziwy znak**
Przykład: N=1, V=1 → S=0 (wynik dodatni mimo N=1)
