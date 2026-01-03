# Ściąga 11: Arytmetyka Modulo

---

## 1. PODSTAWY MODULO

### Definicja:
**a mod n** = reszta z dzielenia a przez n

### Przykłady:
```
7 mod 3 = 1     (7 ÷ 3 = 2 reszta 1)
15 mod 4 = 3    (15 ÷ 4 = 3 reszta 3)
20 mod 5 = 0    (20 ÷ 5 = 4 reszta 0)
```

### Zakres wyniku:
```
Dla a mod n, wynik zawsze: 0 ≤ wynik < n

mod 3 → {0, 1, 2}
mod 8 → {0, 1, 2, 3, 4, 5, 6, 7}
mod 256 → {0, 1, 2, ..., 255}
```

---

## 2. ARYTMETYKA MODULO - PODSTAWOWE OPERACJE

### Dodawanie modulo:
```
(a + b) mod n = ((a mod n) + (b mod n)) mod n

Przykład: (17 + 23) mod 10
= 40 mod 10
= 0

Weryfikacja: (17 mod 10) + (23 mod 10) = 7 + 3 = 10 mod 10 = 0 ✓
```

### Odejmowanie modulo:
```
(a - b) mod n = ((a mod n) - (b mod n)) mod n

Przykład: (15 - 7) mod 4
= 8 mod 4
= 0
```

### Mnożenie modulo:
```
(a × b) mod n = ((a mod n) × (b mod n)) mod n

Przykład: (7 × 9) mod 5
= 63 mod 5
= 3

Weryfikacja: (7 mod 5) × (9 mod 5) = 2 × 4 = 8 mod 5 = 3 ✓
```

---

## 3. MODULO W LICZBACH BINARNYCH

### Modulo potęg 2:
```
n mod 2^k = n AND (2^k - 1)

Przykład: n mod 8 = n AND 7
```

### Dlaczego to działa?
```
2^3 = 8 = 1000₂
2^3 - 1 = 7 = 0111₂  ← Maska (wszystkie młodsze bity)

17 mod 8:
17₁₀ = 10001₂
AND 0111₂
    = 00001₂ = 1 ✓
```

### Praktyczne zastosowania:
```
n mod 2   = n AND 1    (czy parzyste/nieparzyste)
n mod 4   = n AND 3
n mod 16  = n AND 15
n mod 256 = n AND 255  (dolny bajt!)
```

---

## 4. OVERFLOW JAKO MODULO

### W procesorach:
```
n-bitowe rejestry działają modulo 2^n
```

### Przykład 8-bit (mod 256):
```
255 + 1 = 256 mod 256 = 0  (overflow, wrapping)
200 + 100 = 300 mod 256 = 44

Binarnie:
11111111 (255)
+      1
--------
00000000 (0)  ← Bit przepełnienia znika!
```

### Przykład 4-bit (mod 16):
```
15 + 3 = 18 mod 16 = 2

1111 (15)
+ 0011 (3)
------
10010 (18)
  ↓ 4-bit
 0010 (2) ✓
```

**To właśnie jest overflow unsigned!**

---

## 5. BUFORY KOŁOWE (RING BUFFER)

### Koncepcja:
**Indeks wraca do 0 po osiągnięciu rozmiaru**

### Przykład: bufor 8 elementów:
```
┌───┬───┬───┬───┬───┬───┬───┬───┐
│ 0 │ 1 │ 2 │ 3 │ 4 │ 5 │ 6 │ 7 │
└───┴───┴───┴───┴───┴───┴───┴───┘
  ↑                               │
  └───────────────────────────────┘
     indeks 8 wraca do 0
```

### Implementacja:
```c
#define BUFFER_SIZE 8

int index = 0;
buffer[index] = data;
index = (index + 1) % BUFFER_SIZE;  // Modulo!

// Lub szybciej (jeśli rozmiar = 2^k):
index = (index + 1) & (BUFFER_SIZE - 1);  // AND z maską
```

### Zastosowania:
✅ Kolejki FIFO
✅ Audio streaming
✅ Komunikacja szeregowa (UART)

---

## 6. LICZBY UJEMNE I MODULO

### Uwaga: różne definicje!

### W matematyce:
```
-5 mod 8 = 3  (reszta zawsze dodatnia!)

Wyjaśnienie: -5 = -1 × 8 + 3
```

### W językach C/C++:
```
-5 % 8 = -5  (zachowuje znak!)

Uwaga: % w C to reszta, nie modulo matematyczne!
```

### Prawidłowe modulo w C:
```c
int mod(int a, int n) {
    int r = a % n;
    return (r < 0) ? r + n : r;
}

mod(-5, 8) = 3 ✓
```

### W procesorach:
```
Unsigned: zawsze dodatnie (wrapping)
Signed (U2): może być ujemne (zależy od implementacji)
```

---

## 7. ZASTOSOWANIA W ADRESOWANIU

### Adresowanie cykliczne:
```
Pamięć 256 bajtów (0x00-0xFF)

addr = 0xFE
addr + 5 = 0x103 mod 0x100 = 0x03  (wrapping)
```

### Adresowanie relatywne:
```
PC = 0x1000
offset = -10 (0xFFF6 w U2)

new_PC = (0x1000 + 0xFFF6) mod 0x10000
       = 0x0FF6
```

### Hash tables:
```
hash(key) mod table_size = index

Przykład: hash=12345, size=100
index = 12345 mod 100 = 45
```

---

## 8. KONGRUENCJE

### Definicja:
```
a ≡ b (mod n)  oznacza: (a - b) mod n = 0
```

### Przykłady:
```
17 ≡ 5 (mod 4)   bo (17-5) mod 4 = 12 mod 4 = 0 ✓
25 ≡ 1 (mod 8)   bo (25-1) mod 8 = 24 mod 8 = 0 ✓
```

### Właściwości:
```
Jeśli a ≡ b (mod n) i c ≡ d (mod n), to:
- a + c ≡ b + d (mod n)
- a × c ≡ b × d (mod n)
```

---

## 9. PRZYKŁADY PRAKTYCZNE

### Przykład 1: Test parzystości
```
n mod 2:
- 0 → parzyste
- 1 → nieparzyste

Kod: if (n & 1) { /* nieparzyste */ }
```

### Przykład 2: Ostatnia cyfra dziesiętna
```
n mod 10 = ostatnia cyfra

1234 mod 10 = 4
9876 mod 10 = 6
```

### Przykład 3: Dzień tygodnia
```
Dni: 0=Pon, 1=Wt, ..., 6=Ndz

Dzisiaj = 3 (Czw)
Za 10 dni = (3 + 10) mod 7 = 13 mod 7 = 6 (Ndz)
```

### Przykład 4: Timer overflow
```
8-bit timer (0-255):

Timer = 250
delay = 10
new_Timer = (250 + 10) mod 256 = 260 mod 256 = 4
```

---

## 10. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Oblicz 27 mod 5
**A:** 27 ÷ 5 = 5 reszta 2 → **2**

### Q: Jak szybko obliczyć n mod 16 w procesorze?
**A:** n AND 15 (0x0F)

### Q: Co to znaczy, że rejestr 8-bitowy działa modulo 256?
**A:** Wartości "zawijają się": 255 + 1 = 0

### Q: Dlaczego bufory kołowe używają modulo?
**A:** Indeks wraca do 0 po osiągnięciu rozmiaru (cykliczne adresowanie)

### Q: Różnica między % w C a modulo matematyczne?
**A:** % w C zachowuje znak dla liczb ujemnych, modulo matematyczne zawsze daje wynik ≥ 0

---

## 11. SZYBKA ŚCIĄGA - TABELA

```
┌────────────────┬─────────────────────────────┐
│   OPERACJA     │         WYNIK               │
├────────────────┼─────────────────────────────┤
│ a mod n        │ Reszta z dzielenia (0..n-1) │
│ n mod 2^k      │ n AND (2^k - 1)             │
│ n mod 2        │ n AND 1 (parzystość)        │
│ n mod 256      │ n AND 0xFF (dolny bajt)     │
│ 8-bit overflow │ Modulo 256                  │
│ Ring buffer    │ index mod size              │
└────────────────┴─────────────────────────────┘

WZORY:
(a + b) mod n = ((a mod n) + (b mod n)) mod n
(a × b) mod n = ((a mod n) × (b mod n)) mod n
a ≡ b (mod n) ⟺ (a - b) mod n = 0
```

**ZAPAMIĘTAJ:**
- Modulo = reszta z dzielenia
- n mod 2^k = n AND (2^k - 1)
- Overflow = modulo (wrapping)
- Ring buffer = cykliczne adresowanie
- C: % ≠ modulo matematyczne (znak!)

