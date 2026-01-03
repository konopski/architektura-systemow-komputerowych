# Ściąga 03: RISC vs CISC

---

## 1. PODSTAWOWE DEFINICJE

### RISC (Reduced Instruction Set Computer):
```
Operacje TYLKO na rejestrach lub stałych w kodzie
```

**Charakterystyka:**
- Proste instrukcje
- Wszystkie operacje na rejestrach
- Dostęp do pamięci tylko przez LOAD/STORE
- Szybkie wykonanie pojedynczej instrukcji

### CISC (Complex Instruction Set Computer):
```
Operacje bezpośrednio na pamięci
```

**Charakterystyka:**
- Złożone instrukcje
- Operacje mogą pracować bezpośrednio na pamięci
- Zaciąga zmienną z pamięci, operuje, zapisuje
- Jedna instrukcja = wiele operacji

---

## 2. PRZYKŁAD - DODAWANIE

### RISC (np. ARM, AVR):
```assembly
LOAD  R1, [addr1]    ; Załaduj zmienną z pamięci do R1
LOAD  R2, [addr2]    ; Załaduj zmienną z pamięci do R2
ADD   R3, R1, R2     ; Dodaj R1 + R2 → wynik w R3
STORE R3, [addr3]    ; Zapisz wynik z R3 do pamięci
```
**4 instrukcje**

### CISC (np. Intel x86):
```assembly
ADD [addr3], [addr1]    ; Dodaj pamięć+pamięć → pamięć
```
**1 instrukcja**

---

## 3. BŁĘDNE ROZRÓŻNIENIE ❌

### Powszechny błąd:
```
❌ RISC = proste instrukcje
❌ CISC = złożone instrukcje
```

**Dlaczego to błąd?**
- ARM ma bardzo złożone instrukcje!
- Przykład: instrukcja ARM może zawierać:
  - Operację arytmetyczną
  - Przesunięcie bitowe
  - Warunkowe wykonanie

---

## 4. PRAWDZIWE ROZRÓŻNIENIE ✅

### Klucz: **Gdzie wykonywane są operacje**

| Architektura | Operacje na... |
|--------------|----------------|
| **RISC** | Rejestrach (R0-R31) |
| **CISC** | Pamięci (bezpośrednio) |

### RISC:
```
1. LOAD R1, [pamięć]    ← Załaduj do rejestru
2. Operacje na R1, R2, R3...  ← Wszystko na rejestrach
3. STORE R1, [pamięć]   ← Zapisz z rejestru
```

### CISC:
```
1. ADD [pamięć], [pamięć]  ← Operacja bezpośrednio na pamięci
```

---

## 5. DLACZEGO RISC JEST SZYBSZY?

### CISC wydaje się szybszy:
```
1 instrukcja = 1 cykl?  ← Nie!
```

### Rzeczywistość:
```
CISC: 1 instrukcja = wiele cykli (dostęp do pamięci!)
RISC: 1 instrukcja = 1 cykl (operacje na rejestrach)
```

### Dodatkowo RISC:
✅ **Łatwy pipelining** - proste instrukcje → równoległe wykonanie
✅ **Mniejszy procesor** - prostsze instrukcje → mniej tranzystorów
✅ **Szybszy zegar** - mniej logiki → wyższe częstotliwości

### Wynik:
```
16-rdzeniowy ARM >> Intel (w praktyce)
ARM "zmiata Intela na śniadanie"
```

---

## 6. PORÓWNANIE BEZPOŚREDNIE

| Cecha | RISC | CISC |
|-------|------|------|
| **Operacje** | Rejestry | Pamięć |
| **Liczba instrukcji** | Więcej | Mniej |
| **Złożoność instrukcji** | Prosta | Złożona |
| **Czas wykonania** | 1 cykl | Wiele cykli |
| **Rozmiar procesora** | Mniejszy | Większy |
| **Pipelining** | Łatwy | Trudny |
| **Energooszczędność** | Lepsza | Gorsza |

---

## 7. PRZYKŁADY PROCESORÓW

### RISC:
- **ARM** (smartfony, tablety, Apple M1/M2)
- **ATmega** (AVR, Arduino)
- **RISC-V** (open-source, nowa generacja)
- **MIPS** (routery, konsole)

### CISC:
- **Intel x86** (PC, serwery)
- **Intel x86-64** (64-bitowe PC)
- **Motorola 68k** (stare Atari, Amiga, Commodore)

---

## 8. AMD - HYBRYDOWE PODEJŚCIE

### Problem AMD:
```
Chcemy: szybkość RISC
Potrzebujemy: kompatybilność z Intelem (CISC)
```

### Rozwiązanie:
```
┌──────────────────────────┐
│    Interfejs CISC        │ ← Kompatybilność
├──────────────────────────┤
│    Mikrokod (interpreter)│ ← Tłumaczenie
├──────────────────────────┤
│    RISC wewnątrz         │ ← Szybkość!
└──────────────────────────┘
```

**Jak to działa:**
1. Instrukcja CISC wchodzi
2. Mikrokod tłumaczy na instrukcje RISC-owe
3. Procesor wykonuje RISC-owo (szybko!)
4. Wynik zwracany jako CISC

### Wynik:
✅ **Kompatybilność** - działa z Intelem
✅ **Szybkość** - RISC wewnątrz
✅ **Sukces** - AMD wygrywa w grach!

---

## 9. HISTORIA RISC-V

### Geneza:
```
Profesor + studenci na uniwersytecie
Każdy rok → kolejna wersja (I, II, III, IV...)
Wersja V → komercjalizacja
```

### Dlaczego "V" (pięć)?
- RISC I, II, III, IV były eksperymentalne
- RISC V została skomercjalizowana
- Stąd nazwa: **RISC-V** (piąta wersja)

### Zalety RISC-V:
✅ **Open-source** - darmowa licencja
✅ **Modułowa** - wybierasz instrukcje
✅ **Nowoczesna** - uczy się na błędach ARM/MIPS

---

## 10. KIEDY STOSOWAĆ KTÓRĄ?

### RISC - najlepszy dla:
- ✅ **Urządzeń mobilnych** (smartfony, tablety)
- ✅ **Systemów embedded** (mikrokontrolery)
- ✅ **Energooszczędności** (baterie)
- ✅ **Wielordzeniowości** (łatwe skalowanie)
- ✅ **Aplikacji realtime** (przewidywalność)

### CISC - najlepszy dla:
- ✅ **Kompatybilności** (stary kod x86)
- ✅ **PC i serwerów** (ekosystem Windows)
- ✅ **Gęstości kodu** (mniej instrukcji = mniejszy plik)

### Hybrydy (AMD) - najlepsze dla:
- ✅ **Gier** (szybkość + kompatybilność)
- ✅ **Workstation** (wydajność RISC, ekosystem x86)

---

## 11. ARM vs INTEL - PORÓWNANIE ROZMIARU

### Fakty:
```
Intel x86: ~50× większy od ARM (liczba tranzystorów)
```

**Dlaczego?**
- CISC wymaga skomplikowanego dekodera
- Mikrokod zajmuje miejsce
- Kompatybilność wsteczna = martwy kod

**Konsekwencje:**
- ARM: mniejszy → tańszy → mniej energii
- Intel: większy → droższy → więcej ciepła

### W praktyce:
```
16-rdzeniowy ARM >> 8-rdzeniowy Intel
(przy tym samym poborze mocy!)
```

---

## 12. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Jaka jest główna różnica między RISC a CISC?
**A:** RISC operuje na rejestrach (LOAD/STORE), CISC operuje bezpośrednio na pamięci.

### Q: Która architektura jest szybsza?
**A:** RISC - bo proste instrukcje = łatwy pipelining + szybkie wykonanie.

### Q: Podaj przykłady każdej architektury.
**A:** RISC: ARM, ATmega, RISC-V; CISC: Intel x86.

### Q: Jak AMD rozwiązało problem RISC vs CISC?
**A:** RISC wewnątrz (szybkość) + CISC interfejs (kompatybilność) + mikrokod (tłumaczenie).

### Q: Dlaczego RISC-V ma "V" w nazwie?
**A:** To piąta (V) wersja projektu uniwersyteckiego, pierwsza skomercjalizowana.

---

## 13. PRZYKŁAD KODU - SZCZEGÓŁOWO

### Zadanie: Dodaj dwie liczby z pamięci

#### RISC (ARM):
```assembly
LDR  R1, =addr1      ; Załaduj adres addr1 do R1
LDR  R1, [R1]        ; Załaduj wartość z [addr1] do R1
LDR  R2, =addr2      ; Załaduj adres addr2 do R2
LDR  R2, [R2]        ; Załaduj wartość z [addr2] do R2
ADD  R3, R1, R2      ; Dodaj R1 + R2 → R3
LDR  R4, =addr3      ; Załaduj adres addr3 do R4
STR  R3, [R4]        ; Zapisz R3 do [addr3]
```
**7 instrukcji, ale każda szybka (1 cykl dla ADD)**

#### CISC (Intel x86):
```assembly
MOV AX, [addr1]      ; Załaduj [addr1] do AX
ADD AX, [addr2]      ; Dodaj [addr2] do AX
MOV [addr3], AX      ; Zapisz AX do [addr3]
```
**3 instrukcje, ale wolniejsze (dostęp do pamięci)**

#### Porównanie czasu:
```
RISC: 7 instrukcji × 1 cykl = 7 cykli (+ pipelining!)
CISC: 3 instrukcje × 3-5 cykli = 9-15 cykli
```

**RISC wygrywa!**

---

## 14. SZYBKA ŚCIĄGA - WZORY

### Test na RISC:
```
Czy instrukcja może operować bezpośrednio na pamięci?
  NIE → RISC
  TAK → CISC
```

### Test na szybkość:
```
RISC: proste instrukcje → pipelining → szybko
CISC: złożone instrukcje → trudny pipelining → wolno
```

---

## 15. TYPOWE PUŁAPKI

❌ **Błąd 1:** "RISC ma proste instrukcje, CISC złożone"
→ ARM ma bardzo złożone instrukcje! To nie o to chodzi.

❌ **Błąd 2:** "CISC jest szybszy, bo mniej instrukcji"
→ Liczba instrukcji ≠ szybkość. Liczy się czas wykonania!

❌ **Błąd 3:** "Intel to CISC, więc wolny"
→ Intel też ma RISC wewnątrz (mikrokod), ale zewnętrznie CISC dla kompatybilności.

❌ **Błąd 4:** "RISC-V to pięć instrukcji"
→ "V" to rzymska piątka, nie liczba instrukcji!

---

**KLUCZOWE DO ZAPAMIĘTANIA:**
1. **RISC** = operacje na rejestrach (LOAD/STORE)
2. **CISC** = operacje bezpośrednio na pamięci
3. **RISC szybszy** dzięki pipelining + proste instrukcje
4. **AMD** = RISC wewnątrz, CISC interfejs (mikrokod)
5. **Przykłady:** ARM/RISC-V (RISC), Intel x86 (CISC)
