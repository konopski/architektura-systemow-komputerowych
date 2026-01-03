# Ściąga 01: Arytmetyka Binarna i Flagi Procesora

---

## 1. DODAWANIE BINARNE - METODA SŁUPKOWA

### Zasady podstawowe:
```
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 0 (przeniesienie 1)
```

### Przykład:
```
    1101    (13)
  + 0110    (6)
  ------
   10011    (19)
    ↑
    Carry = 1
```

---

## 2. ARYTMETYKA ZAWSZE DODATNIA (UNSIGNED)

### Co obliczamy:
- ✅ Wynik binarny
- ✅ Flagę **C** (Carry) - czy było przeniesienie z najstarszego bitu
- ✅ Wynik dziesiętny

### Przykład:
```
  1110  (14)
+ 1010  (10)
------
 11000  (24)
 ↑
 C = 1 ← Było przeniesienie!

Wynik: 24 (dziesiętnie)
```

### Kiedy C = 1?
- Gdy przeniesienie "wychodzi" poza najstarszy bit
- Wynik nie mieści się w n-bitach

---

## 3. UZUPEŁNIENIE DO DWÓCH (U2, SIGNED)

### Interpretacja bitów (4-bitowe):
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

**Zasada:** Jeśli najstarszy bit = 1, liczba jest ujemna

### Co obliczamy:
- ✅ Wynik binarny
- ✅ Flagę **C** (Carry)
- ✅ Flagę **V** (Overflow)
- ✅ Prawidłowy wynik (z uwzględnieniem V i C)
- ✅ Wynik dziesiętny

---

## 4. FLAGA OVERFLOW (V) - NAJWAŻNIEJSZE!

### Kiedy V = 1?
**Overflow występuje, gdy wynik ma BŁĘDNY ZNAK:**

1. **(+) + (+) = (-)** ← Niemożliwe! V=1
2. **(-) + (-) = (+)** ← Niemożliwe! V=1

### Kiedy V = 0?
3. **(+) + (+) = (+)** ← OK, V=0
4. **(-) + (-) = (-)** ← OK, V=0
5. **(+) + (-) = cokolwiek** ← Zawsze OK, V=0
6. **(-) + (+) = cokolwiek** ← Zawsze OK, V=0

### Test na Overflow:
```
Sprawdź ZNAKI:
- Bit znaku A (najstarszy bit)
- Bit znaku B (najstarszy bit)
- Bit znaku Wyniku (najstarszy bit)

Jeśli: A=B (oba dodatnie lub oba ujemne)
   I: Wynik ma inny znak niż A i B
TO: V = 1
```

---

## 5. PRZYKŁADY KROK PO KROKU

### Przykład 1: Overflow = 1
```
  0111  (+7)
+ 0110  (+6)
------
  1101

Analiza:
- A = 0111 → znak + (bit=0)
- B = 0110 → znak + (bit=0)
- Wynik = 1101 → znak - (bit=1) ← BŁĄD!

(+) + (+) = (-) → NIEMOŻLIWE!
V = 1 ✓

C = 0 (brak przeniesienia)

Prawidłowy wynik:
  0111 + 0110 = 13 (dec)
  Ale to się nie mieści w 4 bitach ze znakiem!
  Wynik 1101 to -3 (BŁĄD!)
```

### Przykład 2: Overflow = 0, Carry = 1
```
  1011  (-5)
+ 1110  (-2)
------
 11001
 ↑
 C=1

Wynik 4-bitowy: 1001

Analiza:
- A = 1011 → znak - (bit=1)
- B = 1110 → znak - (bit=1)
- Wynik = 1001 → znak - (bit=1) ← OK!

(-) + (-) = (-) → Prawidłowy znak!
V = 0 ✓

C = 1 (było przeniesienie, ale to normalne w U2)

Interpretacja:
1001 (U2) = -7 (dec) ✓
-5 + (-2) = -7 ← Prawidłowo!

Prawidłowy wynik: 1001 = -7
```

### Przykład 3: Carry=1, trzeba dopisać
```
  0110  (+6)
+ 1011  (-5)
------
 10001
 ↑
 C=1

Wynik 4-bitowy: 0001

Analiza:
- A = 0110 → znak + (bit=0)
- B = 1011 → znak - (bit=1)
- Wynik = 0001 → znak + (bit=0)

(+) + (-) = (+) → Może być!
V = 0 ✓

C = 1

Prawidłowy wynik BEZ przeniesienia (bo V=0):
0001 = +1 (dec) ✓
6 + (-5) = 1 ← Prawidłowo!
```

---

## 6. ALGORYTM ROZWIĄZYWANIA ZADAŃ U2

### Krok 1: Dodaj binarnie (normalnie, jak unsigned)
```
  AAAA
+ BBBB
------
 CXXXX
```

### Krok 2: Oblicz Carry
```
C = przeniesienie z najstarszego bitu (0 lub 1)
```

### Krok 3: Test na Overflow
```
Sprawdź ZNAKI (najstarsze bity):
- Jeśli A[3]=B[3]=0 (oba +) i Wynik[3]=1 (-) → V=1
- Jeśli A[3]=B[3]=1 (oba -) i Wynik[3]=0 (+) → V=1
- W pozostałych przypadkach → V=0
```

### Krok 4: Prawidłowy wynik
```
Jeśli V=1:
  → Przepełnienie! Wynik 4-bitowy jest błędny
  → Prawidłowy wynik to 5 bitów (z C)

Jeśli V=0:
  → Wynik 4-bitowy jest prawidłowy
  → Ignoruj C (lub nie, zależy od kontekstu)
```

### Krok 5: Interpretacja dziesiętna
```
Jeśli najstarszy bit = 1 (liczba ujemna):
  1. Zaneguj wszystkie bity
  2. Dodaj 1
  3. Wynik to wartość bezwzględna (dodaj minus)

Przykład: 1011 (U2) = ?
  1. NOT 1011 = 0100
  2. 0100 + 1 = 0101 = 5
  3. Wynik: -5
```

---

## 7. ZAMIANA NA WARTOŚĆ PRZECIWNĄ (U2)

### Algorytm negacji:
```
1. Zaneguj wszystkie bity (NOT)
2. Dodaj 1

Przykład: +5 → -5
  0101  (5)
  ↓ NOT
  1010
  ↓ +1
  1011  (-5) ✓
```

---

## 8. WSZYSTKIE FLAGI PROCESORA

| Flaga | Nazwa | Kiedy = 1? |
|-------|-------|------------|
| **C** | Carry | Przeniesienie z najstarszego bitu |
| **Z** | Zero | Wynik = 0 |
| **N** | Negative | Bit znaku = 1 (wynik ujemny) |
| **V** | Overflow | Przepełnienie (błędny znak w U2) |
| **S** | Sign | N XOR V (prawdziwy znak) |
| **H** | Half-carry | Przeniesienie z bitu 3→4 |

### Flaga S (Sign):
```
S = N XOR V

Dlaczego?
- Jeśli V=1, to wynik ma błędny znak
- S koryguje znak: jeśli N=1 i V=1, to S=0 (wynik dodatni!)

Przykład:
  0111 + 0110 = 1101
  N=1 (bit znaku=1), V=1 (overflow)
  S = 1 XOR 1 = 0 ← Wynik DODATNI (mimo że bit=1)
```

---

## 9. SZYBKA ŚCIĄGA - WZORY

### Przeniesienie (Carry):
```
C = 1, jeśli wynik > max(n-bitów)
```

### Overflow w U2:
```
V = (A[MSB] == B[MSB]) AND (Wynik[MSB] != A[MSB])

Czyli:
V = 1 ⟺ (A+B mają ten sam znak) AND (Wynik ma inny znak)
```

### Interpretacja U2 → dziesiętna:
```
Jeśli bit znaku = 0: wartość jak unsigned
Jeśli bit znaku = 1: -(2^n - wartość)

Przykład (4-bit):
  1011 = -(16 - 11) = -5
  1111 = -(16 - 15) = -1
```

---

## 10. TYPOWE PUŁAPKI

❌ **Błąd 1:** Myślenie, że C=1 to zawsze błąd
→ W U2 Carry często występuje i to normalne!

❌ **Błąd 2:** Ignorowanie Overflow
→ V=1 oznacza, że wynik jest BŁĘDNY!

❌ **Błąd 3:** Nieprawidłowa interpretacja U2
→ 1111 to NIE 15, tylko -1!

❌ **Błąd 4:** Zapominanie o komentarzu
→ Wykładowca oczekuje komentarza: "Overflow bo (+)+(+)=(-)"

---

**KLUCZOWE DO ZAPAMIĘTANIA:**
1. V=1 gdy znak się nie zgadza: **(+)+(+)=(-)** lub **(-)+(-)=(+)**
2. Test: porównaj znaki A, B i Wyniku
3. Zawsze napisz komentarz o Overflow!
4. U2: bit=1 → liczba ujemna
