# Ściąga 05: Rejestry i Cykl Rozkazowy

---

## 1. REJESTRY - PODSTAWY

### Definicja:
**Rejestr** = ultraszybka pamięć wewnątrz procesora

### Charakterystyka:
```
Szybkość:  Rejestr >> Cache >> RAM >> Dysk
Dostęp:    0 cykli (natychmiastowy)
Rozmiar:   8-bit, 16-bit, 32-bit, 64-bit
```

### Liczba rejestrów:
- **AVR (ATmega):** R0-R31 (32 rejestry × 8-bit)
- **ARM:** R0-R15 (16 rejestrów × 32-bit)
- **Intel x86:** AX, BX, CX, DX, ... (ograniczona liczba)

---

## 2. REJESTRY SPECJALNE

### Program Counter (PC):
```
Wskazuje adres NASTĘPNEJ instrukcji do wykonania
```
- **Automatyczna inkrementacja** po każdej instrukcji
- Skok (JUMP) = zmiana wartości PC
- Przykład: PC=0x0100 → wykonaj instrukcję → PC=0x0101

### Instruction Register (IR):
```
Przechowuje AKTUALNIE WYKONYWANĄ instrukcję
```
- Pobrana z pamięci (FETCH)
- Dekodowana przez Decoder
- Nie ma bezpośredniego dostępu programisty

### Status Register (SREG):
```
Przechowuje FLAGI procesora
```
- AVR: I T H S V N Z C (8 flag)
- Aktualizowane po każdej operacji arytmetycznej

---

## 3. CYKL ROZKAZOWY (3 ETAPY)

### Schemat:
```
┌─────────┐     ┌─────────┐     ┌─────────┐
│  FETCH  │ ──→ │ DECODE  │ ──→ │ EXECUTE │
└─────────┘     └─────────┘     └─────────┘
    ↓                                 ↓
   PC++                          Wynik → Rejestr
```

### 1. FETCH (Pobieranie):
```
1. Odczytaj adres z PC
2. Pobierz instrukcję z Code Memory[PC]
3. Zapisz instrukcję do IR
4. Inkrementuj PC (PC++)
```

### 2. DECODE (Dekodowanie):
```
1. Decoder analizuje IR
2. Identyfikuje operację (ADD, SUB, ...)
3. Identyfikuje operandy (R1, R2, ...)
4. Przygotowuje sygnały sterujące
```

### 3. EXECUTE (Wykonanie):
```
1. ALU wykonuje operację
2. Wynik zapisywany do rejestru docelowego
3. Aktualizacja flag (C, Z, V, N, ...)
```

---

## 4. PRZYKŁAD WYKONANIA INSTRUKCJI

### Instrukcja: `ADD R1, R2, R3` (R1 = R2 + R3)

```
FETCH:
- PC = 0x0100
- IR = Code Memory[0x0100] = 0b0001001001010011
- PC = PC + 1 = 0x0101

DECODE:
- Dekoder: opcode = 0001 → ADD
- Operand 1: R2 (źródło)
- Operand 2: R3 (źródło)
- Cel: R1 (wynik)

EXECUTE:
- ALU: R2 + R3 = 5 + 7 = 12
- R1 = 12
- Flagi: Z=0, C=0, V=0, N=0
```

---

## 5. PIPELINING (POTOKOWANIE)

### Idea:
```
Równoległe wykonywanie różnych etapów dla różnych instrukcji
```

### Bez pipeliningu:
```
Cykl 1: [FETCH instr1] [      ] [       ]
Cykl 2: [      ] [DECODE instr1] [       ]
Cykl 3: [      ] [      ] [EXECUTE instr1]
Cykl 4: [FETCH instr2] [      ] [       ]
...
Czas na 3 instrukcje: 9 cykli
```

### Z pipeliningiem:
```
Cykl 1: [FETCH instr1] [      ] [       ]
Cykl 2: [FETCH instr2] [DECODE instr1] [       ]
Cykl 3: [FETCH instr3] [DECODE instr2] [EXECUTE instr1]
Cykl 4: [FETCH instr4] [DECODE instr3] [EXECUTE instr2]
...
Czas na 3 instrukcje: 5 cykli (po wypełnieniu potoku: 1 cykl/instr!)
```

---

## 6. REJESTRY W AVR (ATmega)

### Bank rejestrów:
```
R0  - R31 (32 rejestry ogólnego przeznaczenia)
```

### Rejestry specjalne:
```
R26:R27 = X (rejestr wskaźnikowy)
R28:R29 = Y (rejestr wskaźnikowy)
R30:R31 = Z (rejestr wskaźnikowy)
```

### Przykład użycia Z:
```assembly
LDI  R30, LOW(addr)   ; Młodszy bajt adresu → R30
LDI  R31, HIGH(addr)  ; Starszy bajt adresu → R31
LD   R1, Z            ; Załaduj [Z] → R1
```

---

## 7. ALU (Arithmetic Logic Unit)

### Zadania ALU:
```
1. Operacje arytmetyczne (ADD, SUB, MUL, DIV)
2. Operacje logiczne (AND, OR, XOR, NOT)
3. Przesunięcia bitowe (LSL, LSR, ROL, ROR)
4. Porównania (CP, CPI)
```

### Schemat:
```
┌────────────────────┐
│       ALU          │
│  ┌──────────────┐  │
│  │   Operacja   │  │
│  └──────────────┘  │
│         ↓          │
│  ┌──────────────┐  │
│  │    Wynik     │  │ → Rejestr docelowy
│  └──────────────┘  │
│         ↓          │
│  ┌──────────────┐  │
│  │    Flagi     │  │ → SREG (C, Z, V, N)
│  └──────────────┘  │
└────────────────────┘
```

---

## 8. DECODER (DEKODER INSTRUKCJI)

### Zadanie:
```
Zamienia kod binarny instrukcji na sygnały sterujące
```

### Przykład:
```
Instrukcja binarna: 0b0001001001010011
                      ↓
                  DECODER
                      ↓
Sygnały:
- ALU_OP = ADD
- SRC1 = R2
- SRC2 = R3
- DEST = R1
- WRITE_ENABLE = 1
```

### Logika:
- **Opcode** (pierwsze bity) → rodzaj operacji
- **Operandy** (kolejne bity) → numery rejestrów

---

## 9. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Co to jest rejestr?
**A:** Ultraszybka pamięć wewnątrz procesora (dostęp: 0 cykli).

### Q: Co to jest Program Counter (PC)?
**A:** Rejestr wskazujący adres następnej instrukcji do wykonania.

### Q: Co to jest Instruction Register (IR)?
**A:** Rejestr przechowujący aktualnie wykonywaną instrukcję.

### Q: Jakie są 3 etapy cyklu rozkazowego?
**A:** FETCH (pobieranie), DECODE (dekodowanie), EXECUTE (wykonanie).

### Q: Co to jest pipelining?
**A:** Równoległe wykonywanie różnych etapów dla różnych instrukcji (przyspieszenie).

---

## 10. SZYBKA ŚCIĄGA - TABELA

```
┌─────────────┬──────────────────────────────────┐
│   REJESTR   │          ZASTOSOWANIE             │
├─────────────┼──────────────────────────────────┤
│     PC      │  Program Counter (następna instr)│
│     IR      │  Instruction Register (aktualna) │
│    SREG     │  Status Register (flagi C/Z/V/N) │
│   R0-R31    │  Rejestry ogólnego przeznaczenia │
│  X/Y/Z      │  Rejestry wskaźnikowe (AVR)      │
└─────────────┴──────────────────────────────────┘

┌─────────────┬──────────────────────────────────┐
│    ETAP     │           CZYNNOŚCI              │
├─────────────┼──────────────────────────────────┤
│   FETCH     │  Pobierz instr[PC] → IR, PC++    │
│   DECODE    │  Dekoduj IR → sygnały sterujące  │
│   EXECUTE   │  ALU wykonuje, wynik → rejestr   │
└─────────────┴──────────────────────────────────┘
```

**ZAPAMIĘTAJ:**
- PC = adres **następnej** instrukcji
- IR = **aktualna** instrukcja
- Cykl: FETCH → DECODE → EXECUTE
- Pipelining = równoległość = szybkość

