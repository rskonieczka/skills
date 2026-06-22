---
name: analiza
description: Uniwersalny prompt do analizy obiektów.
version: 1.1.0
argument-hint: "[NAZWA OBIEKTU]"
triggers:
  - user
  - model
---

# Uniwersalny Prompt do Analizy

## Rola

Przyjmij rolę eksperta od analizy obiektów i systemów, łączącego myślenie systemowe, analityczne i krytyczne.

## Kiedy stosować

Stosuj, gdy użytkownik prosi o analizę:
- rzeczy fizycznej,
- procesu,
- pojęcia abstrakcyjnego,
- organizacji,
- systemu informatycznego,
- artefaktu informacyjnego (dokument, tekst, raport, strona, instrukcja, regulamin),
- innego obiektu, którego typ rozpoznasz w toku analizy.

## Kiedy nie stosować

Nie stosuj, gdy użytkownik chce:
- audytu odpowiedzi albo artefaktu AI - użyj skilla `sprawdzenie`,
- podjęcia decyzji między wariantami - użyj trybu decyzyjnego,
- wygenerowania kodu, konfiguracji albo plików,
- czystego researchu bez wskazanego obiektu analizy.

## Język

Analizę prowadź i zwracaj wyłącznie po polsku, zgodnie z globalnymi zasadami stylu.

## Wejście

Wymagane:
- `NAZWA OBIEKTU`

Opcjonalnie:
- `KONTEKST` - środowisko, ograniczenia, sytuacja,
- `ZAKRES` - które sekcje pominąć albo pogłębić,
- `ŹRÓDŁA` - materiały bazowe,
- `OCZEKIWANY POZIOM SZCZEGÓŁOWOŚCI` - skrócony, standardowy, dogłębny.

## Polityka źródeł

1. Weryfikuj wiedzę zgodnie z hierarchią źródeł prawty: kod źródłowy, pamięć projektu Serena, dokumentacja projektu, Context7 MCP, NotebookLM.
2. Dla bibliotek, frameworków i API potwierdzaj aktualną składnię przez Context7 MCP.
3. Dla kodu źródłowego projektu używaj Serena MCP do nawigacji semantycznej.
4. Twierdzenia wymagające weryfikacji oznaczaj jako `niezweryfikowane`, jeśli brak źródeł.
5. Oddzielaj fakt potwierdzony od hipotezy i interpretacji.

## Instrukcja główna

Najpierw rozpoznaj, czym jest analizowany obiekt. Nie zakładaj z góry jego typu.

Możliwe typy:
- rzecz fizyczna,
- proces,
- pojęcie abstrakcyjne,
- organizacja,
- system informatyczny,
- artefakt informacyjny (dokument, tekst, raport, strona internetowa, instrukcja, regulamin itp.),
- inny typ, jeśli analiza wykaże taką potrzebę.

Po rozpoznaniu typu obiektu dostosuj zakres analizy. Nie stosuj wszystkich sekcji mechanicznie. Uwzględniaj wyłącznie te elementy, które mają znaczenie dla badanego obiektu.

Jeżeli jakaś sekcja nie występuje lub nie ma zastosowania, napisz krótko:

> Nie dotyczy dla tego typu obiektu.

Analiza ma opierać się na faktach, logicznych zależnościach i obserwowalnych cechach. Unikaj spekulacji oraz generowania treści bez podstaw.

---

Analiza obiektu: [NAZWA OBIEKTU]

## 1. Tożsamość

### Definicja
- Czym jest analizowany obiekt?
- Jak można go jednoznacznie zdefiniować?
- Do jakiej kategorii należy?

### Zakres
- Co należy do tego obiektu?
- Co nie należy do tego obiektu?
- Gdzie przebiegają jego granice?

### Kontekst
- W jakim środowisku funkcjonuje?
- W jakich sytuacjach występuje?

---

## 2. Struktura

### Składniki
- Z jakich elementów składa się obiekt?
- Które elementy są kluczowe?
- Które są pomocnicze?

### Hierarchia
- Jakie występują poziomy organizacji?
- Jakie są zależności między częściami?

### Architektura
- W jaki sposób elementy są uporządkowane?
- Jak wygląda organizacja całości?

---

## 3. Relacje

### Relacje wewnętrzne
- Jak elementy obiektu wpływają na siebie nawzajem?
- Jakie występują zależności?

### Relacje zewnętrzne
- Z czym obiekt współpracuje?
- Od czego jest zależny?
- Na co oddziałuje?

### Powiązania systemowe
- Jaką pełni rolę w szerszym kontekście?
- Jakie są jego wejścia i wyjścia?

---

## 4. Zachowanie

### Funkcjonowanie
- Jak działa obiekt?
- Jak przebiegają jego procesy lub mechanizmy?

### Zmiany
- Jak reaguje na zmiany otoczenia?
- Jakie stany może przyjmować?

### Dynamika
- Co inicjuje działanie?
- Co wpływa na jego zachowanie?
- Jakie występują skutki działania?

---

## 5. Cel

### Funkcja podstawowa
- Po co istnieje analizowany obiekt?
- Jaki problem rozwiązuje?

### Wartość
- Jaką korzyść dostarcza?
- Dla kogo jest użyteczny?

### Efekty
- Jakie rezultaty powinien generować?
- Jak można ocenić skuteczność realizacji celu?

---

## 6. Ograniczenia

### Ograniczenia wewnętrzne
- Jakie cechy konstrukcyjne lub organizacyjne ograniczają działanie?

### Ograniczenia zewnętrzne
- Jakie czynniki środowiskowe wpływają na funkcjonowanie?

### Ryzyka
- Co może powodować błędy, awarie lub niepowodzenia?

### Warunki brzegowe
- W jakich sytuacjach obiekt przestaje działać zgodnie z przeznaczeniem?
- Jakie są granice jego zastosowania?

---

## 7. Wnioski

### Najważniejsze ustalenia
Przedstaw najważniejsze obserwacje wynikające z analizy.

### Mocne strony
Wymień najistotniejsze zalety.

### Słabe strony
Wymień najważniejsze ograniczenia lub problemy.

### Kluczowe zależności
Wskaż relacje mające największy wpływ na funkcjonowanie obiektu.

### Podsumowanie
Przedstaw syntetyczny opis analizowanego obiektu w kilku akapitach, uwzględniając jego tożsamość, strukturę, relacje, zachowanie, cel i ograniczenia.

---

## Zasady analizy

1. Najpierw rozpoznaj typ obiektu.
2. Dostosuj głębokość analizy do charakteru obiektu.
3. Nie twórz sztucznej treści dla sekcji, które nie mają zastosowania.
4. Oddzielaj fakty od interpretacji.
5. Wskazuj zależności przyczynowo-skutkowe.
6. Uwzględniaj zarówno elementy jawne, jak i ukryte.
7. Koncentruj się na zrozumieniu działania obiektu, a nie wyłącznie na jego opisie.
8. Każdy wniosek powinien wynikać z wcześniejszej analizy.
9. Jeżeli informacje są niepełne, wskaż poziom niepewności.
10. Celem analizy jest zrozumienie: czym jest obiekt, jak działa, po co istnieje, od czego zależy i jakie ma ograniczenia.

## Format wyniku

- Zachowaj numerację sekcji 1-7.
- Pomijaj sekcje nie mające zastosowania z jawnym oznaczeniem `Nie dotyczy dla tego typu obiektu.`
- Zawsze kończ sekcją `Wnioski`.
- Używaj list punktowanych dla pytań pomocniczych.
- Oznaczaj niezweryfikowane twierdzenia.

## Przykład

### Wejście

```text
NAZWA OBIEKTU: Rejestr BIP
KONTEKST: Samorządowy Biuletyn Informacji Publicznej
```

### Wyjście (skrócone)

```text
1. Tożsamość
Definicja: Rejestr BIP to publicznie dostępny wykaz informacji o działalności organu administracji publicznej, prowadzony zgodnie z ustawą o dostępie do informacji publicznej.
Zakres: Obejmuje informacje, dokumenty i dane publikowane obowiązkowo; nie obejmuje informacji niepublicznych.
Kontekst: Funkcjonuje w środowisku prawnym i organizacyjnym jednostki samorządu terytorialnego.

2. Struktura
Składniki: Moduł publikacji, moduł wyszukiwania, archiwum, panel redaktorów.
Hierarchia: Organ -> Wydział -> Redaktor -> Treść.

...

7. Wnioski
Najważniejsze ustalenia: Rejestr BIP jest narzędziem transparentności, którego działanie zależy od poprawności procesów publikacji i dostępności technicznej.
Mocne strony: Wymóg ustawowy, publiczny dostęp, ustandaryzowany zakres.
Słabe strony: Zależność od redaktorów, ryzyko przestarzałych treści, ograniczona wyszukiwalność.
```
