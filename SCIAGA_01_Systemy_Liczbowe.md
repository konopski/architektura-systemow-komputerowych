# Ściąga 06: Systemy Liczbowe i Kodowanie

---

## 1. SYSTEMY POZYCYJNE

### Definicja:
**System pozycyjny** = każda cyfra ma wagę zależną od pozycji

### Ogólny wzór:
```
Liczba = c_n × p^n + c_(n-1) × p^(n-1) + ... + c_1 × p^1 + c_0 × p^0

gdzie:
p = podstawa systemu
c = cyfra na pozycji
```

### Przykład (dziesiętny, p=10):
```
1234 = 1×10³ + 2×10² + 3×10¹ + 4×10⁰
     = 1000 + 200 + 30 + 4
     = 1234
```

---

## 2. SYSTEM BINARNY (p=2)

### Cyfry: 0, 1

### Zamiana binarny → dziesiętny:
```
1011₂ = 1×2³ + 0×2² + 1×2¹ + 1×2⁰
      = 8 + 0 + 2 + 1
      = 11₁₀
```

### Zamiana dziesiętny → binarny (dzielenie przez 2):
```
13₁₀ → binarny:
13 ÷ 2 = 6 reszta 1  ←┐
 6 ÷ 2 = 3 reszta 0   │
 3 ÷ 2 = 1 reszta 1   │ Czytaj od dołu
 1 ÷ 2 = 0 reszta 1  ←┘

Wynik: 1101₂
```

---

## 3. UZUPEŁNIENIE DO DWÓCH (U2, TWO'S COMPLEMENT)

### Definicja:
**U2** = sposób reprezentacji liczb ze znakiem w systemach binarnych

### Zakres dla n bitów:
```
n-bit U2: od -(2^(n-1)) do +(2^(n-1) - 1)

4-bit: od -8 do +7
8-bit: od -128 do +127
16-bit: od -32768 do +32767
```

### Interpretacja (4-bit):
```
0000 =  0     1000 = -8
0001 =  1     1001 = -7
0010 =  2     1010 = -6
0011 =  3     1011 = -5
0100 =  4     1100 = -4
0101 =  5     1101 = -3
0110 =  6     1110 = -2
0111 =  7     1111 = -1
```

**Zasada:** Bit znaku (MSB) = 1 → liczba ujemna

---

## 3a. KONWERSJA U2 → DZIESIĘTNY

### Metoda 1: Wzór matematyczny
```
Jeśli MSB = 0: jak unsigned
Jeśli MSB = 1: -(2^n - wartość)

Przykład 4-bit:
1011₂ w U2:
MSB = 1 (ujemna)
= -(2^4 - 11) = -(16 - 11) = -5 ✓
```

### Metoda 2: NOT + 1
```
1011₂ → ujemna (MSB=1)
1. NOT: 0100
2. +1:  0101 = 5
3. Wynik: -5 ✓
```

---

## 3b. KONWERSJA DZIESIĘTNY → U2

### Liczba dodatnia (0..7 dla 4-bit):
```
+5 → normalny binarny: 0101
```

### Liczba ujemna:
```
-5 → U2:
1. Weź wartość bezwzględną: 5 = 0101
2. NOT: 1010
3. +1:  1011  ← to jest -5 w U2 ✓
```

---

## 3c. DODAWANIE W U2

### Prosty przykład:
```
  0011 (+3)
+ 0101 (+5)
------
  1000

MSB = 1 → ujemna!
Ale to overflow! (+)+(+) nie może dać (-)
V = 1 (flaga overflow)
```

### Prawidłowy przykład:
```
  1011 (-5)
+ 0101 (+5)
------
 10000
 ↑
 C=1

4-bit wynik: 0000 = 0 ✓
V = 0 (znaki różne, OK)
-5 + 5 = 0 ✓
```

### Klucz: Sprawdzaj flagę V!
```
V = 1 → overflow (błędny znak)
V = 0 → wynik prawidłowy
```

---

## 4. SYSTEM SZESNASTKOWY (HEXADECIMAL, p=16)

### Cyfry: 0-9, A-F

```
0=0, 1=1, 2=2, 3=3, 4=4, 5=5, 6=6, 7=7,
8=8, 9=9, A=10, B=11, C=12, D=13, E=14, F=15
```

### Zamiana hex → dziesiętny:
```
2A3₁₆ = 2×16² + 10×16¹ + 3×16⁰
      = 512 + 160 + 3
      = 675₁₀
```

### Zamiana binarny ↔ hex (grupowanie po 4 bity):
```
1101 1010₂ → hex:
  D    A
= DA₁₆

0xFA₁₆ → binarny:
F=1111, A=1010
= 11111010₂
```

---

## 5. SYSTEM ÓSEMKOWY (OCTAL, p=8)

### Cyfry: 0-7

### Zamiana octal → dziesiętny:
```
157₈ = 1×8² + 5×8¹ + 7×8⁰
     = 64 + 40 + 7
     = 111₁₀
```

### Zamiana binarny ↔ octal (grupowanie po 3 bity):
```
110 101 111₂ → octal:
 6   5   7
= 657₈

0o123₈ → binarny:
1=001, 2=010, 3=011
= 001010011₂
```

**Uwaga:** Rzadko używany w informatyce (hex bardziej popularny).

---

## 6. BCD (Binary Coded Decimal)

### Definicja:
**BCD** = każda cyfra dziesiętna kodowana osobno w 4 bitach

### Przykład:
```
Dziesiętnie: 1 9 4
BCD:      0001 1001 0100
             ↑    ↑    ↑
             1    9    4
```

### Porównanie z binarnym:
```
194₁₀ w binarnym: 11000010₂ (8 bitów)
194₁₀ w BCD:      0001 1001 0100 (12 bitów)
```

### Zastosowania:
✅ Wyświetlacze siedmiosegmentowe
✅ Kalkulatory
✅ Tam, gdzie ważna jest czytelność dziesiętna

❌ Nieefektywne (zajmuje więcej bitów)

---

## 7. NOTACJE W PROGRAMOWANIU

### Prefiksy systemów liczbowych:

| System | C/C++ | Python | Assembler | Przykład |
|--------|-------|--------|-----------|----------|
| Binarny | `0b` | `0b` | `0b` lub `%` | `0b1101` |
| Ósemkowy | `0` | `0o` | - | `0123` |
| Dziesiętny | brak | brak | brak | `123` |
| Hex | `0x` | `0x` | `0x` lub `$` | `0xFA` |

### Przykłady w C:
```c
int a = 0b1010;   // binarny: 10
int b = 012;      // ósemkowy: 10
int c = 10;       // dziesiętny: 10
int d = 0xA;      // hex: 10
```

---

## 8. SZYBKIE ZAMIANY

### Binarny → Hex (grupuj po 4):
```
1111 0101 1010₂
  F    5    A
= 0xF5A
```

### Hex → Binarny (rozwiń każdą cyfrę):
```
0x3C
3 = 0011
C = 1100
= 00111100₂
```

### Binarny → Octal (grupuj po 3):
```
101 110 011₂
 5   6   3
= 563₈
```

### Trick: Mnożenie/dzielenie przez 2^n:
```
× 2 = przesunięcie w lewo (<<)
÷ 2 = przesunięcie w prawo (>>)

1010₂ << 1 = 10100₂ (×2)
1010₂ >> 1 = 101₂   (÷2)
```

---

## 9. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Zamień 0xAB na binarny.
**A:** A=1010, B=1011 → 10101011₂

### Q: Zamień 11010111₂ na hex.
**A:** 1101 0111 → D7 → 0xD7

### Q: Co to jest BCD?
**A:** Binary Coded Decimal - każda cyfra dziesiętna kodowana osobno w 4 bitach.

### Q: Ile wynosi 0xFF w dziesiętnym?
**A:** 15×16¹ + 15×16⁰ = 240 + 15 = 255

### Q: Jak szybko pomnożyć liczbę binarną przez 8?
**A:** Przesunięcie w lewo o 3 pozycje (×2³ = ×8).

### Q: Co to jest U2 (uzupełnienie do dwóch)?
**A:** Sposób reprezentacji liczb ze znakiem: bit MSB=1 → ujemna.

### Q: Zamień -6 na U2 (4-bit).
**A:** 6 = 0110 → NOT = 1001 → +1 = 1010 (to jest -6)

### Q: Ile wynosi 1101 w U2 (4-bit)?
**A:** MSB=1 (ujemna) → -(16-13) = -3

---

## 10. SZYBKA ŚCIĄGA - TABELA

```
┌────────────┬───────┬──────────┬──────────────┐
│   SYSTEM   │ CYFRY │ PODSTAWA │   PRZYKŁAD   │
├────────────┼───────┼──────────┼──────────────┤
│  Binarny   │  0-1  │    2     │  1010₂       │
│    U2      │  0-1  │    2*    │ 1011 = -5    │
│  Ósemkowy  │  0-7  │    8     │  123₈        │
│ Dziesiętny │  0-9  │   10     │  456₁₀       │
│    Hex     │ 0-F   │   16     │  0xABC       │
│    BCD     │  0-9  │   10**   │ 0001 0101    │
└────────────┴───────┴──────────┴──────────────┘
* U2: liczby ze znakiem, MSB=bit znaku
** każda cyfra osobno w 4 bitach

Zamiany szybkie:
Bin ↔ Hex: grupuj po 4 bity
Bin ↔ Oct: grupuj po 3 bity
```

**ZAPAMIĘTAJ:**
- **U2:** MSB=1 → ujemna, negacja = NOT + 1
- **U2 zakres (n-bit):** -(2^(n-1)) do +(2^(n-1) - 1)
- Hex: A=10, B=11, C=12, D=13, E=14, F=15
- 1 cyfra hex = 4 bity
- 1 cyfra oct = 3 bity
- BCD: każda cyfra dziesiętna = 4 bity
- Przesunięcie << = ×2, >> = ÷2
- **V=1** w U2 → overflow (błędny znak!)

