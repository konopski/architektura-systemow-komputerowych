# Ściąga 12: Schemat Procesora RISC

---

## 1. SCHEMAT BLOKOWY PROCESORA RISC

```
┌─────────────────────────────────────────────────────────────┐
│                    PROCESOR RISC                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────┐                                              │
│  │    PC    │──────┐ (adres)                               │
│  │ Program  │      │                                       │
│  │ Counter  │◄─────┼───(+1 / skok)                         │
│  └──────────┘      │                                       │
│                    │                                       │
│                    ▼                                       │
│           ┌─────────────────┐                             │
│           │  CODE MEMORY    │                             │
│           │  (pamięć kodu)  │                             │
│           └────────┬────────┘                             │
│                    │ (instrukcja)                         │
│                    ▼                                       │
│           ┌─────────────────┐                             │
│           │   IR / RI       │                             │
│           │   Instruction   │                             │
│           │   Register      │                             │
│           │ (rej. instrukcji)│                            │
│           └────────┬────────┘                             │
│                    │                                       │
│                    ▼                                       │
│           ┌─────────────────┐                             │
│           │   DECODER       │                             │
│           │  Instruction    │                             │
│           └─┬─────┬─────┬───┘                             │
│             │     │     │                                 │
│             ▼     ▼     ▼                                 │
│           ┌───┐ ┌───┐ ┌───┐                              │
│           │M0 │ │M1 │ │M2 │  (rejestry sterujące)        │
│           └─┬─┘ └─┬─┘ └─┬─┘                              │
│             │     │     │                                 │
│    ┌────────┼─────┼─────┼────────┐                       │
│    │        │     │     │        │                       │
│    │   ┌────┼─────┘     └────┐   │                       │
│    │   │    │                │   │                       │
│    │   │    │  ┌───────┐    │   │                       │
│    │   │    └─►│  MUX  │◄───┘   │                       │
│    │   │       │  M1   │        │                       │
│    │   │       └───┬───┘        │                       │
│    │   │           │  ┌───────┐ │                       │
│    │   │           └─►│  MUX  │◄┘                       │
│    │   │              │  M2   │                         │
│    │   │              └───┬───┘                         │
│    │   │                  │                             │
│    │   ▼                  ▼                             │
│    │ ┌─────────────────────────────┐                   │
│    │ │          ALU                │                   │
│    │ │  Jednostka Arytmetyczno-    │                   │
│    │ │        Logiczna             │                   │
│    │ │  (ADD, SUB, AND, OR, XOR...) │                  │
│    │ └──────────┬──────────────────┘                   │
│    │            │ (wynik)                              │
│    │            ▼                                       │
│    │  ┌───┐  ┌───┐  ┌───┐  ┌───┐                      │
│    └─►│R0 │  │R1 │  │R2 │  │R3 │  (rejestry uniw.)    │
│       └─┬─┘  └─┬─┘  └─┬─┘  └─┬─┘                      │
│         └─────┴─────┴─────┴───────────┐               │
│                                        │               │
│                            (feedback)  │               │
│                                        │               │
└────────────────────────────────────────┘
```

---

## 2. ELEMENTY PROCESORA - OPIS

### PC - Program Counter (Licznik Rozkazów)
**Funkcje:**
- Przechowuje adres **aktualnie wykonywanej instrukcji**
- Adresuje **Code Memory** (pamięć programu)
- Automatycznie **inkrementuje się** (+1, +4, zależnie od architektury)
- Może wykonywać **skoki** (jump) - zmiana wartości przez decoder

**Przykład:**
```
PC = 0x1000  → pobierz instrukcję z adresu 0x1000
PC = 0x1004  → następna instrukcja (+4 bajty)
JUMP 0x2000  → PC = 0x2000 (skok)
```

---

### IR / RI - Instruction Register (Rejestr Instrukcji)
**Funkcje:**
- Przechowuje **ostatnio pobraną instrukcję** z Code Memory
- Instrukcja jest zapisana w **kodzie maszynowym** (binarnie)
- Przekazuje instrukcję do **Decodera**

**Przykład instrukcji w IR:**
```
ADD R1, R2  → 0b00010010  (kod maszynowy)
```

---

### Decoder Instrukcji (Instruction Decoder)
**Funkcje:**
- **Układ logiki kombinacyjnej** (nie rejestr!)
- Dekoduje instrukcję z IR
- Wyciąga informacje: **CO** zrobić? **KTO** bierze udział?
- Steruje rejestrami M0, M1, M2

**Dekodowanie:**
```
IR: ADD R1, R2
       ↓
Decoder wyciąga:
- Operacja: ADD  → M0
- Arg1: R1       → M1
- Arg2: R2       → M2
```

---

### M0, M1, M2 - Rejestry Sterujące
**Funkcje:**
- **M0** - określa **operację** dla ALU (ADD, SUB, AND, OR...)
- **M1** - wybiera **pierwszy operand** (który rejestr R0-R3)
- **M2** - wybiera **drugi operand** (który rejestr R0-R3)

**Przechowują informacje z Decodera** do następnego cyklu zegarowego.

---

### MUX (Multiplexer) - M1 i M2
**Funkcje:**
- **Selektor** - wybiera jedno z wielu wejść
- **MUX M1** - wybiera jeden z R0-R3 jako pierwszy operand ALU
- **MUX M2** - wybiera jeden z R0-R3 jako drugi operand ALU
- Sterowane przez rejestry M1 i M2

**Przykład:**
```
M1 = 01 (binarnie) → wybierz R1
M2 = 10 (binarnie) → wybierz R2
```

---

### ALU - Jednostka Arytmetyczno-Logiczna
**Funkcje:**
- Wykonuje **operacje arytmetyczne**: ADD, SUB, MUL, DIV
- Wykonuje **operacje logiczne**: AND, OR, XOR, NOT
- Operacja wybierana przez **M0**
- Operandy dostarczane z **MUX M1** i **MUX M2**

**Typowe operacje:**
```
ADD:  A + B
SUB:  A - B
AND:  A & B
OR:   A | B
XOR:  A ^ B
SHL:  A << 1  (shift left)
SHR:  A >> 1  (shift right)
```

---

### R0-R3 - Rejestry Uniwersalne (General Purpose Registers)
**Funkcje:**
- **Przechowują dane** - wyniki operacji, zmienne
- **Podają operandy** do ALU (przez MUX)
- **Przyjmują wyniki** z ALU
- W prawdziwych procesorach: 8, 16, 32 rejestry (np. ARM: 16, AVR: 32)

**RISC: Operacje TYLKO na rejestrach!**

**Zapadki (Enable):**
- **Decoder** steruje, który rejestr ma zapisać wynik
- **Enable** = "pozwól zapisać wartość"
- Zwykle **rejestr docelowy = pierwszy operand** (R1 = R1 + R2)

---

## 3. CYKL ROZKAZOWY (3-CYKLOWY)

### FETCH → DECODE → EXECUTE

```
┌─────────────────────────────────────────────────────────┐
│  CYKL 1: FETCH (Pobranie instrukcji)                   │
├─────────────────────────────────────────────────────────┤
│  1. PC wskazuje adres w Code Memory                    │
│  2. Instrukcja pobierana z pamięci                     │
│  3. Instrukcja zapisywana do IR                        │
│  4. PC += 1 (lub +4)                                   │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│  CYKL 2: DECODE (Dekodowanie instrukcji)               │
├─────────────────────────────────────────────────────────┤
│  1. Decoder analizuje instrukcję z IR                  │
│  2. Ustawienie M0 (jaka operacja?)                     │
│  3. Ustawienie M1 (który rejestr - arg1?)              │
│  4. Ustawienie M2 (który rejestr - arg2?)              │
│  5. MUX-y wybierają odpowiednie rejestry               │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│  CYKL 3: EXECUTE (Wykonanie instrukcji)                │
├─────────────────────────────────────────────────────────┤
│  1. ALU wykonuje operację (sterowaną przez M0)         │
│  2. Wynik z ALU                                        │
│  3. Zapis wyniku do rejestru docelowego (R0-R3)        │
│  4. LUB: PC = nowa wartość (dla skoków)                │
└─────────────────────────────────────────────────────────┘
```

---

## 4. PRZYKŁAD WYKONANIA INSTRUKCJI

### Instrukcja: ADD R1, R2  (R1 = R1 + R2)

**Stan początkowy:**
```
PC = 0x100
R1 = 5
R2 = 3
```

**CYKL 1 - FETCH:**
```
1. PC (0x100) → Code Memory
2. Instrukcja "ADD R1, R2" → IR
3. PC = 0x104 (+=4)
```

**CYKL 2 - DECODE:**
```
Decoder analizuje IR:
- Operacja: ADD    → M0 = 0b00 (kod dla ADD)
- Arg1: R1         → M1 = 0b01 (wybierz R1)
- Arg2: R2         → M2 = 0b10 (wybierz R2)

MUX M1 wybiera R1 (wartość: 5)
MUX M2 wybiera R2 (wartość: 3)
```

**CYKL 3 - EXECUTE:**
```
1. ALU otrzymuje:
   - Operacja: ADD (z M0)
   - Operand A: 5 (z MUX M1 → R1)
   - Operand B: 3 (z MUX M2 → R2)
2. ALU wykonuje: 5 + 3 = 8
3. Wynik (8) zapisany do R1
```

**Stan końcowy:**
```
R1 = 8  ← zmienione!
R2 = 3
PC = 0x104
```

---

## 5. PIPELINE (Potok Rozkazowy)

### Sekwencja bez potoku (3 cykle na instrukcję):
```
Instrukcja 1: [FETCH][DECODE][EXECUTE]
Instrukcja 2:                         [FETCH][DECODE][EXECUTE]
Instrukcja 3:                                                 [FETCH][DECODE][EXECUTE]

Czas: 9 cykli na 3 instrukcje
```

### Z potokiem (1 cykl na instrukcję po wypełnieniu):
```
Instr 1:  [FETCH][DECODE][EXECUTE]
Instr 2:        [FETCH][DECODE][EXECUTE]
Instr 3:              [FETCH][DECODE][EXECUTE]

Czas: 5 cykli na 3 instrukcje! (3x szybciej)
```

**Zalety potoku:**
- Zwiększona przepustowość
- Lepsze wykorzystanie zasobów
- RISC → proste instrukcje → łatwiej zrobić potok

**Problemy potoku:**
- Hazardy danych (instrukcja 2 potrzebuje wyniku instrukcji 1)
- Skoki (branch) - przewidywanie skoków

---

## 6. RISC VS CISC - RÓŻNICE W SCHEMACIE

### RISC (Reduced Instruction Set Computer)
```
✅ Operacje TYLKO na rejestrach (R0-R3)
✅ Proste instrukcje
✅ Łatwy pipeline
✅ Szybki zegar
```

**Przykład RISC (ARM, AVR):**
```assembly
LOAD R1, [addr]   ; 1. Załaduj z pamięci do R1
ADD  R1, R2       ; 2. Dodaj R1 + R2
STORE R1, [addr]  ; 3. Zapisz do pamięci
```

### CISC (Complex Instruction Set Computer)
```
❌ Operacje bezpośrednio na pamięci
❌ Złożone instrukcje
❌ Trudniejszy pipeline
❌ Wolniejszy zegar
```

**Przykład CISC (x86):**
```assembly
ADD [addr], R2    ; 1 instrukcja: pobierz z pamięci, dodaj, zapisz
```

**Różnica:**
- RISC: 3 instrukcje, każda prosta, szybki pipeline
- CISC: 1 instrukcja, złożona, trudny pipeline

---

## 7. ARM - WYJĄTEK OD REGUŁY

### Standardowy RISC:
```
ADD R1, R2   → R1 = R1 + R2  (cel = pierwszy operand)
```

### ARM (egzcentryczny):
```
ADD R0, R1, R2   → R0 = R1 + R2  (3 argumenty!)
```

**Różnica w schemacie:**
- Standardowy RISC: 2 multiplexery (M1, M2)
- ARM: 3 multiplexery (M1, M2, **M3 dla celu**)

**Zaleta ARM:**
- Więcej elastyczności
- Nie nadpisujemy operandu

---

## 8. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Opisz cykl rozkazowy FETCH-DECODE-EXECUTE
**A:**
1. **FETCH**: PC → Code Memory → IR, PC += 1
2. **DECODE**: Decoder → M0/M1/M2, MUX wybierają rejestry
3. **EXECUTE**: ALU wykonuje operację, wynik → rejestr

### Q: Jaka jest rola Decodera?
**A:** Decoder to logika kombinacyjna, która dekoduje instrukcję z IR i ustawia rejestry sterujące M0 (operacja), M1 (arg1), M2 (arg2).

### Q: Po co multiplexery (MUX)?
**A:** MUX wybierają, który rejestr (R0-R3) ma być podłączony do ALU jako operand. Sterowane przez M1 i M2.

### Q: Czym różni się RISC od CISC?
**A:**
- **RISC**: operacje tylko na rejestrach, proste instrukcje, łatwy pipeline
- **CISC**: operacje na pamięci, złożone instrukcje, trudny pipeline

### Q: Co to jest pipeline?
**A:** Równoległe wykonywanie etapów różnych instrukcji (FETCH instr2 podczas DECODE instr1). Przyspiesza wykonanie programu.

### Q: Co to jest "zapadka" (enable)?
**A:** Sygnał sterujący, który pozwala rejestrowi zapisać wartość. Decoder steruje zapadkami, aby wybrać właściwy rejestr docelowy.

---

## 9. SZYBKA ŚCIĄGA - TABELA

```
┌──────────────┬─────────────────────────────────────────────┐
│   ELEMENT    │              FUNKCJA                        │
├──────────────┼─────────────────────────────────────────────┤
│ PC           │ Program Counter - adresuje pamięć kodu     │
│ IR / RI      │ Instruction Register - przechowuje instrukcję│
│ Decoder      │ Dekoduje instrukcję → M0, M1, M2           │
│ M0           │ Wybiera operację dla ALU (ADD, SUB...)     │
│ M1, M2       │ Wybierają rejestry-operandy (R0-R3)        │
│ MUX          │ Multiplexer - przełącznik rejestrów        │
│ ALU          │ Jednostka arytmetyczno-logiczna            │
│ R0-R3        │ Rejestry uniwersalne (dane)                │
└──────────────┴─────────────────────────────────────────────┘

CYKL ROZKAZOWY:
1. FETCH   → PC → Code Memory → IR
2. DECODE  → Decoder → M0/M1/M2 → MUX
3. EXECUTE → ALU → Wynik → Rejestr
```

**ZAPAMIĘTAJ:**
- RISC = operacje tylko na rejestrach
- Decoder = logika kombinacyjna (nie rejestr!)
- MUX = selektor/przełącznik rejestrów
- Pipeline = wykonywanie równoległe etapów
- ARM = 3 operandy (wyjątek)
- Cykl 3-fazowy: FETCH → DECODE → EXECUTE
- PC automatycznie += 1 (lub skok)
- IR przechowuje instrukcję w kodzie maszynowym
- Zapadki (enable) sterują zapisem do rejestrów

---

**Źródło:** Wykład "Architektura Systemów Komputerowych" - projektowanie procesora RISC
