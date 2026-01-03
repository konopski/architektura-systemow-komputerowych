# Egzamin - Architektura Systemów Komputerowych
## Zestaw 01 - ROZWIĄZANIA

---

## Zadanie 1. Arytmetyka binarna (10 pkt)

### a) Dodawanie unsigned (5 pkt):

```
  1101  (13)
+ 0110  (6)
------
 10011  (19)
 ↑
 C=1
```

**Rozwiązanie:**
- Wynik binarny: **10011** (lub 0011 jeśli 4-bitowy)
- Flaga **C** (Carry): **1** (było przeniesienie z najstarszego bitu)
- Wynik dziesiętny: **19** (13 + 6 = 19)

**Punktacja:**
- Poprawny wynik binarny: 2 pkt
- Poprawna flaga C: 1 pkt
- Poprawny wynik dziesiętny: 2 pkt

---

### b) Dodawanie U2 signed (5 pkt):

```
  1011  (-5 w U2)
+ 0101  (+5)
------
 10000
 ↑
 C=1

Wynik 4-bitowy: 0000
```

**Analiza:**
- A = 1011 → znak **-** (bit znaku = 1)
- B = 0101 → znak **+** (bit znaku = 0)
- Wynik = 0000 → znak **+** (bit znaku = 0)

**Test Overflow:**
- A i B mają **różne znaki** (- i +)
- **(-) + (+) = może być cokolwiek** → **V = 0** ✓

**Rozwiązanie:**
- Wynik binarny: **10000** (5-bitowy) lub **0000** (4-bitowy)
- Flaga **C** (Carry): **1**
- Flaga **V** (Overflow): **0** (znaki różne, więc nie ma overflow)
- Prawidłowy wynik: **0000** (bo V=0, ignorujemy C)
- Wynik dziesiętny: **0** (-5 + 5 = 0) ✓

**Punktacja:**
- Poprawny wynik binarny: 1 pkt
- Poprawna flaga C: 1 pkt
- Poprawna flaga V: 1 pkt
- Prawidłowa interpretacja: 1 pkt
- Poprawny wynik dziesiętny: 1 pkt

---

## Zadanie 2. Pytania teoretyczne (10 pkt)

### 1. von Neumann vs Harvard (2 pkt)

**Dwie główne różnice:**
1. **Magistrale:** von Neumann ma **jedną wspólną** magistralę, Harvard ma **dwie osobne** (dla kodu i danych)
2. **Pamięć:** von Neumann ma **jedną wspólną** pamięć, Harvard ma **dwie osobne** (Code Memory i Data Memory)

**Zaleta Harvarda:**
- **Szybsza** - może równolegle pobierać kod i dane (łatwiejszy pipelining)
- LUB: **Bezpieczniejsza** - nie można nadpisać kodu danymi

**Wada Harvarda:**
- **Droższa** - wymaga dwóch pamięci i więcej połączeń
- LUB: **Mniej elastyczna** - kod nie może się zmieniać w czasie działania

**Punktacja:** 2 pkt (po 0.5 pkt za każdy element)

---

### 2. RISC vs CISC (2 pkt)

**Główna różnica:**
- **RISC:** Operacje wykonywane **tylko na rejestrach** (dostęp do pamięci tylko przez LOAD/STORE)
- **CISC:** Operacje mogą być wykonywane **bezpośrednio na pamięci**

**Przykłady:**
- **RISC:** ARM, ATmega (AVR), RISC-V, MIPS
- **CISC:** Intel x86, Intel x86-64, Motorola 68000

**Punktacja:** 2 pkt (1 pkt za różnicę, 1 pkt za przykłady)

---

### 3. Flaga Overflow (2 pkt)

**Flaga V=1 gdy:**
1. **(+) + (+) = (-)** - suma dwóch liczb dodatnich daje ujemną (niemożliwe!)
2. **(-) + (-) = (+)** - suma dwóch liczb ujemnych daje dodatnią (niemożliwe!)

**Wyjaśnienie:**
Overflow występuje, gdy wynik ma **błędny znak** - oba składniki mają ten sam znak, ale wynik ma inny.

**Punktacja:** 2 pkt (po 1 pkt za każdy przypadek)

---

### 4. Big Endian vs Little Endian (2 pkt)

**Liczba: 0x1234ABCD**

**Little Endian** (LSB pod najmniejszym adresem):
- 0x100: **CD**
- 0x101: **AB**
- 0x102: **34**
- 0x103: **12**

**Big Endian** (MSB pod najmniejszym adresem):
- 0x100: **12**
- 0x101: **34**
- 0x102: **AB**
- 0x103: **CD**

**Punktacja:** 2 pkt (1 pkt za Little, 1 pkt za Big)

---

### 5. Pipelining (2 pkt)

**Trzy etapy:**

1. **FETCH (Pobieranie)**
   - Odczytaj instrukcję z Code Memory pod adresem PC
   - Zapisz do IR (Instruction Register)
   - Inkrementuj PC (PC++)

2. **DECODE (Dekodowanie)**
   - Dekoder analizuje instrukcję w IR
   - Identyfikuje operację (ADD, SUB, ...)
   - Identyfikuje operandy (rejestry)

3. **EXECUTE (Wykonanie)**
   - ALU wykonuje operację
   - Wynik zapisywany do rejestru docelowego
   - Aktualizacja flag (C, Z, V, N, ...)

**Punktacja:** 2 pkt (po ~0.66 pkt za każdy etap)

---

## Punktacja końcowa:
- **Zadanie 1a:** 5 pkt
- **Zadanie 1b:** 5 pkt
- **Zadanie 2 (5 pytań × 2 pkt):** 10 pkt
- **RAZEM:** 20 pkt
