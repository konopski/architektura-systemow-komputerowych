# Egzamin - Architektura Systemów Komputerowych
## Zestaw 02 - ROZWIĄZANIA

---

## Zadanie 1. Arytmetyka binarna (10 pkt)

### a) Dodawanie unsigned (5 pkt):

```
  1111  (15)
+ 0011  (3)
------
 10010  (18)
 ↑
 C=1
```

**Rozwiązanie:**
- Wynik binarny: **10010** (lub 0010 jeśli 4-bitowy)
- Flaga **C** (Carry): **1** (było przeniesienie)
- Wynik dziesiętny: **18** (15 + 3 = 18)

---

### b) Dodawanie U2 signed (5 pkt):

```
  1100  (-4 w U2)
+ 1110  (-2 w U2)
------
 11010
 ↑
 C=1

Wynik 4-bitowy: 1010
```

**Analiza:**
- A = 1100 → znak **-** (bit = 1) → -4
- B = 1110 → znak **-** (bit = 1) → -2
- Wynik = 1010 → znak **-** (bit = 1)

**Test Overflow:**
- A i B mają **ten sam znak** (oba ujemne -)
- Wynik **też ujemny** (-)
- **(-) + (-) = (-)**  → Prawidłowy znak! → **V = 0** ✓

**Interpretacja U2:**
- 1010 w U2 = -(16-10) = -6 ✓
- -4 + (-2) = -6 ✓ Prawidłowo!

**Rozwiązanie:**
- Wynik binarny: **11010** (5-bit) lub **1010** (4-bit)
- Flaga **C**: **1**
- Flaga **V**: **0** (znaki się zgadzają)
- Prawidłowy wynik: **1010**
- Wynik dziesiętny: **-6**

---

## Zadanie 2. Pytania teoretyczne (10 pkt)

### 1. Magistrale (2 pkt)

**Trzy rodzaje magistral:**

1. **ADDRESS BUS (magistrala adresowa)**
   - Przesyła **adresy** pamięci/peryferiów
   - Jednokierunkowa (CPU → Pamięć)

2. **DATA BUS (magistrala danych)**
   - Przesyła **dane** (odczyt/zapis)
   - **Dwukierunkowa** (CPU ↔ Pamięć)

3. **CONTROL BUS (magistrala sterująca)**
   - Przesyła **sygnały sterujące** (R/W, Clock, Request)
   - Jednokierunkowa (CPU → Pamięć)

---

### 2. ALU (2 pkt)

**Definicja:**
ALU (Arithmetic Logic Unit) = jednostka arytmetyczno-logiczna procesora wykonująca operacje.

**Cztery operacje:**
1. **Arytmetyczne:** ADD, SUB, MUL, DIV
2. **Logiczne:** AND, OR, XOR, NOT
3. **Przesunięcia:** LSL, LSR, ROL, ROR
4. **Porównania:** CP, CPI

---

### 3. Instrukcje RISC (2 pkt)

**Trzy instrukcje RISC:**
1. **LOAD R1, [addr1]** - załaduj pierwszą liczbę z pamięci do rejestru
2. **LOAD R2, [addr2]** - załaduj drugą liczbę z pamięci do rejestru
3. **ADD R3, R1, R2** - dodaj R1 + R2 → R3
4. **STORE R3, [addr3]** - zapisz wynik do pamięci

**W CISC wystarczy:**
```
ADD [addr3], [addr1]  ; Dodaj pamięć+pamięć → pamięć
```
(jedna instrukcja, bo CISC może operować bezpośrednio na pamięci)

---

### 4. Przestrzeń adresowa (2 pkt)

**Obliczenia:**
- Magistrala adresowa: **16-bit**
- Przestrzeń = **2^16 = 65 536 bajtów**
- W kilobajtach: **64 KB** (65536 ÷ 1024 = 64)

**Wzór:**
```
Przestrzeń adresowa = 2^n (gdzie n = liczba linii ADDRESS BUS)
2^16 = 65 536 bajtów = 64 KB
```

---

### 5. Uzupełnienie do dwóch - negacja (2 pkt)

**Algorytm negacji w U2:**

1. **Zaneguj wszystkie bity** (NOT - zamień 0↔1)
2. **Dodaj 1** do wyniku

**Przykład: +5 → -5**
```
+5  = 0101
NOT = 1010
+1  = 1011  → to jest -5 w U2 ✓
```

**Weryfikacja: -5 → +5**
```
-5  = 1011
NOT = 0100
+1  = 0101  → to jest +5 ✓
```

---

## Punktacja końcowa:
- **Zadanie 1a:** 5 pkt
- **Zadanie 1b:** 5 pkt
- **Zadanie 2 (5 pytań × 2 pkt):** 10 pkt
- **RAZEM:** 20 pkt
