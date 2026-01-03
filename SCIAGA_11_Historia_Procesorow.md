# Ściąga 10: Historia Procesorów (8-bit do 64-bit)

---

## 1. ERA 8-BITOWA (lata 70-80)

### Procesory:
- **Intel 8080** (1974)
- **Zilog Z80** (1976)
- **MOS 6502** (1975)

### Charakterystyka:
```
Szyna danych: 8-bit
Szyna adresowa: 16-bit
Maksymalna pamięć: 2^16 = 64 KB
Częstotliwość: 1-4 MHz
```

### Zastosowania:
✅ **Commodore 64** (6502)
✅ **ZX Spectrum** (Z80)
✅ **Apple II** (6502)
✅ Pierwsze komputery osobiste

---

## 2. ERA 16-BITOWA (lata 80)

### Procesory:
- **Intel 8086** (1978) - pierwszy 16-bit
- **Intel 80286** (1982)
- **Motorola 68000** (1979)

### Intel 8086:
```
Szyna danych: 16-bit
Szyna adresowa: 20-bit
Maksymalna pamięć: 2^20 = 1 MB
Częstotliwość: 4.77-10 MHz
```

### Zastosowania:
✅ **IBM PC** (1981, 8088 - wersja 8086)
✅ **Atari ST** (68000)
✅ **Amiga** (68000)
✅ **Commodore** (68000)

**Motorola 68000 przegrała z Intelem** w latach 90 (ARM wygrał)

---

## 3. ERA 32-BITOWA (lata 90-2000)

### Procesory:
- **Intel 80386** (1985) - pierwszy 32-bit x86
- **Intel 80486** (1989)
- **Pentium** (1993)
- **ARM** (lata 90)

### Intel 386:
```
Szyna danych: 32-bit
Szyna adresowa: 32-bit
Maksymalna pamięć: 2^32 = 4 GB
Częstotliwość: 16-40 MHz
```

### Intel 386 SX:
- **Super skalarny** - wiele instrukcji równocześnie
- Pipelining rozwija skrzydła
- Przełom w wydajności

### Zastosowania:
✅ Windows 95/98/XP
✅ Eksplozja komputerów osobistych

---

## 4. ERA 64-BITOWA (2000-dziś)

### Procesory:
- **AMD Athlon 64** (2003) - pierwszy x86-64
- **Intel Core 2** (2006)
- **ARM64** (2011)
- **Apple M1/M2** (2020+)

### AMD64 (x86-64):
```
Szyna danych: 64-bit
Szyna adresowa: 48-bit (faktycznie)
Maksymalna pamięć: 2^48 = 256 TB (teoretycznie)
Częstotliwość: 2-5 GHz
```

### Dlaczego 64-bit?
✅ Adresy > 4 GB (więcej RAM)
✅ Większe rejestry (szybsze operacje)
✅ Lepsze bezpieczeństwo (ASLR)

**Uwaga:** Aplikacje 32-bit działają na 64-bit (kompatybilność)

---

## 5. PRZEŁOMY TECHNOLOGICZNE

### 1. Miedź zamiast aluminium (koniec lat 90):
```
Aluminium: opór elektryczny wysoki → max ~400 MHz
Miedź: opór elektryczny niski → 2-3 GHz możliwe!
```
**Efekt:** Skok z 400 MHz do 2-3 GHz

### 2. Wielordzeniowość (2005+):
```
Pentium 4: 1 rdzeń, 3.8 GHz (gorący, głośny)
Core 2 Duo: 2 rdzenie, 2.4 GHz (wydajniejszy!)
```
**Efekt:** Zamiast wyższego zegara → więcej rdzeni

### 3. Litografia (nm):
```
1995: 350 nm
2005: 90 nm
2015: 14 nm
2023: 5 nm (Apple M2)
```
**Efekt:** Mniejsze tranzystory = szybciej + mniej energii

---

## 6. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Jaki był pierwszy procesor 32-bitowy Intela?
**A:** Intel 80386 (1985)

### Q: Dlaczego przejście na miedź było ważne?
**A:** Miedź ma niższy opór → możliwe wyższe częstotliwości (400 MHz → 2-3 GHz)

### Q: Co to znaczy "super skalarny"?
**A:** Procesor wykonuje wiele instrukcji równocześnie (np. Intel 386 SX)

### Q: Dlaczego 64-bit lepszy niż 32-bit?
**A:** Większa przestrzeń adresowa (>4 GB RAM), większe rejestry

### Q: Kto pierwszy zrobił x86-64?
**A:** AMD (Athlon 64, 2003), potem Intel przyjął standard

---

## 7. SZYBKA ŚCIĄGA - TABELA

```
┌────────┬──────────┬───────────┬──────────────┐
│  ERA   │ DATA BUS │ MAX RAM   │   PRZYKŁAD   │
├────────┼──────────┼───────────┼──────────────┤
│ 8-bit  │   8-bit  │   64 KB   │  Z80, 6502   │
│ 16-bit │  16-bit  │    1 MB   │  8086, 68000 │
│ 32-bit │  32-bit  │    4 GB   │  386, ARM32  │
│ 64-bit │  64-bit  │  256 TB   │  AMD64, ARM64│
└────────┴──────────┴───────────┴──────────────┘

PRZEŁOMY:
- 1985: Intel 386 (pierwszy 32-bit x86)
- Koniec 90: Miedź → 400 MHz → 3 GHz
- 2003: AMD64 (pierwszy x86-64)
- 2005+: Wielordzeniowość (koniec wyścigu GHz)
```

**ZAPAMIĘTAJ:**
- 8-bit = 64 KB, 16-bit = 1 MB, 32-bit = 4 GB, 64-bit = 256 TB
- Miedź → skok częstotliwości
- Intel 386 SX = super skalarny
- AMD64 → standard 64-bit

