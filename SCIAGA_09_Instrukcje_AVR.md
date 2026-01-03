# Ściąga 07: Instrukcje AVR (ATmega)

---

## 1. PODSTAWOWE INSTRUKCJE ARYTMETYCZNE

### ADD (Addition):
```assembly
ADD Rd, Rr    ; Rd = Rd + Rr
```
- Dodaje dwa rejestry
- Aktualizuje flagi: **C, Z, V, N, H, S**
- Przykład: `ADD R1, R2` → R1 = R1 + R2

### SUB (Subtraction):
```assembly
SUB Rd, Rr    ; Rd = Rd - Rr
```
- Odejmuje rejestry
- Aktualizuje flagi: **C, Z, V, N, H, S**
- Przykład: `SUB R3, R4` → R3 = R3 - R4

---

## 2. INKREMENTACJA I DEKREMENTACJA

### INC (Increment):
```assembly
INC Rd        ; Rd = Rd + 1
```
- Zwiększa rejestr o 1
- Aktualizuje: **Z, V, N, S** (NIE aktualizuje C!)
- Szybsza niż `ADD Rd, 1`

### DEC (Decrement):
```assembly
DEC Rd        ; Rd = Rd - 1
```
- Zmniejsza rejestr o 1
- Aktualizuje: **Z, V, N, S** (NIE aktualizuje C!)
- Szybsza niż `SUB Rd, 1`

**WAŻNE:** INC/DEC nie zmieniają Carry!

---

## 3. MNOŻENIE

### MUL (Multiply Unsigned):
```assembly
MUL Rd, Rr    ; R1:R0 = Rd × Rr (unsigned)
```
- Mnoży dwie liczby **bez znaku**
- Wynik 16-bit w **R1:R0**
- Aktualizuje: **C, Z**

### MULS (Multiply Signed):
```assembly
MULS Rd, Rr   ; R1:R0 = Rd × Rr (signed)
```
- Mnoży liczby **ze znakiem** (U2)
- Wynik 16-bit w **R1:R0**
- Aktualizuje: **C, Z**

### MULSU (Multiply Signed × Unsigned):
```assembly
MULSU Rd, Rr  ; R1:R0 = Rd(signed) × Rr(unsigned)
```
- Rd ze znakiem, Rr bez znaku
- Rzadko używane

---

## 4. PORÓWNANIA

### CP (Compare):
```assembly
CP Rd, Rr     ; Rd - Rr (tylko flagi!)
```
- Odejmuje, ale **NIE zapisuje wyniku**
- Aktualizuje wszystkie flagi
- Używane przed skokami warunkowymi

### CPI (Compare with Immediate):
```assembly
CPI Rd, K     ; Rd - K (tylko flagi!)
```
- Porównuje rejestr ze stałą
- **Tylko R16-R31** (ograniczenie!)
- Aktualizuje wszystkie flagi

**Różnica CP vs SUB:**
- CP: tylko flagi, rejestr niezmieniony
- SUB: flagi + zmienia rejestr

---

## 5. SKOKI BEZWARUNKOWE

### RJMP (Relative Jump):
```assembly
RJMP label    ; PC = PC + offset
```
- Skok **względny** (offset ±2K)
- Szybki (1 cykl)
- Używany w pętlach lokalnych

### JMP (Jump):
```assembly
JMP addr      ; PC = addr
```
- Skok **bezwzględny** (cała pamięć)
- Wolniejszy (3 cykle)
- Używany do odległych skoków

### IJMP (Indirect Jump):
```assembly
IJMP          ; PC = Z (R31:R30)
```
- Skok do adresu w rejestrze Z
- Dynamiczne skoki (tablice skoków)

---

## 6. SKOKI WARUNKOWE (BRANCH)

### BREQ (Branch if Equal):
```assembly
BREQ label    ; Jeśli Z=1, skocz
```
- Sprawdza flagę **Z** (Zero)
- Używane po CP/CPI

### BRNE (Branch if Not Equal):
```assembly
BRNE label    ; Jeśli Z=0, skocz
```
- Sprawdza flagę **Z**
- Odwrotność BREQ

### BRLO (Branch if Lower):
```assembly
BRLO label    ; Jeśli C=1, skocz (unsigned)
```
- Sprawdza flagę **C** (Carry)
- Dla liczb bez znaku: A < B

### BRLT (Branch if Less Than):
```assembly
BRLT label    ; Jeśli S=1, skocz (signed)
```
- Sprawdza flagę **S** (Sign)
- Dla liczb ze znakiem: A < B

### Inne BRANCH:
- **BRGE** (Greater or Equal) - S=0
- **BRSH** (Same or Higher) - C=0
- **BRMI** (Minus) - N=1
- **BRPL** (Plus) - N=0

---

## 7. WYWOŁANIA FUNKCJI

### CALL (Call Subroutine):
```assembly
CALL addr     ; Push PC, PC=addr
```
- Zapisuje PC na stosie
- Skacze do funkcji
- Używane do podprogramów

### RET (Return):
```assembly
RET           ; Pop PC
```
- Pobiera PC ze stosu
- Wraca z funkcji
- Zawsze używane na końcu CALL

### RETI (Return from Interrupt):
```assembly
RETI          ; Pop PC + I=1
```
- Pobiera PC ze stosu
- Włącza przerwania (I=1)
- **Tylko w obsłudze przerwań!**

**WAŻNE:** RETI ≠ RET (różnica: flaga I)

---

## 8. OPERACJE LOGICZNE

### AND (Logical AND):
```assembly
AND Rd, Rr    ; Rd = Rd AND Rr
```
- Iloczy logiczny (bit po bicie)
- Aktualizuje: **Z, V, N, S**

### OR (Logical OR):
```assembly
OR Rd, Rr     ; Rd = Rd OR Rr
```
- Suma logiczna
- Aktualizuje: **Z, V, N, S**

### EOR (Exclusive OR):
```assembly
EOR Rd, Rr    ; Rd = Rd XOR Rr
```
- XOR (różnica symetryczna)
- Trick: `EOR R1, R1` → wyzerowanie R1

---

## 9. PRZESUNIĘCIA BITOWE

### LSL (Logical Shift Left):
```assembly
LSL Rd        ; Rd = Rd << 1 (mnożenie ×2)
```
- Przesunięcie w lewo
- MSB → Carry, LSB ← 0

### LSR (Logical Shift Right):
```assembly
LSR Rd        ; Rd = Rd >> 1 (dzielenie ÷2)
```
- Przesunięcie w prawo
- LSB → Carry, MSB ← 0

### ROL/ROR (Rotate):
- **ROL** (Left) - rotacja z Carry
- **ROR** (Right) - rotacja z Carry

---

## 10. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Różnica między ADD a INC?
**A:** INC nie aktualizuje Carry, ADD tak. INC szybsze.

### Q: Która instrukcja nie zmienia rejestru?
**A:** CP (Compare) - tylko aktualizuje flagi.

### Q: Jakie są 3 instrukcje mnożenia?
**A:** MUL (unsigned), MULS (signed), MULSU (mixed).

### Q: Gdzie zapisywany jest wynik mnożenia?
**A:** W R1:R0 (16-bit).

### Q: Różnica między BREQ a BRNE?
**A:** BREQ skacze gdy Z=1 (równe), BRNE gdy Z=0 (nierówne).

### Q: Różnica między RET a RETI?
**A:** RETI dodatkowo ustawia flagę I=1 (przerwania).

---

## 11. SZYBKA ŚCIĄGA - TABELA

```
┌─────────────┬────────────────┬──────────────────┐
│  INSTRUKCJA │   OPERACJA     │      FLAGI       │
├─────────────┼────────────────┼──────────────────┤
│     ADD     │   Rd + Rr      │  C, Z, V, N, H, S│
│     SUB     │   Rd - Rr      │  C, Z, V, N, H, S│
│     INC     │   Rd + 1       │  Z, V, N, S (¬C!)│
│     DEC     │   Rd - 1       │  Z, V, N, S (¬C!)│
│     MUL     │   Rd × Rr      │  C, Z            │
│      CP     │   Rd - Rr      │  C, Z, V, N, H, S│
│    BREQ     │  Skok Z=1      │  -               │
│    BRNE     │  Skok Z=0      │  -               │
│     RET     │  Powrót        │  -               │
│    RETI     │  Powrót + I=1  │  I               │
└─────────────┴────────────────┴──────────────────┘
```

**ZAPAMIĘTAJ:**
- INC/DEC nie zmieniają Carry!
- MUL → wynik w R1:R0
- CP = SUB bez zapisu
- RETI ≠ RET (flaga I)

