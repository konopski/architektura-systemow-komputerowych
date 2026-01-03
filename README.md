# 📚 Zalecana Kolejność Nauki - Architektura Systemów Komputerowych

---

## 🎯 Ścieżka pedagogiczna - od podstaw do zaawansowanych

### Poziom 1️⃣ - FUNDAMENTY (zacznij tutaj!)

**01. Systemy Liczbowe** (`SCIAGA_01_Systemy_Liczbowe.md`)
- 📌 Bin, Hex, Oct, BCD
- 📌 **U2 (uzupełnienie do dwóch)** ← KLUCZOWE!
- 📌 Konwersje między systemami
- ⏱️ Czas nauki: ~30 min
- ✅ **Musisz to opanować przed przejściem dalej!**

**02. Arytmetyka Binarna** (`SCIAGA_02_Arytmetyka_Binarna.md`)
- 📌 Dodawanie unsigned i signed (U2)
- 📌 Flagi: C, V, Z, N, H, S
- 📌 Overflow vs Carry
- ⏱️ Czas nauki: ~45 min
- ⚠️ **Wymaga znajomości #01 (U2)**

**03. Arytmetyka Modulo** (`SCIAGA_03_Arytmetyka_Modulo.md`)
- 📌 Modulo w procesorach
- 📌 Bufory kołowe
- 📌 Overflow = modulo 2^n
- ⏱️ Czas nauki: ~20 min
- 💡 Rozszerza wiedzę z #02

---

### Poziom 2️⃣ - HARDWARE (budowa procesorów)

**04. Technika Cyfrowa** (`SCIAGA_04_Technika_Cyfrowa.md`)
- 📌 Bramki logiczne (AND, OR, XOR, NAND)
- 📌 Half Adder, Full Adder
- 📌 Multiplexer, Rejestry (flip-flop)
- ⏱️ Czas nauki: ~40 min
- 💡 Fizyczna realizacja arytmetyki z #02

**05. Rejestry i Cykl Rozkazowy** (`SCIAGA_05_Rejestry_i_Cykl_Rozkazowy.md`)
- 📌 PC, IR, SREG
- 📌 FETCH → DECODE → EXECUTE
- 📌 Pipelining
- ⏱️ Czas nauki: ~35 min
- 💡 Jak procesor działa wewnętrznie

**06. Magistrale i Adresowanie** (`SCIAGA_06_Magistrale_i_Adresowanie.md`)
- 📌 ADDRESS, DATA, CONTROL
- 📌 Big Endian vs Little Endian
- 📌 Alignment, przestrzeń adresowa
- ⏱️ Czas nauki: ~30 min
- 💡 Jak procesor komunikuje się z pamięcią

---

### Poziom 3️⃣ - ARCHITEKTURY (organizacja systemów)

**07. Architektury Pamięci** (`SCIAGA_07_Architektury_Pamieci.md`)
- 📌 von Neumann vs Harvard
- 📌 Hybrydy (RISC-V, ARM)
- 📌 Code Memory vs Data Memory
- ⏱️ Czas nauki: ~30 min
- 💡 Różne podejścia do organizacji pamięci

**08. RISC vs CISC** (`SCIAGA_08_RISC_vs_CISC.md`)
- 📌 Główna różnica (operacje na rejestrach vs pamięci)
- 📌 ARM vs Intel
- 📌 AMD - hybryda (mikrokod)
- ⏱️ Czas nauki: ~25 min
- 💡 Filozofie projektowania procesorów

---

### Poziom 4️⃣ - PRAKTYKA (konkretne procesory)

**09. Instrukcje AVR** (`SCIAGA_09_Instrukcje_AVR.md`)
- 📌 ADD, SUB, MUL, CP
- 📌 BREQ, BRNE, CALL, RET
- 📌 Różnica INC vs ADD
- ⏱️ Czas nauki: ~40 min
- 💡 Praktyczne zastosowanie wiedzy z #02, #05

---

### Poziom 5️⃣ - ZAAWANSOWANE (szerszy kontekst)

**10. Wielordzeniowość, GPU, Turing** (`SCIAGA_10_Wielordzeniowość_GPU.md`)
- 📌 Limit 20-32 rdzeni (bottleneck)
- 📌 GPU vs CPU
- 📌 Maszyna Turinga, Test Turinga, Enigma
- ⏱️ Czas nauki: ~30 min
- 💡 Współczesne architektury i historia

**11. Historia Procesorów** (`SCIAGA_11_Historia_Procesorow.md`)
- 📌 8-bit → 16-bit → 32-bit → 64-bit
- 📌 Intel 386, Motorola 68k
- 📌 Miedź vs aluminium, wielordzeniowość
- ⏱️ Czas nauki: ~25 min
- 💡 Kontekst historyczny i ewolucja

---

## 📊 Mapa Zależności

```
                    ┌─────────────┐
                    │ 01. SYSTEMY │ ← START TUTAJ!
                    │  LICZBOWE   │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ 02. ARYTM.  │
                    │   BINARNA   │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ 03. MODULO  │
                    └──────┬──────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
    ┌─────▼─────┐   ┌──────▼──────┐  ┌─────▼─────┐
    │04.TECHNIKA│   │05. REJESTRY │  │06.MAGISTR.│
    │  CYFROWA  │   │  i CYKL     │  │i ADRESOW. │
    └─────┬─────┘   └──────┬──────┘  └─────┬─────┘
          │                │                │
          └────────────────┼────────────────┘
                           │
                    ┌──────▼──────┐
                    │07.ARCHITEKT.│
                    │   PAMIĘCI   │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  08. RISC   │
                    │   vs CISC   │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │09.INSTRUKCJE│
                    │     AVR     │
                    └──────┬──────┘
                           │
          ┌────────────────┼────────────────┐
          │                                 │
    ┌─────▼─────┐                    ┌─────▼─────┐
    │  10. GPU  │                    │11. HISTORIA│
    │   TURING  │                    │ PROCESORÓW │
    └───────────┘                    └───────────┘
```

---

## ⏰ Plan Nauki

### 📅 PLAN 1-DNIOWY (Intensywny, ~5h):
1. Rano: #01, #02, #03 (podstawy matematyczne)
2. Popołudnie: #04, #05, #06 (hardware)
3. Wieczór: #07, #08, #09 (architektury + AVR)
4. Przegląd: #10, #11 (kontekst)

### 📅 PLAN 3-DNIOWY (Komfortowy):
- **Dzień 1:** #01, #02, #03 + ćwiczenia z arytmetyki
- **Dzień 2:** #04, #05, #06, #07 + rysowanie schematów
- **Dzień 3:** #08, #09, #10, #11 + powtórka + egzaminy próbne

### 📅 PLAN TYGODNIOWY (Spokojny):
- **Pon:** #01 Systemy + #02 Arytmetyka
- **Wt:** #03 Modulo + #04 Technika cyfrowa
- **Śr:** #05 Rejestry + #06 Magistrale
- **Czw:** #07 Architektury + #08 RISC/CISC
- **Pt:** #09 Instrukcje AVR
- **Sob:** #10 GPU/Turing + #11 Historia
- **Ndz:** Powtórka + 10 zestawów egzaminacyjnych

---

## 🎓 Materiały Dodatkowe

### Po opanowaniu ściąg, przejdź do:
1. **10 zestawów egzaminacyjnych** (`EGZAMIN_ZESTAW_01.md` - `_10.md`)
2. **Rozwiązania** (`EGZAMIN_ZESTAW_01_ROZWIAZANIA.md` - `_10_ROZWIAZANIA.md`)

### Strategia egzaminów próbnych:
- Zrób zestaw 1, 2, 3 **bez zaglądania** w ściągi
- Sprawdź rozwiązania
- Uzupełnij wiedzę ze ściąg
- Powtórz dla zestawów 4-10

---

## ✅ Checkpointy - Czy jestem gotowy?

### Po ściądze #01:
- ✅ Potrafię zamienić hex ↔ bin ↔ dec
- ✅ Rozumiem U2 (wiem że 1011 = -5 w 4-bit)
- ✅ Umiem negować liczby w U2 (NOT + 1)

### Po ściądze #02:
- ✅ Potrafię dodawać liczby binarne "słupkiem"
- ✅ Wiem kiedy V=1 (overflow): (+)+(+)=(-) lub (-)+(-)=(+)
- ✅ Rozumiem różnicę między C a V

### Po ściądze #05:
- ✅ Rozumiem cykl FETCH → DECODE → EXECUTE
- ✅ Wiem co to PC i IR
- ✅ Potrafię wyjaśnić pipelining

### Po ściądze #09:
- ✅ Znam różnicę INC vs ADD (flaga C!)
- ✅ Wiem że MUL → wynik w R1:R0
- ✅ Rozumiem CALL vs RET

---

## 🚀 GOTOWY NA EGZAMIN!

Po przejściu wszystkich 11 ściąg + 10 zestawów egzaminacyjnych jesteś w pełni przygotowany!

**Powodzenia! 💪**
