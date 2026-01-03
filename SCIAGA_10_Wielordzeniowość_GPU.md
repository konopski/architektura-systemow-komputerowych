# Ściąga 09: Wielordzeniowość, GPU i Maszyna Turinga

---

## 1. WIELORDZENIOWOŚĆ - PODSTAWY

### Definicja:
**Wielordzeniowość** = wiele niezależnych jednostek wykonawczych (rdzeni) w jednym procesorze

### Schemat:
```
┌─────────────────────────┐
│      PROCESOR           │
│  ┌──────┐    ┌──────┐   │
│  │ RDZEŃ│    │ RDZEŃ│   │
│  │  1   │    │  2   │   │
│  └──────┘    └──────┘   │
│  ┌──────┐    ┌──────┐   │
│  │ RDZEŃ│    │ RDZEŃ│   │
│  │  3   │    │  4   │   │
│  └──────┘    └──────┘   │
└─────────────────────────┘
```

**Zalety:**
✅ Równoległe wykonywanie zadań
✅ Lepsza wydajność w aplikacjach wielowątkowych

---

## 2. LIMIT WIELORDZENIOWOŚCI

### Pytanie: Dlaczego nie 100 rdzeni?

**Problem:** Magistrala pamięci (bottleneck)

### Schemat problemu:
```
Rdzeń 1 ─┐
Rdzeń 2 ─┤
Rdzeń 3 ─┤
  ...    ├─→ MAGISTRALA ──→ RAM
Rdzeń 20─┤    (wąskie gardło!)
Rdzeń 21─┤
  ...    ─┘
```

### Dlaczego 20-32 rdzenie to max?
1. **Wspólna magistrala** - wszystkie rdzenie konkurują o dostęp
2. **Ograniczona przepustowość** RAM
3. **Koordynacja** - synchronizacja kosztowna
4. **Pamięć cache** - konflikty (cache coherency)

**Powyżej 32 rdzeni:** Kolejne rdzenie czekają na pamięć!

---

## 3. GPU (Graphics Processing Unit)

### Definicja:
**GPU** = procesor graficzny z tysiącami prostych rdzeni

### Architektura GPU:
```
┌─────────────────────────────┐
│           GPU               │
│ ┌─┐┌─┐┌─┐┌─┐┌─┐┌─┐┌─┐┌─┐   │
│ └─┘└─┘└─┘└─┘└─┘└─┘└─┘└─┘   │ × 1000+ rdzeni
│ ┌─┐┌─┐┌─┐┌─┐┌─┐┌─┐┌─┐┌─┐   │ (CUDA cores)
│ └─┘└─┘└─┘└─┘└─┘└─┘└─┘└─┘   │
│         ...                 │
└─────────────────────────────┘
```

### Różnice CPU vs GPU:

| Cecha | CPU | GPU |
|-------|-----|-----|
| **Rdzenie** | 4-32 | 1000+ |
| **Moc rdzenia** | Wysoka | Niska |
| **Zadania** | Złożone | Proste |
| **Pamięć** | Cache duży | Cache mały |

---

## 4. DLACZEGO GPU JEST SZYBKIE?

### Kluczowa różnica:
**GPU = wiele prostych operacji równolegle**

### Przykład - renderowanie pikseli:
```
CPU (4 rdzenie):
Piksel 1 → Rdzeń 1
Piksel 2 → Rdzeń 2
Piksel 3 → Rdzeń 3
Piksel 4 → Rdzeń 4
...czas: 1920×1080÷4 = 518 400 cykli

GPU (2000 rdzeni):
Piksel 1-2000 → Rdzenie 1-2000 RÓWNOCZEŚNIE
...czas: 1920×1080÷2000 = 1036 cykli

GPU ~500× SZYBSZE!
```

### Zastosowania GPU:
✅ **Grafika** (renderowanie, tekstury)
✅ **Obliczenia** (AI, machine learning)
✅ **Kryptowaluty** (mining)

---

## 5. MASZYNA TURINGA

### Definicja:
**Maszyna Turinga** = abstrakcyjny model komputera (1936, Alan Turing)

### Składowe:
1. **Taśma** (nieskończona pamięć)
2. **Głowica** (czyta/pisze na taśmie)
3. **Stan** (aktualne "myślenie" maszyny)
4. **Tabela przejść** (instrukcje: co robić)

### Schemat:
```
┌─────────────────────────────┐
│   TAŚMA (nieskończona)      │
│ ...│0│1│0│1│1│0│0│...       │
└──────────▲──────────────────┘
           │
        Głowica
           │
      ┌────┴────┐
      │  STAN   │
      │  (Q5)   │
      └─────────┘
```

**Teza Churcha-Turinga:** Wszystko co obliczalne → maszyna Turinga

---

## 6. TEST TURINGA

### Definicja:
**Test Turinga** = test inteligencji maszyny

### Jak działa:
```
Człowiek ←→ Terminal ←→ ???
                         ├─ Człowiek?
                         └─ Komputer?

Jeśli człowiek NIE POTRAFI odróżnić
→ Maszyna "inteligentna"
```

### Pytanie Turinga:
"Czy maszyny potrafią myśleć?"
→ Test: Czy maszyna potrafi **oszukać** człowieka?

### Współczesność:
- **ChatGPT, Claude** - częściowo przechodzą test
- **Problem:** Co to znaczy "myśleć"?

---

## 7. ALAN TURING i ENIGMA

### Kim był Alan Turing?
- **Matematyk, kryptolog** (1912-1954)
- Ojciec informatyki teoretycznej
- Złamał kod **Enigma** (WWII)

### Enigma:
```
┌─────────────────────────┐
│   Maszyna szyfrująca    │
│   (Wehrmacht, Kriegsmarine)│
│   ┌─────────────┐       │
│   │  ROTORY (3) │       │
│   └─────────────┘       │
│   Kombinacje: 159 mln   │
└─────────────────────────┘
```

### Osiągnięcie Turinga:
✅ Zbudował **Bomba kryptologiczna** (komputer mechaniczny)
✅ Złamał Enigmę → skrócił wojnę o ~2 lata
✅ Uratował miliony żyć

---

## 8. TYPOWE PYTANIA EGZAMINACYJNE

### Q: Dlaczego max 20-32 rdzenie w CPU?
**A:** Magistrala pamięci (bottleneck) - rdzenie konkurują o dostęp do RAM.

### Q: Czym różni się GPU od CPU?
**A:** GPU ma tysiące prostych rdzeni (proste zadania równolegle), CPU ma kilka mocnych rdzeni (złożone zadania).

### Q: Co to jest maszyna Turinga?
**A:** Abstrakcyjny model komputera: taśma + głowica + stan + tabela przejść.

### Q: Co to jest test Turinga?
**A:** Test inteligencji: czy człowiek potrafi odróżnić maszynę od człowieka?

### Q: Co zrobił Alan Turing?
**A:** Złamał Enigmę (kod niemiecki), stworzył teorię maszyn Turinga.

---

## 9. SZYBKA ŚCIĄGA - TABELA

```
┌──────────────┬────────────────────────────────┐
│    TEMAT     │        KLUCZOWE PUNKTY         │
├──────────────┼────────────────────────────────┤
│ Wielordzeni. │  Max 20-32 (magistrala!)       │
│ GPU          │  1000+ prostych rdzeni         │
│ CPU vs GPU   │  CPU: złożone, GPU: proste     │
│ Maszyna Tur. │  Taśma + Głowica + Stan        │
│ Test Turinga │  Oszukać człowieka?            │
│ Enigma       │  Złamana przez Turinga (WWII)  │
└──────────────┴────────────────────────────────┘
```

**ZAPAMIĘTAJ:**
- **20-32 rdzenie** = limit przez magistralę
- **GPU** = masywna równoległość (grafika, AI)
- **Maszyna Turinga** = teoretyczny model komputera
- **Test Turinga** = test inteligencji (oszukanie człowieka)
- **Alan Turing** = Enigma + teoria obliczeń

