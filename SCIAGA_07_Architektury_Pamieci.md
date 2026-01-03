# Ściąga 02: Architektury Pamięci (von Neumann vs Harvard)

---

## 1. ARCHITEKTURA VON NEUMANNA

### Schemat:
```
         ┌──────────────┐
         │   PROCESOR   │
         │  ┌────────┐  │
         │  │  CPU   │  │
         │  └────────┘  │
         └───────┬──────┘
                 │
        ┌────────┴────────┐
        │  MAGISTRALA     │
        │  (wspólna)      │
        └────────┬────────┘
                 │
         ┌───────┴───────┐
         │    PAMIĘĆ     │
         │ ┌───────────┐ │
         │ │   CODE    │ │
         │ │    +      │ │
         │ │   DATA    │ │
         │ └───────────┘ │
         └───────────────┘
```

### Cechy:
- **Jedna magistrala** dla kodu i danych
- **Jedna pamięć** wspólna
- Kod i dane w tej samej przestrzeni adresowej

### ✅ Zalety:
1. **Tańsza** - tylko jedna pamięć
2. **Prostsza** - mniej połączeń
3. **Elastyczna** - kod może się zmieniać w pamięci
4. **Kompatybilność** - łatwa wymiana pamięci

### ❌ Wady:
1. **Bottleneck** - wąskie gardło (jedna magistrala)
2. **Wolniejsza** - nie można jednocześnie pobierać kodu i danych
3. **Niebezpieczna** - można nadpisać kod danymi! (katastrofa)
4. **Trudniejszy pipelining** - nie da się robić Fetch i Execute jednocześnie

### Przykłady procesorów:
- **Wczesne komputery** (pierwotna koncepcja)
- **Współczesne PC** (zewnętrznie von Neumann)

---

## 2. ARCHITEKTURA HARVARD

### Schemat:
```
         ┌──────────────────┐
         │    PROCESOR      │
         │   ┌────────┐     │
         │   │  CPU   │     │
         │   └───┬─┬──┘     │
         └───────┼─┼────────┘
                 │ │
      ┌──────────┘ └──────────┐
      │                       │
 ┌────┴─────┐          ┌─────┴────┐
 │ MAGISTR. │          │ MAGISTR. │
 │   CODE   │          │   DATA   │
 └────┬─────┘          └─────┬────┘
      │                      │
 ┌────┴─────┐          ┌─────┴────┐
 │  CODE    │          │   DATA   │
 │  MEMORY  │          │  MEMORY  │
 └──────────┘          └──────────┘
```

### Cechy:
- **Dwie osobne magistrale**
- **Dwie osobne pamięci**
- Całkowite rozdzielenie kodu i danych

### ✅ Zalety:
1. **Szybsza** - równoległe pobieranie kodu i danych
2. **Bezpieczna** - NIE DA SIĘ nadpisać kodu danymi
3. **Łatwiejszy pipelining** - Fetch i Execute równolegle
4. **Bardziej przewidywalna** - deterministyczne czasy dostępu

### ❌ Wady:
1. **Droższa** - dwie pamięci
2. **Więcej połączeń** - bardziej skomplikowana
3. **Mniej elastyczna** - kod nie może się zmieniać
4. **Trudniejsza do zaprogramowania** - trzeba zarządzać dwiema pamięciami

### Przykłady procesorów:
- **ATmega** (AVR)
- **DSP** (Digital Signal Processors)
- **Mikrokontrolery embedded**

---

## 3. PORÓWNANIE BEZPOŚREDNIE

| Cecha | von Neumann | Harvard |
|-------|-------------|---------|
| **Magistrale** | 1 wspólna | 2 osobne |
| **Pamięci** | 1 wspólna | 2 osobne |
| **Szybkość** | Wolniejsza | Szybsza |
| **Bezpieczeństwo** | Można nadpisać kod | Kod chroniony |
| **Koszt** | Tańsza | Droższa |
| **Pipelining** | Trudniejszy | Łatwiejszy |
| **Elastyczność** | Większa | Mniejsza |

---

## 4. HYBRYDY (Najczęściej spotykane!)

### a) RISC-V: Harvard wewnątrz, von Neumann zewnątrz
```
┌─────────────────────────────────┐
│         PROCESOR RISC-V          │
│  ┌─────────────────────────┐    │
│  │   Harvard wewnątrz:     │    │
│  │   - Osobne cache I/D    │    │
│  │   - Szybki pipelining   │    │
│  └──────────┬──────────────┘    │
└─────────────┼───────────────────┘
              │ von Neumann
         ┌────┴─────┐
         │  RAM     │
         │ (wspólna)│
         └──────────┘
```

**Dlaczego?**
- Wewnątrz: szybkość (Harvard)
- Zewnątrz: kompatybilność (von Neumann)

### b) ARM: von Neumann wewnątrz, Harvard zewnątrz
```
┌─────────────────────────────────┐
│           PROCESOR ARM           │
│  ┌─────────────────────────┐    │
│  │  von Neumann wewnątrz   │    │
│  │  - Wspólna magistrala   │    │
│  └──────────┬───┬──────────┘    │
└─────────────┼───┼───────────────┘
              │   │ Harvard
         ┌────┘   └────┐
    ┌────┴────┐   ┌────┴────┐
    │ CODE    │   │  DATA   │
    │ Memory  │   │ Memory  │
    └─────────┘   └─────────┘
```

**Dlaczego?**
- Projektant może ustawić: kod/dane/peryferia
- 2-3 kontrolery zarządzają dostępem
- Elastyczność w konfiguracji

### c) Współczesne PC
```
┌──────────────────┐
│       CPU        │
│  ┌──────────┐    │
│  │ L1 Cache │    │ ← Harvard (osobne I/D)
│  │ I-Cache  │    │
│  │ D-Cache  │    │
│  └────┬─────┘    │
│  ┌────┴─────┐    │
│  │ L2 Cache │    │ ← von Neumann (wspólna)
│  └────┬─────┘    │
└───────┼──────────┘
        │
   ┌────┴────┐
   │   RAM   │         ← von Neumann (wspólna)
   └─────────┘
```

---

## 5. CODE MEMORY vs DATA MEMORY

### Code Memory (pamięć kodu):
```c
for(i=0; i<5; i++) {  // ← To jest KOD
    x = x + 1;        // ← To jest KOD
}
```
- Przechowuje **instrukcje** programu
- W Harvard: osobna pamięć
- Zazwyczaj **Flash** (nieulotna)

### Data Memory (pamięć danych):
```c
int i;      // ← To jest DEKLARACJA (dla kompilatora)
int x = 10; // ← x=10 to DANE w pamięci

// Kompilator rezerwuje:
// - i: 1 bajt (int8) lub 4 bajty (int32)
// - x: 1 bajt (int8) lub 4 bajty (int32)
```
- Przechowuje **zmienne** programu
- W Harvard: osobna pamięć
- Zazwyczaj **RAM** (ulotna)

### Przykład ATmega (Harvard):
```
Code Memory (Flash): 32 KB
  ├─ Adres 0x0000 - 0x7FFF
  └─ Instrukcje programu

Data Memory (SRAM): 2 KB
  ├─ Adres 0x0000 - 0x07FF
  └─ Zmienne, stos
```

**Ważne:** W Harvard te przestrzenie się NIE POKRYWAJĄ!

---

## 6. NADPISANIE KODU - PRZYKŁAD PROBLEMU

### W von Neumann (MOŻLIWE):
```c
int* ptr = (int*)0x1000;  // Wskaźnik na kod
*ptr = 0xDEADBEEF;        // NADPISANIE KODU! 💀
// Procesor może się zawiesić lub wykonać losowe instrukcje
```

### W Harvard (NIEMOŻLIWE):
```c
int* ptr = (int*)0x1000;  // Wskaźnik na DANE
*ptr = 0xDEADBEEF;        // Nadpisanie danych - OK

// Kod jest w OSOBNEJ pamięci
// Nie da się go nadpisać wskaźnikiem do danych!
```

---

## 7. PIPELINING - DLACZEGO HARVARD JEST LEPSZA?

### von Neumann (problem):
```
Cykl 1: FETCH instrukcji      ← Magistrala zajęta
Cykl 2: DECODE instrukcji
Cykl 3: EXECUTE (czytanie z RAM) ← Magistrala zajęta
                                  (nie można robić FETCH!)
```
**Bottleneck:** Jedna magistrala = konflikt dostępu

### Harvard (brak problemu):
```
Cykl 1: FETCH instr.   (magistrala CODE)
        ↓
Cykl 2: DECODE instr.
        ↓
Cykl 3: EXECUTE + czytanie (magistrala DATA)
        + FETCH kolejnej instr. (magistrala CODE) ← Równolegle!
```
**Brak konfliktu:** Dwie magistrale = równoległy dostęp

---

## 8. KIEDY STOSOWAĆ KTÓRĄ?

### von Neumann - najlepsza dla:
- ✅ Komputerów PC (elastyczność, kompatybilność)
- ✅ Systemów z dynamicznym kodem (JIT, interpretery)
- ✅ Tanich rozwiązań
- ✅ Dużej ilości RAM

### Harvard - najlepsza dla:
- ✅ Mikrokontrolerów (szybkość, bezpieczeństwo)
- ✅ DSP (przetwarzanie sygnałów)
- ✅ Systemów embedded (deterministyczność)
- ✅ Aplikacji realtime

### Hybrydy - najlepsza dla:
- ✅ Procesorów ARM (smartfony, tablety)
- ✅ RISC-V (nowe zastosowania)
- ✅ Współczesnych CPU (cache Harvard, RAM von Neumann)

---

## 9. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Jaka jest główna różnica?
**A:** von Neumann ma wspólną magistralę i pamięć dla kodu i danych, Harvard ma osobne.

### Q: Która jest szybsza?
**A:** Harvard - bo może robić Fetch i Execute równolegle.

### Q: Która jest bezpieczniejsza?
**A:** Harvard - bo nie można nadpisać kodu danymi.

### Q: Która jest tańsza?
**A:** von Neumann - bo wymaga tylko jednej pamięci.

### Q: Podaj przykład każdej.
**A:** von Neumann: PC, Harvard: ATmega, Hybryda: ARM/RISC-V

---

## 10. SZYBKA ŚCIĄGA - TABELA

```
┌───────────────┬─────────────┬─────────────┐
│     CECHA     │ von Neumann │   Harvard   │
├───────────────┼─────────────┼─────────────┤
│ Magistrala    │      1      │      2      │
│ Pamięć        │      1      │      2      │
│ Szybkość      │      ↓      │      ↑      │
│ Bezpieczeństwo│      ↓      │      ↑      │
│ Koszt         │      ↓      │      ↑      │
│ Pipelining    │   trudny    │    łatwy    │
│ Przykład      │     PC      │   ATmega    │
└───────────────┴─────────────┴─────────────┘
```

**ZAPAMIĘTAJ:**
- von Neumann = 1 magistrala = prosto/tanio/wolno
- Harvard = 2 magistrale = szybko/bezpiecznie/drogo
- Hybrydy = łączą zalety obu!
