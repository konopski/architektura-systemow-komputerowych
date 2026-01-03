# Ściąga 08: Technika Cyfrowa (Bramki i Układy)

---

## 1. BRAMKI LOGICZNE - PODSTAWOWE

### AND (Iloczyn logiczny):
```
Symbol: &, ∧, •
A B | Y
----+---
0 0 | 0
0 1 | 0
1 0 | 0
1 1 | 1
```
Y = 1 tylko gdy **obie** wejścia = 1

### OR (Suma logiczna):
```
Symbol: |, ∨, +
A B | Y
----+---
0 0 | 0
0 1 | 1
1 0 | 1
1 1 | 1
```
Y = 1 gdy **przynajmniej jedno** wejście = 1

### NOT (Negacja):
```
Symbol: ¬, ~, !
A | Y
--+---
0 | 1
1 | 0
```
Y = odwrotność A

### XOR (Exclusive OR):
```
Symbol: ⊕, ^
A B | Y
----+---
0 0 | 0
0 1 | 1
1 0 | 1
1 1 | 0
```
Y = 1 gdy wejścia **różne**

---

## 2. BRAMKI ZŁOŻONE

### NAND (NOT AND):
```
A B | Y
----+---
0 0 | 1
0 1 | 1
1 0 | 1
1 1 | 0
```
Y = NOT(A AND B)
**Bramka uniwersalna** - można zbudować wszystkie inne!

### NOR (NOT OR):
```
A B | Y
----+---
0 0 | 1
0 1 | 0
1 0 | 0
1 1 | 0
```
Y = NOT(A OR B)
**Również uniwersalna**

---

## 3. HALF ADDER (Półsumator)

### Zadanie:
Dodaje 2 bity (A + B)

### Schemat:
```
A ───┐
     ├─ XOR ─→ S (Sum)
B ───┘

A ───┐
     ├─ AND ─→ C (Carry)
B ───┘
```

### Tabelka prawdy:
```
A B | S C
----+----
0 0 | 0 0
0 1 | 1 0
1 0 | 1 0
1 1 | 0 1
```

**Wzory:**
- S = A XOR B
- C = A AND B

---

## 4. FULL ADDER (Pełny sumator)

### Zadanie:
Dodaje 3 bity (A + B + Cin)

### Schemat:
```
    ┌──────────┐
A ──┤          │
B ──┤   Full   ├─→ S (Sum)
Cin─┤  Adder   ├─→ Cout (Carry Out)
    └──────────┘
```

### Tabelka prawdy:
```
A B Cin | S Cout
--------+-------
0 0  0  | 0  0
0 0  1  | 1  0
0 1  0  | 1  0
0 1  1  | 0  1
1 0  0  | 1  0
1 0  1  | 0  1
1 1  0  | 0  1
1 1  1  | 1  1
```

**Wzory:**
- S = A XOR B XOR Cin
- Cout = (A AND B) OR (Cin AND (A XOR B))

---

## 5. SUMATOR 4-BITOWY

### Schemat:
```
A3 B3  A2 B2  A1 B1  A0 B0
 │  │   │  │   │  │   │  │
 └──┼───┘  │   │  │   │  │
    │      │   │  │   │  │
   [FA]   [FA] [FA] [FA]
    │      │   │  │   │  │
   C4←────C3←─C2←─C1←─C0(=0)
    │      │   │  │   │
    S3     S2  S1  S0
```

### Działanie:
1. FA0: A0 + B0 + 0 → S0, C1
2. FA1: A1 + B1 + C1 → S1, C2
3. FA2: A2 + B2 + C2 → S2, C3
4. FA3: A3 + B3 + C3 → S3, C4

**C4 = Carry Out** (flaga C w procesorze!)

---

## 6. MULTIPLEXER (MUX)

### Definicja:
**Multiplexer** = przełącznik cyfrowy, wybiera jedno z wielu wejść

### MUX 2:1 (2 wejścia, 1 wyjście):
```
I0 ──┐
     ├─→ Y
I1 ──┘
     │
     S (Select)

Y = (NOT S) AND I0  OR  S AND I1
```

### Tabelka:
```
S | Y
--+---
0 | I0
1 | I1
```

### MUX 4:1:
```
4 wejścia (I0-I3)
2 sygnały wyboru (S1, S0)
```

---

## 7. REJESTRY (FLIP-FLOPY)

### D Flip-Flop (najprostszy):
```
    ┌────────┐
D ──┤   D    │
    │  FF    ├─→ Q
CLK─┤        ├─→ NOT Q
    └────────┘
```

### Działanie:
- Na **narastającym zboczu CLK**: Q = D
- Poza zboczem: Q **pamiętane**

### Zastosowania:
✅ **Rejestry procesora** (R0-R31)
✅ **Pamięć** (SRAM)
✅ **Synchronizacja**
✅ **Podróżowanie w czasie** (opóźnienie sygnału)

---

## 8. PARZYSTOŚĆ (PARITY)

### Definicja:
**Bit parzystości** = kontrola liczby jedynek

### Parzystość parzysta (Even):
```
XOR wszystkich bitów = 0
```

### Przykład:
```
Dane: 1 0 1 1 0 1 0
XOR:  1⊕0⊕1⊕1⊕0⊕1⊕0 = 0 (parzysta)

Dane: 1 0 1 1 0 1 1
XOR:  1⊕0⊕1⊕1⊕0⊕1⊕1 = 1 (nieparzysta)
```

### Zastosowanie:
✅ **Ethernet** - detekcja błędów
✅ **Pamięć ECC** - korekcja błędów
✅ **Transmisja szeregowa**

---

## 9. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Narysuj tabelkę prawdy XOR.
**A:** (Zobacz sekcja 1)

### Q: Czym różni się Half Adder od Full Adder?
**A:** HA dodaje 2 bity, FA dodaje 3 bity (w tym Cin).

### Q: Co to jest bramka uniwersalna?
**A:** NAND lub NOR - można z niej zbudować wszystkie inne bramki.

### Q: Jak działa sumator 4-bitowy?
**A:** 4 Full Addery połączone kaskadowo, Cout jednego → Cin następnego.

### Q: Co to jest multiplexer?
**A:** Przełącznik cyfrowy wybierający jedno z wielu wejść.

---

## 10. SZYBKA ŚCIĄGA - TABELA

```
┌───────────┬─────────────────────────────────┐
│  BRAMKA   │         WYNIK Y=1 GDY...        │
├───────────┼─────────────────────────────────┤
│    AND    │  Wszystkie wejścia = 1          │
│    OR     │  Przynajmniej jedno = 1         │
│    XOR    │  Wejścia różne                  │
│   NAND    │  Nie wszystkie = 1              │
│    NOR    │  Wszystkie = 0                  │
└───────────┴─────────────────────────────────┘

┌─────────────┬─────────────────────────────┐
│    UKŁAD    │       ZASTOSOWANIE          │
├─────────────┼─────────────────────────────┤
│ Half Adder  │  Dodawanie 2 bitów          │
│ Full Adder  │  Dodawanie 3 bitów          │
│ Multiplexer │  Wybór jednego z N wejść    │
│ D Flip-Flop │  Pamięć 1 bitu              │
│ Parzystość  │  Detekcja błędów (XOR)      │
└─────────────┴─────────────────────────────┘
```

**ZAPAMIĘTAJ:**
- XOR = różne wejścia
- NAND/NOR = uniwersalne
- FA = HA + HA + OR
- Rejestr = D Flip-Flop

