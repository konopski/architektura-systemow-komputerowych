# Ściąga 04: Magistrale i Adresowanie Pamięci

---

## 1. MAGISTRALE - PODSTAWY

### Definicja:
**Magistrala (bus)** = zestaw linii (przewodów) do przesyłania informacji między komponentami.

### Trzy główne magistrale:

#### a) **ADDRESS BUS** (magistrala adresowa):
```
CPU → Pamięć/Peryferia
Jednokierunkowa →
```
- Przesyła **adresy** (gdzie chcemy czytać/pisać)
- Liczba linii określa przestrzeń adresową
- Przykład: 8 linii = 2^8 = 256 adresów

#### b) **DATA BUS** (magistrala danych):
```
CPU ↔ Pamięć/Peryferia
Dwukierunkowa ↔
```
- Przesyła **dane** (co zapisujemy/odczytujemy)
- Szerokość: 8-bit, 16-bit, 32-bit, 64-bit
- **Dwukierunkowa** - czytanie i pisanie

#### c) **CONTROL BUS** (magistrala sterująca):
```
CPU → Pamięć/Peryferia
Sygnały sterujące
```
- **R/W** (Read/Write) - czy czytamy (1) czy piszemy (0)
- **NOT R/W** - zanegowane (0=read, 1=write)
- **Request signals** - żądania dostępu
- **Clock** - sygnał zegara

---

## 2. SCHEMAT MAGISTRAL

```
         ┌──────────┐
         │   CPU    │
         └────┬─────┘
              │
    ┌─────────┼─────────┐
    │         │         │
┌───▼───┐ ┌──▼──┐ ┌────▼────┐
│ADDRESS│ │DATA │ │ CONTROL │
│  BUS  │ │ BUS │ │   BUS   │
│  →    │ │  ↔  │ │    →    │
└───┬───┘ └──┬──┘ └────┬────┘
    │         │         │
    └─────────┼─────────┘
              │
         ┌────▼─────┐
         │  PAMIĘĆ  │
         └──────────┘
```

---

## 3. ADRESOWANIE PAMIĘCI - PODSTAWY

### Przestrzeń adresowa:
```
Liczba linii ADDRESS BUS = n
Przestrzeń adresowa = 2^n
```

### Przykłady:
```
8 linii  → 2^8  = 256 adresów
16 linii → 2^16 = 65 536 adresów (64 KB)
32 linii → 2^32 = 4 294 967 296 adresów (4 GB)
```

### Szybkie obliczanie:
```
2^10 ≈ 1024 ≈ 1K (kilo)
2^20 ≈ 1 048 576 ≈ 1M (mega)
2^30 ≈ 1 073 741 824 ≈ 1G (giga)
```

---

## 4. BYTE-ORIENTED vs WORD-ORIENTED

### Byte-oriented (najczęstsze):
```
Adres 0x0000 → bajt 0
Adres 0x0001 → bajt 1
Adres 0x0002 → bajt 2
...
```
- **1 adres = 1 bajt**
- 16-bit liczba zajmuje 2 adresy
- 32-bit liczba zajmuje 4 adresy

### Word-oriented (rzadkie):
```
Adres 0x0000 → słowo 0 (16-bit lub 32-bit)
Adres 0x0001 → słowo 1
...
```
- **1 adres = 1 słowo** (16 lub 32 bity)
- Oszczędność linii ADDRESS BUS

---

## 5. ALIGNMENT (WYRÓWNANIE)

### Definicja:
**Alignment** = adres podzielny przez rozmiar danych

### Przykład (32-bit):
```
✅ Aligned:
Adres 0x0000 → OK (0 ÷ 4 = 0)
Adres 0x0004 → OK (4 ÷ 4 = 1)
Adres 0x0008 → OK (8 ÷ 4 = 2)

❌ Not aligned:
Adres 0x0001 → BŁĄD (1 ÷ 4 = 0.25)
Adres 0x0003 → BŁĄD (3 ÷ 4 = 0.75)
```

### Konsekwencje "not aligned":
- **Motorola 68k:** Wyjątek! (crash programu)
- **Intel x86:** Wolniejszy dostęp (2 cykle zamiast 1)

---

## 6. BIG ENDIAN vs LITTLE ENDIAN

### Definicja:
**Endianness** = kolejność bajtów w pamięci dla liczb wielobajtowych

### Little Endian (Intel):
```
Liczba: 0x12345678
Adres 0x00: 0x78  ← LSB (Least Significant Byte)
Adres 0x01: 0x56
Adres 0x02: 0x34
Adres 0x03: 0x12  ← MSB (Most Significant Byte)
```
**LSB pod najmniejszym adresem**

### Big Endian (Motorola, ARM):
```
Liczba: 0x12345678
Adres 0x00: 0x12  ← MSB
Adres 0x01: 0x34
Adres 0x02: 0x56
Adres 0x03: 0x78  ← LSB
```
**MSB pod najmniejszym adresem**

---

## 7. TRANSMISJA SZEREGOWA - ENDIANNESS

### Pytanie: Big czy Little Endian?

**ODPOWIEDŹ: SPRAWDŹ DOKUMENTACJĘ!**

### Dlaczego?
- **Brak standardu** - każdy protokół może być inny
- **TCP/IP:** Big Endian (network byte order)
- **USB:** Little Endian
- **CAN:** Big Endian
- **Ethernet:** Big Endian (ramka)

### Ważne:
```
NIGDY nie zakładaj!
Zawsze czytaj dokumentację protokołu!
```

---

## 8. KONWERSJA ADRESÓW: SŁOWA ↔ BAJTY

### Słowa → Bajty (ŁATWE):
```
Adres_bajtowy = Adres_słowowy × rozmiar_słowa

Przykład (16-bit słowo):
Słowo 0 → Bajt 0 (0 × 2 = 0)
Słowo 1 → Bajt 2 (1 × 2 = 2)
Słowo 5 → Bajt 10 (5 × 2 = 10)
```

### Bajty → Słowa (TRUDNE):
```
Adres_słowowy = Adres_bajtowy ÷ rozmiar_słowa

Przykład (16-bit słowo):
Bajt 0 → Słowo 0 (0 ÷ 2 = 0)
Bajt 2 → Słowo 1 (2 ÷ 2 = 1)
Bajt 5 → ??? (5 ÷ 2 = 2.5) ← BŁĄD!
```

**Uwaga:** Nie każdy adres bajtowy ma odpowiednik w słowach!

---

## 9. PRZYKŁAD: ODCZYT Z PAMIĘCI

### Scenariusz: CPU chce odczytać bajt z adresu 0x1234

```
Krok 1: CPU wysyła adres
┌────┐  ADDRESS BUS: 0x1234  ┌────────┐
│CPU │ ────────────────────→ │ PAMIĘĆ │
└────┘                        └────────┘

Krok 2: CPU ustawia R/W = 1 (READ)
┌────┐  CONTROL: R/W=1       ┌────────┐
│CPU │ ────────────────────→ │ PAMIĘĆ │
└────┘                        └────────┘

Krok 3: Pamięć wysyła dane
┌────┐  DATA BUS: 0xAB       ┌────────┐
│CPU │ ←──────────────────── │ PAMIĘĆ │
└────┘                        └────────┘
```

---

## 10. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Co to jest magistrala?
**A:** Zestaw linii (przewodów) do przesyłania informacji między CPU a pamięcią/peryferiami.

### Q: Jakie są trzy główne magistrale?
**A:** ADDRESS (adresy →), DATA (dane ↔), CONTROL (sygnały sterujące →).

### Q: Jak obliczyć przestrzeń adresową?
**A:** 2^n, gdzie n = liczba linii ADDRESS BUS.

### Q: Co to jest alignment?
**A:** Adres podzielny przez rozmiar danych (np. 32-bit → adres ÷ 4 = liczba całkowita).

### Q: Różnica między Big a Little Endian?
**A:** Little: LSB pod najmniejszym adresem, Big: MSB pod najmniejszym adresem.

---

## 11. SZYBKA ŚCIĄGA - TABELA

```
┌──────────────┬─────────────────────────────────┐
│  MAGISTRALA  │          CHARAKTERYSTYKA         │
├──────────────┼─────────────────────────────────┤
│   ADDRESS    │  → jednokierunkowa, adresy      │
│    DATA      │  ↔ dwukierunkowa, dane          │
│   CONTROL    │  → sygnały (R/W, Clock)         │
└──────────────┴─────────────────────────────────┘

┌──────────────┬─────────────┬─────────────┐
│    CECHA     │ Byte-orient │ Word-orient │
├──────────────┼─────────────┼─────────────┤
│ 1 adres =    │   1 bajt    │   1 słowo   │
│ 16-bit data  │  2 adresy   │   1 adres   │
│ Elastyczność │    Wysoka   │    Niska    │
└──────────────┴─────────────┴─────────────┘
```

**ZAPAMIĘTAJ:**
- ADDRESS → adresy (→)
- DATA → dane (↔)
- CONTROL → sterowanie (→)
- 2^n = przestrzeń adresowa
- Little Endian = LSB@addr_0 (Intel)
- Big Endian = MSB@addr_0 (Motorola, ARM)

