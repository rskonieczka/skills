# Uniwersalny prompt do tworzenia i sprawdzania skilli

Niniejszy dokument zawiera kompletne opracowanie: analizę pojęcia "skill" przeprowadzoną za pomocą promptu `analiza/SKILL.md`, mapowanie pojęcia "umiejętność" z `_pojecie_umiejetnosci.md` na "skill", uniwersalny prompt do tworzenia skilli oraz prompt do sprawdzania utworzonych skilli. Każda część zawiera wyjaśnienia kluczowych decyzji projektowych.

---

## Spis treści

1. Analiza pojęcia "skill"
2. Mapowanie pojęcia umiejętności na skill
3. Prompt A: Uniwersalny prompt do tworzenia skilli
4. Prompt B: Prompt do sprawdzania utworzonych skilli
5. Wyjaśnienia kluczowych decyzji projektowych

---

## 1. Analiza pojęcia "skill"

Analiza została przeprowadzona przez zastosowanie promptu `analiza/SKILL.md` do obiektu "skill". Poniżej przedstawiam syntetyczny wynik analizy w formie dostosowanej do celów niniejszego dokumentu. Pełna analiza siedmiu sekcji znajduje się w załączniku mentalnym; tu wyciągam elementy decydujące dla konstrukcji promptów.

### Rozpoznanie typu obiektu

Skill jest artefaktem informacyjnym o charakterze operacyjnym i dyspozycyjnym.

Jest artefaktem informacyjnym, ponieważ jest dokumentem tekstowym (plik `SKILL.md` z frontmatterem YAML). Jest operacyjny, ponieważ definiuje procedurę działania agenta AI. Jest dyspozycyjny, ponieważ opisuje zdolność agenta do wykonania określonego zadania, aktywowaną na żądanie, a nie wykonywaną stale.

**Pewność rozpoznania: wysoki.**

### 1.1. Definicja

Skill to zapisana w pliku `SKILL.md` operacyjna umiejętność agenta AI, składająca się z frontmatteru YAML (metadane techniczne) i treści instrukcji (procedura działania), która przekształca cel użytkownika w powtarzalny, zgodny z kryteriami rezultat poprzez określoną sekwencję kroków, reguł i formatów wyjścia.

Definicja łączy pięć elementów (zgodnych z definicją umiejętności z `_pojecie_umiejetnosci.md`):

- podmiot - agent AI,
- działanie - wykonanie zadania opisanego w skillu,
- cel - rezultat do osiągnięcia,
- warunki - kontekst, wejście, ograniczenia, narzędzia,
- kryterium oceny - kryteria jakości zdefiniowane w skillu.

### 1.2. Kategoria

Skill należy jednocześnie do kategorii:

- artefaktu informacyjnego (plik tekstowy),
- operacyjnej umiejętności agenta AI,
- zasobu działania (prompt operacyjny),
- przedmiotu oceny i walidacji (audyt przez Prompt B),
- elementu repozytorium umiejętności (katalog skilli).

Skill nie jest tym samym co:

- reguła globalna (reguła jest zawsze aktywna, skill jest wyzwalany na żądanie, chyba że `trigger: always_on`),
- dokumentacja (dokumentacja opisuje, skill instruuje działanie),
- skrypt (skrypt wykonuje kod, skill instruuje model językowy),
- pamięć projektu (pamięć przechowuje ustalenia, skill definiuje procedurę).

### 1.3. Zakres

Do zakresu skilla należą:

- frontmatter YAML z metadanymi technicznymi,
- definicja roli i trybów rozumowania,
- warunki stosowania i niestosowania,
- kontrakt wejścia (wymagane i opcjonalne),
- kontrola kompletności wejścia,
- tryby działania,
- hierarchia źródeł prawdy i narzędzia lokalne,
- instrukcja główna (procedura),
- sekcje merytoryczne dostosowane do typu zadania,
- zasady wykonania,
- format wyniku,
- przykład użycia.

Do zakresu skilla nie należą automatycznie:

- implementacja kodu (skill instruuje, nie wykonuje),
- pamięć projektu (to domena Serena memory),
- konfiguracja środowiska (to domena reguł globalnych i `.ai-kb`),
- dokumentacja bibliotek (to domena Context7),
- relacje między encjami (to domena Memgraph).

### 1.4. Granice pojęcia

| Pojęcie | Podstawowe pytanie | Przykład |
| --- | --- | --- |
| Skill | Jak agent ma wykonać określone zadanie? | `analiza/SKILL.md` instruuje analizę obiektu |
| Reguła globalna | Jakie zasady obowiązują zawsze? | `global_rules.md` definiuje hierarchię źródeł |
| Dokumentacja | Jak działa system lub biblioteka? | `README.md` opisuje repozytorium skilli |
| Pamięć projektu | Co ustalono w projekcie? | Serena memory: decyzje architektoniczne |
| Prompt jednorazowy | Jak rozwiązać konkretne zapytanie? | Prompt ad hoc bez frontmatteru i powtarzalności |

Granica między skillem a promptem jednorazowym przebiega w miejscu przejścia od jednorazowej instrukcji do powtarzalnej, sparametryzowanej umiejętności z metadanymi, kontraktem wejścia i formatem wyjścia.

### 1.5. Kontekst

Skille funkcjonują w środowisku agenta AI pracującego w Devin/Windsurf, we współpracy z serwerami MCP (Context7, Serena, NotebookLM, Memgraph) i lokalnymi narzędziami (`desktop-commander`). Wartość skilla zależy od dopasowania do konwencji repozytorium, hierarchii źródeł prawdy i dostępnych narzędzi.

### 2. Struktura

#### 2.1. Charakter struktury

Skill ma strukturę logiczną i funkcjonalną, nie materialną. Składa się z frontmatteru (metadane) i treści instrukcji (procedura).

#### 2.2. Składniki kluczowe

| Składnik | Znaczenie |
| --- | --- |
| Frontmatter YAML | Metadane techniczne: name, description, version, argument-hint, triggers |
| Rola | Definiuje ekspertową tożsamość agenta dla zadania |
| Kiedy stosować / nie stosować | Warunki aktywacji i granice zastosowania |
| Wejście | Kontrakt danych wejściowych (wymagane i opcjonalne) |
| Kontrola kompletności wejścia | Reguły zachowania przy niepełnym wejściu |
| Tryby | Warianty głębokości lub profilu działania |
| Źródła prawdy | Hierarchia źródeł informacji (referencja do `_shared`) |
| Narzędzia lokalne | Dostępne narzędzia wykonawcze (referencja do `_shared`) |
| Instrukcja główna | Procedura działania, sekwencja kroków |
| Sekcje merytoryczne | Dostosowane do typu zadania (np. wymiary audytu, sekcje analizy) |
| Zasady wykonania | Reguły jakości, ograniczenia, zakazy |
| Format wyniku | Struktura i oznaczanie wyjścia |
| Przykład | Demonstracja wejścia i wyjścia |

#### 2.3. Architektura działania

```text
żądanie użytkownika -> rozpoznanie celu -> kontrola wejścia -> wybór trybu -> dobór źródeł i narzędzi -> wykonanie procedury -> kontrola rezultatu -> korekta -> formatowanie wyjścia -> wynik
```

Proces ma charakter cykliczny przy zadaniach złożonych: agent wielokrotnie weryfikuje wejście, dobiera źródła i koryguje tok pracy.

### 3. Relacje

#### 3.1. Relacje wewnętrzne

- Frontmatter warunkuje wykrywalność i aktywację skilla.
- Rola wpływa na dobór trybów rozumowania.
- Wejście determinuje zakres wykonania procedury.
- Tryby sterują głębokością i profilem sekcji merytorycznych.
- Format wyniku warunkuje użyteczność rezultatu.
- Zasady wykonania ograniczają i porządkują procedurę.

#### 3.2. Relacje zewnętrzne

Skill współpracuje z:

- regułami globalnymi (hierarchia źródeł, styl, język),
- `_shared/zrodla-i-narzedzia.md` (kanoniczne źródła i narzędzia),
- serwerami MCP (Context7, Serena, NotebookLM, Memgraph),
- `desktop-commander` (narzędzia lokalne),
- innymi skillami (współpraca i odróżnianie zakresów),
- pamięcią projektu (Serena memory),
- bazą wiedzy projektu (`.ai-kb`).

#### 3.3. Powiązania systemowe

W repozytorium skilli skill jest:

- elementem katalogu skilli,
- przedmiotem wersjonowania (semver),
- przedmiotem audytu (Prompt B),
- zasobem wywoływanym przez agenta,
- jednostką współdzielącą `_shared`.

### 4. Zachowanie

#### 4.1. Funkcjonowanie

Skill ujawnia się poprzez wykonanie. Obserwuje się jego przejawy:

- zgodność rezultatu z celem,
- kompletność wyjścia,
- poprawność logiczną i merytoryczną,
- powtarzalność przy podobnym wejściu,
- samodzielność agenta (bez dodatkowych pytań),
- adaptację do wariantów wejścia.

Pojedyncze wykonanie jest słabym dowodem jakości skilla. Wiarygodna ocena wymaga powtarzalnego działania w reprezentatywnych warunkach (stąd Prompt B).

#### 4.2. Stany skilla

- brak skilla,
- szkic bez frontmatteru,
- szkic z frontmatterem, bez procedury,
- skill z procedurą, bez przykładu,
- skill kompletny, nieaudytowany,
- skill kompletny, audytowany, bez korekty,
- skill kompletny, audytowany, skorygowany,
- skill przestarzały (niezgodny z aktualną konwencją lub narzędziami).

### 5. Cel

#### 5.1. Funkcja podstawowa

Skill umożliwia przekształcanie celu użytkownika w powtarzalny, zgodny z kryteriami rezultat poprzez sparametryzowaną procedurę.

Skill rozwiązuje problem rozbieżności między:

- intencją użytkownika a wykonaniem agenta,
- jednorazowym promptem a powtarzalną umiejętnością,
- wiedzą dziedzinową a operacyjnym działaniem,
- dostępnością narzędzi a ich celowym użyciem.

#### 5.2. Ocena skuteczności

| Kryterium | Pytanie oceniające |
| --- | --- |
| Poprawność | Czy rezultat jest zgodny z celem i kryteriami skilla? |
| Kompletność | Czy skill zawiera wszystkie wymagane sekcje? |
| Powtarzalność | Czy podobne wejście daje podobny rezultat? |
| Samodzielność | Czy agent wykonuje zadanie bez nadmiarowych pytań? |
| Adaptacja | Czy skill dostosowuje się do wariantów wejścia? |
| Transfer | Czy struktura skilla nadaje się do podobnych zadań? |
| Bezpieczeństwo | Czy skill nie prowadzi do destrukcyjnych lub niebezpiecznych działań? |
| Trwałość | Czy skill pozostaje zgodny z konwencją po zmianach narzędzi? |
| Spójność | Czy skill jest zgodny z `_shared` i regułami globalnymi? |

### 6. Ograniczenia

#### 6.1. Ograniczenia wewnętrzne

- Jakość skilla jest ograniczona przez jakość definicji celu i kryteriów.
- Skill nie zastąpi wiedzy dziedzinowej, której brak w źródłach prawdy.
- Skill zbyt sztywny nie adaptuje się do wariantów wejścia.
- Skill zbyt ogólny traci powtarzalność i użyteczność.

#### 6.2. Ograniczenia zewnętrzne

- Skill zależy od dostępności serwerów MCP i narzędzi lokalnych.
- Zmiana konwencji repozytorium może uczynić skill przestarzałym.
- Zmiana hierarchii źródeł prawdy wymaga aktualizacji referencji do `_shared`.

#### 6.3. Ryzyka

- Skill bez sekcji "Kiedy nie stosować" może być wywołany poza zakresem.
- Skill bez kontroli wejścia może wykonać się na niepełnych danych.
- Skill bez formatu wyniku może zwrócić niejednoznaczne wyjście.
- Skill bez przykładu jest trudny do walidacji.
- Skill naruszający hierarchię źródeł może generować niespójne rezultaty.

### 7. Wnioski

#### Najważniejsze ustalenia

1. Skill to operacyjna umiejętność agenta AI zapisana jako artefakt informacyjny z metadanymi i procedurą.
2. Skill mapuje się na pojęcie umiejętności: podmiot (agent), działanie (zadanie), cel (rezultat), warunki (wejście, kontekst), kryterium (ocena).
3. Struktura skilla jest funkcjonalna: frontmatter + rola + kontrakt wejścia + procedura + format wyjścia + przykład.
4. Jakość skilla ocenia się przez powtarzalność, kompletność, adaptację, bezpieczeństwo i spójność z konwencją.
5. Skill współpracuje z `_shared`, regułami globalnymi, serwerami MCP i narzędziami lokalnymi.

---

## 2. Mapowanie pojęcia umiejętności na skill

Mapowanie opiera się na definicji umiejętności z `_pojecie_umiejetnosci.md`:

> Umiejętność to nabyta, możliwa do wykazania zdolność do celowego zastosowania wiedzy, metod, procedur, doświadczenia lub narzędzi w celu wykonania zadania albo rozwiązania problemu zgodnie z określonym kryterium jakości i w określonych warunkach.

### 2.1. Mapowanie pięciu elementów definicji

| Element umiejętności | Odpowiednik w skillu |
| --- | --- |
| Podmiot (osoba posiadająca umiejętność) | Agent AI wykonujący skill |
| Działanie (co ma zostać wykonane) | Zadanie zdefiniowane w instrukcji głównej i sekcjach merytorycznych |
| Cel lub problem | Rezultat opisany w sekcji celu i formatu wyniku |
| Warunki wykonania | Kontekst, wejście, ograniczenia, narzędzia, tryby |
| Kryterium oceny rezultatu | Kryteria jakości w sekcji zasad i formatu wyniku |

### 2.2. Mapowanie składników funkcjonalnych umiejętności

| Składnik umiejętności | Odpowiednik w skillu |
| --- | --- |
| Cel działania | Sekcja celu i opis rezultatu w formacie wyjścia |
| Rozpoznanie sytuacji | Sekcje "Kiedy stosować" i "Kiedy nie stosować" oraz kontrola wejścia |
| Wiedza operacyjna | Sekcja "Źródła prawdy" i referencje do `_shared` |
| Know-how | Instrukcja główna i sekcje merytoryczne |
| Procedura lub strategia | Sekwencja kroków w instrukcji głównej i sekcjach merytorycznych |
| Wykonanie | Format wyniku i oznaczanie wyjścia |
| Kontrola | Sekcja "Zasady wykonania" i kryteria oceny |
| Korekta | Tryby działania i reguły adaptacji |
| Adaptacja | Reguły dostosowania do typu obiektu lub wariantów wejścia |

### 2.3. Mapowanie architektury działania

Architektura działania umiejętności:

```text
bodziec lub zadanie -> rozpoznanie sytuacji -> wybór sposobu działania -> wykonanie -> ocena rezultatu -> korekta -> wynik
```

Odpowiednik w skillu:

```text
żądanie użytkownika -> rozpoznanie celu i kontroli wejścia -> wybór trybu i źródeł -> wykonanie procedury -> kontrola zgodności z zasadami -> korekta -> formatowanie wyniku
```

### 2.4. Mapowanie hierarchii umiejętności

| Poziom umiejętności | Odpowiednik w skillu |
| --- | --- |
| Czynności elementarne | Pojedyncze kroki w procedurze (np. odczyt frontmatteru) |
| Umiejętności cząstkowe | Pojedyncze sekcje skilla (np. kontrola wejścia) |
| Umiejętności złożone | Kompletny skill z wszystkimi sekcjami |
| Repertuar umiejętności | Zbiór skilli w repozytorium współpracujących przez `_shared` |
| Kompetencja kontekstowa | Dobór odpowiedniego skilla do zadania i łączenie skilli |

### 2.5. Mapowanie kryteriów oceny

| Kryterium umiejętności | Pytanie dla skilla |
| --- | --- |
| Poprawność | Czy rezultat skilla jest zgodny z celem i kryteriami? |
| Jakość | Czy wyjście jest czytelne, kompletne i użyteczne? |
| Czas | Czy skill prowadzi do rezultatu bez nadmiarowych kroków? |
| Powtarzalność | Czy podobne wejście daje podobny rezultat? |
| Samodzielność | Czy agent wykonuje skill bez nadmiarowych pytań do użytkownika? |
| Adaptacja | Czy skill dostosowuje się do wariantów wejścia i typu obiektu? |
| Transfer | Czy struktura skilla nadaje się do podobnych zadań? |
| Bezpieczeństwo | Czy skill nie prowadzi do destrukcyjnych lub niebezpiecznych działań? |
| Trwałość | Czy skill pozostaje zgodny z konwencją po zmianach narzędzi? |

### 2.6. Wniosek z mapowania

Skill jest operacyjną instancją pojęcia umiejętności w domenie agenta AI. Każdy składnik funkcjonalny umiejętności ma swój odpowiednik w strukturze skilla. Prompt do tworzenia skilli musi therefore wymuszać obecność wszystkich składników funkcjonalnych, a prompt do sprawdzania skilli musi weryfikować, czy wszystkie składniki są obecne i spójne.

---

## 3. Prompt A: Uniwersalny prompt do tworzenia skilli

Poniższy prompt jest uniwersalny i kompletny. Można go użyć do stworzenia dowolnego skilla w repozytorium `/etc/windsurf/skills/`. Prompt jest sparametryzowany: miejsce oznaczone `[...]` wypełnia twórca lub agent na podstawie celu skilla.

### Wyjaśnienie struktury promptu

Prompt jest zorganizowany w bloki odpowiadające składnikom funkcjonalnym umiejętności (patrz sekcja 2.2):

1. **Rola** - definiuje tożsamość agenta (podmiot umiejętności).
2. **Kiedy stosować / nie stosować** - rozpoznanie sytuacji.
3. **Wejście i kontrola kompletności** - warunki wykonania.
4. **Tryby** - korekta i adaptacja.
5. **Źródła prawdy i narzędzia** - wiedza operacyjna.
6. **Instrukcja główna** - know-how i procedura.
7. **Struktura skilla do wygenerowania** - wykonanie.
8. **Zasady tworzenia** - kontrola.
9. **Format wyniku** - formatowanie wyjścia.
10. **Przykład** - demonstracja.

### Treść promptu

````text
---
name: tworzenie-skilla
description: Uniwersalny prompt do tworzenia skilli agenta AI zgodnych z konwencją repozytorium /etc/windsurf/skills/.
version: 1.0.0
argument-hint: "[CEL SKILLA] [OPCJONALNIE: TYP ZADANIA, TRYB, ŹRÓDŁA]"
triggers:
  - user
  - model
---

# Uniwersalny prompt do tworzenia skilli

## Rola

Przyjmij rolę architekta umiejętności agenta AI, łączącego inżynierię promptów, projektowanie procedur operacyjnych i wiedzę o konwencjach repozytorium skilli. Twoim zadaniem jest stworzenie kompletnego pliku SKILL.md zgodnego z konwencją repozytorium /etc/windsurf/skills/.

## Kiedy stosować

Stosuj, gdy użytkownik prosi o:
- stworzenie nowego skilla,
- zaprojektowanie promptu operacyjnego dla agenta AI,
- sparametryzowanie powtarzalnej procedury jako umiejętności agenta,
- rozbudowę istniejącego skilla o brakujące sekcje.

## Kiedy nie stosować

Nie stosuj, gdy:
- użytkownik prosi o jednorazowy prompt bez metadanych i powtarzalności,
- użytkownik prosi o regułę globalną (zamiast skilla użyj reguł w global_rules.md),
- użytkownik prosi o dokumentację projektu (zamiast skilla użyj .ai-kb lub docs),
- użytkownik prosi o audyt istniejącego skilla (użyj Promptu B - sprawdzania skilli),
- użytkownik prosi o analizę obiektu (użyj skilla analiza).

## Język

Skilla twórz wyłącznie po polsku, zgodnie z globalnymi zasadami stylu. Nie używaj emoji w treści skilla ani w kodzie.

## Wejście

Wymagane:
- `CEL SKILLA` - jaki rezultat ma osiągać skill,
- `TYP ZADANIA` - kategoria zadania (analiza, audyt, generowanie, transformacja, weryfikacja, planowanie, ekstrakcja, inne).

Opcjonalnie:
- `TRYB TWORZENIA` - `szybki`, `pełny` (domyślnie), `dogłębny`,
- `ŹRÓDŁA` - materiały bazowe dla treści skilla,
- `KONTEKST` - środowisko, ograniczenia, sytuacja,
- `INSPIRACJA` - istniejący skill jako wzorzec struktury,
- `NARZĘDZIA` - serwery MCP i narzędzia lokalne do uwzględnienia,
- `ARGUMENT-HINT` - podpowiedź argumentów wejściowych skilla,
- `TRIGGERS` - wyzwalacze skilla (`user`, `model`, `always_on`).

## Kontrola kompletności wejścia

1. Jeśli brakuje `CEL SKILLA`, nie twórz skilla. Poproś o wskazanie celu.
2. Jeśli `TYP ZADANIA` jest niejednoznaczny, rozstrzygnij go na podstawie celu albo poproś o doprecyzowanie.
3. Jeśli `ŹRÓDŁA` są wskazane, traktuj je jako główną podstawę treści merytorycznej.
4. Jeśli brakuje `INSPIRACJI`, użyj struktury z `analiza/SKILL.md` lub `sprawdzenie/SKILL.md` jako wzorca.
5. Jeśli `TRYB TWORZENIA` nie jest wskazany, zastosuj tryb `pełny`.

## Tryby tworzenia

- `szybki` - frontmatter, rola, kiedy stosować, wejście, uproszczona procedura, format wyniku. Bez przykładu i bez pełnych sekcji merytorycznych.
- `pełny` - domyślny: wszystkie sekcje z konwencji repozytorium, pełna procedura, format wyniku, przykład.
- `dogłębny` - pełne sekcje, rozbudowane podsekcje merytoryczne, tabele, schematy, alternatywne tryby działania, obszerny przykład.

## Źródła prawdy

1. Konwencja repozytorium - `README.md` i istniejące skille w `/etc/windsurf/skills/`.
2. `_shared/zrodla-i-narzedzia.md` - kanoniczna hierarchia źródeł i narzędzi lokalnych.
3. `_pojecie_umiejetnosci.md` - definicja umiejętności i składników funkcjonalnych.
4. `analiza/SKILL.md` i `sprawdzenie/SKILL.md` - wzorce struktury skilla.
5. Reguły globalne - styl, język, hierarchia źródeł, reżim pracy.

Stosuj w podanej kolejności. Skille współdzielą sekcje `Źródła prawdy` i `Narzędzia lokalne` przez referencję do `_shared/zrodla-i-narzedzia.md`.

## Narzędzia lokalne

Do tworzenia skilla używaj:
- `desktop-commander` - odczyt istniejących skilli, `_shared`, `README.md`, zapis pliku SKILL.md,
- odczyt bezpośredni - jeśli desktop-commander jest niedostępny.

Nie używaj Context7 ani NotebookLM do tworzenia struktury skilla (one służą treści merytorycznej skilla, nie jego szkieletowi).

## Instrukcja główna

1. Rozpoznaj cel skilla i typ zadania na podstawie wejścia.
2. Wybierz wzorzec struktury: dla skilla analitycznego użyj `analiza/SKILL.md`, dla skilla audytowego użyj `sprawdzenie/SKILL.md`, dla innych typów użyj ogólnej struktury z `README.md`.
3. Zbuduj frontmatter YAML z polami: `name`, `description`, `version`, `argument-hint`, `triggers` (i opcjonalnie `trigger`, `subagent`, `updated`).
4. Zdefiniuj rolę agenta adekwatną do typu zadania.
5. Określ "Kiedy stosować" i "Kiedy nie stosować" z jawnym odróżnieniem od pokrewnych skilli.
6. Zdefiniuj kontrakt wejścia: wymagane i opcjonalne pola.
7. Zdefiniuj kontrolę kompletności wejścia z regułami zachowania przy brakach.
8. Zdefiniuj tryby działania skilla (np. `szybki`, `pełny`, `dogłębny` lub tryby profilowe).
9. Wstaw kompaktową listę źródeł prawdy i narzędzi lokalnych z referencją do `_shared/zrodla-i-narzedzia.md`.
10. Napisz instrukcję główną jako sekwencję kroków procedury.
11. Zbuduj sekcje merytoryczne dostosowane do typu zadania (np. wymiary audytu, sekcje analizy, typy zmiennych).
12. Zdefiniuj zasady wykonania: reguły jakości, ograniczenia, zakazy.
13. Zdefiniuj format wyniku z oznaczaniem sekcji wyjścia.
14. Dodaj przykład wejścia i wyjścia.
15. Zweryfikuj, czy skill zawiera wszystkie składniki funkcjonalne umiejętności (patrz sekcja "Struktura skilla do wygenerowania").

## Struktura skilla do wygenerowania

Każdy skill musi zawierać następujące sekcje w podanej kolejności. Sekcje oznaczone [wymagane] są obowiązkowe; [opcjonalne] zależą od typu zadania.

### Frontmatter YAML [wymagane]

Pola frontmatter zgodne z konwencją z `README.md`:

| Pole | Wymagane | Znaczenie |
| --- | --- | --- |
| `name` | tak | Nazwa techniczna skilla (małe litery, myślniki) |
| `description` | tak | Krótki opis działania skilla |
| `version` | tak | Wersja semantyczna skilla (semver) |
| `argument-hint` | tak | Podpowiedź argumentów przyjmowanych przez skill |
| `triggers` | tak | Lista wyzwalaczy: `user`, `model` |
| `trigger` | nie | `always_on`, jeśli skill ma być aktywny permanentnie |
| `subagent` | nie | `true`, jeśli skill może być uruchamiany jako subagent |
| `updated` | nie | Data ostatniej aktualizacji |

### Rola [wymagane]

Zdefiniuj ekspertową tożsamość agenta dla zadania. Rola musi implikować wieloletnie, praktyczne doświadczenie komercyjne w domenie zadania.

### Kiedy stosować [wymagane]

Wymień sytuacje, w których skill ma być stosowany. Użyj listy punktowanej.

### Kiedy nie stosować [wymagane]

Wymień sytuacje, w których skill nie ma być stosowany, z jawnym odróżnieniem od pokrewnych skilli (np. "użyj skilla X").

### Język [wymagane]

Zadeklaruj, że skill prowadzony jest po polsku, zgodnie z globalnymi zasadami stylu.

### Wejście [wymagane]

Podziel na:
- Wymagane - pola niezbędne do wykonania zadania,
- Opcjonalnie - pola sterujące trybem, zakresem, źródłami, szczegółowością.

### Kontrola kompletności wejścia [wymagane]

Zdefiniuj reguły zachowania przy brakach w wejściu. Każda reguła jako punkt listy.

### Tryby [wymagane]

Zdefiniuj tryby działania skilla. Domyślnie co najmniej `szybki` i `pełny`. Dla zadań złożonych dodaj tryby profilowe (np. `źródłowy`, `logiczny`, `techniczny`).

### Źródła prawdy [wymagane]

Wstaw kompaktową listę 4 źródeł prawdy z referencją do `_shared/zrodla-i-narzedzia.md`:

1. `.ai-kb` - dokumentacja projektu.
2. Context7 - dokumentacja bibliotek, frameworków i zewnętrznych API.
3. notebooklm-mcp - notebooki i źródła badawcze użytkownika.
4. Memgraph MCP - warstwa grafowa.

Dodaj reguły specyficzne dla danego skilla, jeśli są potrzebne.

### Narzędzia lokalne [wymagane]

Wstaw kompaktową listę narzędzi lokalnych z referencją do `_shared/zrodla-i-narzedzia.md`:

- `desktop-commander` (pełne) - lokalne przeszukiwanie kodu, `.ai-kb`, `docs`, formaty binarne, sesje REPL.
- `Memgraph MCP` (warstwa grafowa) - relacje, graf zależności, analiza architektury.

### Instrukcja główna [wymagane]

Opisz procedurę działania jako sekwencję kroków. Każdy krok jako punkt listy. Krok pierwszy to rozpoznanie celu i typu zadania.

### Sekcje merytoryczne [wymagane, dostosowane do typu zadania]

Zbuduj sekcje specyficzne dla typu zadania. Przykłady:

- dla skilla analitycznego: Rozpoznanie typu, Tożsamość, Struktura, Relacje, Zachowanie, Cel, Ograniczenia, Wnioski,
- dla skilla audytowego: Wymiary audytu (Zgodność, Kompletność, Logika, Merytoryka, Ontologia, Bezpieczeństwo, Użyteczność),
- dla skilla ekstrakcyjnego: Typy zmiennych, Źródła zmiennych, Walidacja, Normalizacja,
- dla skilla planistycznego: Cel, Zasoby, Ryzyka, Kroki, Kryteria sukcesu.

### Zasady wykonania [wymagane]

Zdefiniuj reguły jakości, ograniczenia i zakazy. Każda reguła jako punkt listy. Uwzględnij:
- oddzielanie faktów od interpretacji i hipotez,
- oznaczanie twierdzeń niezweryfikowanych,
- niezgadywanie brakujących danych,
- zachowanie intencji użytkownika,
- minimalny konieczny zakres zmian (jeśli skill modyfikuje artefakt),
- bezpieczeństwo (nie destrukcyjne, nie ujawniaj sekretów).

### Format wyniku [wymagane]

Zdefiniuj strukturę wyjścia. Określ:
- oznaczanie sekcji wyjścia (tagi lub nagłówki),
- kolejność sekcji,
- wymagane elementy,
- oznaczanie niezweryfikowanych twierdzeń,
- obsługę przypadku niemożliwego (gdy wejście nie pozwala na wykonanie).

### Przykład [wymagane w trybie pełny i dogłębny]

Dodaj przykład z:
- Wejście - oznaczone sekcje wejścia,
- Wyjście - skrócony lub pełny przykład wyniku.

## Zasady tworzenia

1. Zachowaj język polski w treści skilla.
2. Nie używaj emoji w treści skilla ani w kodzie.
3. Nie zgaduj składni frontmatteru - używaj wyłącznie pól z konwencji z `README.md`.
4. Nie duplikuj pełnych tabel z `_shared/zrodla-i-narzedzia.md` - wstaw kompaktową listę z referencją.
5. Każdy skill musi zawierać wszystkie składniki funkcjonalne umiejętności: cel, rozpoznanie sytuacji, wiedza operacyjna, know-how, procedura, wykonanie, kontrola, korekta, adaptacja.
6. Sekcja "Kiedy nie stosować" musi odróżniać skill od pokrewnych skilli w repozytorium.
7. Format wyniku musi być jawny i jednoznaczny.
8. Przykład musi demonstrować typowe wejście i wyjście.
9. Wersja semver: nowy skill zaczyna od `1.0.0`.
10. Nazwa skilla (pole `name`) musi być unikalna w repozytorium i zgodna z nazwą katalogu.
11. Nie twórz skilla, który pokrywa się zakresowo z istniejącym - najpierw sprawdź repozytorium.
12. Jeśli skill ma być zawsze aktywny, ustaw `trigger: always_on` i uzasadnij to w sekcji "Kiedy stosować".
13. Nie dodawaj sekcji, które nie mają zastosowania dla danego typu zadania - adaptuj strukturę do celu.
14. Zachowaj minimalny konieczny zakres - nie rozbudowuj skilla o sekcje niepotrzebne do celu.

## Format wyniku

Zwróć kompletny plik SKILL.md w bloku kodu markdown, gotowy do zapisu w katalogu `[nazwa-skilla]/SKILL.md`.

Struktura wyjścia:

```text
STATUS TWORZENIA: [pełny|ograniczony]
TRYB TWORZENIA: [szybki|pełny|dogłębny]
TYP ZADANIA: [analiza|audyt|generowanie|transformacja|weryfikacja|planowanie|ekstrakcja|inne]

SKILL:
[pełna treść pliku SKILL.md z frontmatterem]

UZASADNIENIE STRUKTURY:
[krótkie wyjaśnienie, dlaczego wybrano daną strukturę i tryby]

SPRAWDZENIE KOMPLETNOŚCI:
[lista składników funkcjonalnych umiejętności z oznaczeniem, czy są obecne w skillu]
```

Gdy tworzenie jest ograniczone (np. brak `CEL SKILLA`), zwróć:

```text
STATUS TWORZENIA: ograniczony
BRAKUJĄCE DANE: [lista]
PYTANIE UZUPEŁNIAJĄCE: [jedno precyzyjne pytanie]
```

## Przykład

### Wejście

```text
CEL SKILLA: Weryfikacja statusu prawdziwościowego twierdzeń wobec hierarchii źródeł prawdy.
TYP ZADANIA: weryfikacja
TRYB TWORZENIA: pełny
INSPIRACJA: sprawdzenie/SKILL.md
```

### Wyjście (skrócone)

```text
STATUS TWORZENIA: pełny
TRYB TWORZENIA: pełny
TYP ZADANIA: weryfikacja

SKILL:
---
name: weryfikacja
description: Weryfikuje fakty, twierdzenia, hipotezy i źródła względem hierarchii źródeł prawdy.
version: 1.0.0
argument-hint: "[TWIERDZENIE LUB ZBIÓR TWIERDZEŃ] [opcjonalnie: KRYTERIUM, ŹRÓDŁA, TRYB WERYFIKACJI]"
triggers:
  - user
  - model
---

# Weryfikacja statusu prawdziwościowego twierdzeń

## Rola
Przyjmij rolę eksperta od weryfikacji faktów, logiki argumentacji i walidacji źródeł.

## Kiedy stosować
[...]

## Kiedy nie stosować
[...]

[pozostałe sekcje zgodnie ze strukturą]

UZASADNIENIE STRUKTURY:
Struktura oparta na sprawdzenie/SKILL.md, ponieważ weryfikacja jest zadaniem pokrewnym audytowi, ale węższym - sprawdza status prawdziwościowy konkretnych twierdzeń, nie całość odpowiedzi AI.

SPRAWDZENIE KOMPLETNOŚCI:
- cel działania: obecny (sekcja celu i formatu wyniku)
- rozpoznanie sytuacji: obecny (kiedy stosować / nie stosować)
- wiedza operacyjna: obecny (źródła prawdy)
- know-how: obecny (instrukcja główna)
- procedura: obecny (kroki weryfikacji)
- wykonanie: obecny (format wyniku)
- kontrola: obecny (zasady wykonania)
- korekta: obecny (tryby weryfikacji)
- adaptacja: obecny (reguły adaptacji do typu twierdzenia)
````

---

## 4. Prompt B: Prompt do sprawdzania utworzonych skilli

Poniższy prompt służy do audytu utworzonych skilli. Weryfikuje, czy skill jest kompletny, spójny z konwencją repozytorium, zgodny z pojęciem umiejętności i wykonalny. Prompt jest sparametryzowany: miejsce oznaczone `[...]` wypełnia audytor lub agent.

### Wyjaśnienie struktury Promptu B

Prompt B jest zorganizowany w wymiary audytu odpowiadające kryteriom oceny umiejętności (patrz sekcja 2.5) oraz konwencji repozytorium:

1. **Zgodność z konwencją frontmatter** - weryfikacja metadanych technicznych.
2. **Kompletność sekcji** - weryfikacja obecności wszystkich wymaganych sekcji.
3. **Spójność z pojęciem umiejętności** - weryfikacja obecności składników funkcjonalnych.
4. **Wykonalność** - weryfikacja, czy procedura jest realnie wykonalna.
5. **Adaptacyjność** - weryfikacja, czy skill dostosowuje się do wariantów wejścia.
6. **Kryteria oceny** - weryfikacja, czy skill definiuje kryteria jakości.
7. **Zgodność z `_shared` i regułami globalnymi** - weryfikacja spójności z repozytorium.
8. **Bezpieczeństwo** - weryfikacja, czy skill nie prowadzi do destrukcyjnych działań.
9. **Powtarzalność i transfer** - weryfikacja, czy skill nadaje się do powtarzalnego użycia.

### Treść Promptu B

````text
---
name: sprawdzanie-skilla
description: Audyt utworzonych skilli pod kątem kompletności, spójności z konwencją, zgodności z pojęciem umiejętności i wykonalności.
version: 1.0.0
argument-hint: "[SKILL DO AUDYTU] [opcjonalnie: TRYB AUDYTU, KRYTERIA, INSPIRACJA]"
triggers:
  - user
  - model
---

# Audyt utworzonych skilli

## Rola

Przyjmij rolę audytora umiejętności agenta AI, łączącego inżynierię promptów, walidację konwencji i wiedzę o pojęciu umiejętności. Twoim zadaniem jest rzetelny audyt pliku SKILL.md pod kątem kompletności, spójności, wykonalności i bezpieczeństwa.

## Kiedy stosować

Stosuj, gdy użytkownik chce:
- sprawdzić nowo utworzony skill,
- zweryfikować skill przed dodaniem do repozytorium,
- ocenić, czy skill spełnia konwencję repozytorium,
- wykryć brakujące sekcje, niespójności lub ryzyka w skillu,
- ocenić, czy skill jest zgodny z pojęciem umiejętności.

## Kiedy nie stosować

Nie stosuj, gdy:
- użytkownik nie dostarczył pliku SKILL.md do audytu,
- użytkownik prosi o stworzenie skilla (użyj Promptu A - tworzenia skilli),
- użytkownik prosi o audyt odpowiedzi AI (użyj skilla sprawdzenie),
- użytkownik prosi o analizę obiektu (użyj skilla analiza),
- użytkownik prosi o weryfikację twierdzeń (użyj skilla weryfikacja).

## Język

Audyt prowadź i zwracaj wyłącznie po polsku, zgodnie z globalnymi zasadami stylu.

## Wejście

Wymagane:
- `SKILL DO AUDYTU` - pełna treść pliku SKILL.md.

Opcjonalnie:
- `TRYB AUDYTU` - `szybki`, `pełny` (domyślnie), `konwencja`, `umiejętność`, `wykonalność`, `bezpieczeństwo`,
- `KRYTERIA OCENY` - dodatkowe kryteria specyficzne dla projektu,
- `INSPIRACJA` - wzorzec skilla, względem którego audytować,
- `KONTEKST` - środowisko, w którym skill ma działać.

## Kontrola kompletności wejścia

1. Jeśli brakuje `SKILL DO AUDYTU`, nie wykonuj audytu. Poproś o dostarczenie pliku.
2. Jeśli plik nie zawiera frontmatteru YAML, ustaw status `ograniczony` i zgłoś brak frontmatteru.
3. Jeśli plik nie jest plikiem SKILL.md (brak struktury skilla), ustaw status `niemożliwy` i zgłoś, że materiał nie jest skillem.
4. Jeśli `TRYB AUDYTU` nie jest wskazany, zastosuj tryb `pełny`.

## Tryby audytu

- `szybki` - krótki werdykt, najważniejsze problemy i minimalna poprawka.
- `pełny` - domyślny audyt wszystkich wymiarów.
- `konwencja` - zgodność z konwencją frontmatter i strukturą z `README.md`.
- `umiejętność` - zgodność z pojęciem umiejętności (składniki funkcjonalne, kryteria oceny).
- `wykonalność` - czy procedura jest realnie wykonalna i powtarzalna.
- `bezpieczeństwo` - czy skill nie prowadzi do destrukcyjnych lub niebezpiecznych działań.

## Źródła prawdy

1. Konwencja repozytorium - `README.md` i istniejące skille w `/etc/windsurf/skills/`.
2. `_shared/zrodla-i-narzedzia.md` - kanoniczna hierarchia źródeł i narzędzi.
3. `_pojecie_umiejetnosci.md` - definicja umiejętności i składników funkcjonalnych.
4. `analiza/SKILL.md` i `sprawdzenie/SKILL.md` - wzorce struktury skilla.

## Narzędzia lokalne

Do audytu skilla używaj:
- `desktop-commander` - odczyt istniejących skilli, `_shared`, `README.md` dla porównania,
- odczyt bezpośredni - jeśli desktop-commander jest niedostępny.

## Wymiary audytu

### 1. Zgodność z konwencją frontmatter

Sprawdź:
- czy frontmatter YAML jest obecny i poprawny składniowo,
- czy zawiera wymagane pola: `name`, `description`, `version`, `argument-hint`, `triggers`,
- czy `name` jest unikalne w repozytorium i zgodne z nazwą katalogu,
- czy `version` jest w formacie semver,
- czy `triggers` zawiera `user` lub `model` (lub `trigger: always_on`),
- czy nie użyto nieobsługiwanych pól frontmatter.

### 2. Kompletność sekcji

Sprawdź obecność wszystkich wymaganych sekcji:
- Rola,
- Kiedy stosować,
- Kiedy nie stosować,
- Język,
- Wejście (wymagane i opcjonalne),
- Kontrola kompletności wejścia,
- Tryby,
- Źródła prawdy (z referencją do `_shared`),
- Narzędzia lokalne (z referencją do `_shared`),
- Instrukcja główna,
- Sekcje merytoryczne (dostosowane do typu zadania),
- Zasady wykonania,
- Format wyniku,
- Przykład (wymagany w trybie pełny i dogłębny).

Dla każdej brakującej sekcji wskaż priorytet: `krytyczny` (skill nie zadziała bez niej) lub `zalecany` (skill zadziała, ale jakość spadnie).

### 3. Spójność z pojęciem umiejętności

Sprawdź, czy skill zawiera wszystkie składniki funkcjonalne umiejętności:

| Składnik umiejętności | Gdzie w skillu | Pytanie audytowe |
| --- | --- | --- |
| Cel działania | Format wyniku, opis rezultatu | Czy skill jasno definiuje rezultat? |
| Rozpoznanie sytuacji | Kiedy stosować / nie stosować, kontrola wejścia | Czy skill rozpoznaje, kiedy i jak działać? |
| Wiedza operacyjna | Źródła prawdy, referencje do `_shared` | Czy skill wskazuje, skąd czerpać wiedzę? |
| Know-how | Instrukcja główna, sekcje merytoryczne | Czy skill opisuje, jak wykonać zadanie? |
| Procedura lub strategia | Sekwencja kroków w instrukcji głównej | Czy skill definiuje uporządkowaną procedurę? |
| Wykonanie | Format wyniku, oznaczanie wyjścia | Czy skill definiuje, jak wygląda wykonanie? |
| Kontrola | Zasady wykonania, kryteria oceny | Czy skill definiuje reguły kontroli jakości? |
| Korekta | Tryby działania, reguły adaptacji | Czy skill pozwala na korektę toku pracy? |
| Adaptacja | Reguły dostosowania do typu obiektu lub wariantów wejścia | Czy skill adaptuje się do wariantów wejścia? |

Dla każdego brakującego składnika wskaż, gdzie powinien się znaleźć i jak go uzupełnić.

### 4. Wykonalność

Sprawdź:
- czy instrukcja główna jest sekwencją wykonalnych kroków,
- czy kroki nie są zbyt ogólne (np. "zrób analizę" bez podsekcji),
- czy kroki nie są zbyt szczegółowe na poziomie instrukcji głównej (szczegóły w sekcjach merytorycznych),
- czy format wyniku jest jednoznaczny i osiągalny przez procedurę,
- czy kontrola wejścia jest spójna z kontraktem wejścia,
- czy tryby są spójne z instrukcją główną.

### 5. Adaptacyjność

Sprawdź:
- czy skill definiuje tryby działania,
- czy skill zawiera reguły dostosowania do wariantów wejścia,
- czy sekcje merytoryczne są dostosowane do typu zadania,
- czy skill nie jest zbyt sztywny (mechaniczne stosowanie wszystkich sekcji bez adaptacji),
- czy skill nie jest zbyt ogólny (utrata powtarzalności).

### 6. Kryteria oceny

Sprawdź, czy skill definiuje kryteria oceny rezultatu, odpowiadające kryteriom umiejętności:

| Kryterium | Pytanie audytowe |
| --- | --- |
| Poprawność | Czy skill definiuje, co jest poprawnym rezultatem? |
| Kompletność | Czy skill wymaga wszystkich sekcji wyjścia? |
| Powtarzalność | Czy podobne wejście daje podobny rezultat? |
| Samodzielność | Czy skill minimalizuje nadmiarowe pytania do użytkownika? |
| Adaptacja | Czy skill dostosowuje się do wariantów wejścia? |
| Bezpieczeństwo | Czy skill nie prowadzi do destrukcyjnych działań? |

### 7. Zgodność z `_shared` i regułami globalnymi

Sprawdź:
- czy sekcja "Źródła prawdy" zawiera kompaktową listę 4 źródeł z referencją do `_shared/zrodla-i-narzedzia.md`,
- czy sekcja "Narzędzia lokalne" zawiera kompaktową listę z referencją do `_shared`,
- czy skill nie duplikuje pełnych tabel z `_shared`,
- czy skill jest spójny z hierarchią źródeł prawdy z reguł globalnych,
- czy skill zachowuje język polski i styl z reguł globalnych,
- czy skill nie używa emoji w treści.

### 8. Bezpieczeństwo

Sprawdź:
- czy skill nie prowadzi do destrukcyjnych działań bez ostrzeżenia i potwierdzenia,
- czy skill nie ujawnia ani nie utrwala sekretów,
- czy skill nie modyfikuje plików, bazy danych ani środowiska bez zgody (jeśli skill ma efekty uboczne),
- czy sekcja "Kiedy nie stosować" wyklucza sytuacje ryzykowne,
- czy kontrola wejścia zapobiega wykonaniu na niepełnych lub niebezpiecznych danych.

### 9. Powtarzalność i transfer

Sprawdź:
- czy skill jest powtarzalny (podobne wejście daje podobny rezultat),
- czy struktura skilla nadaje się do podobnych zadań (transfer),
- czy przykład demonstruje typowe wejście i wyjście,
- czy skill nie pokrywa się zakresowo z istniejącym skillem w repozytorium.

## Skala oceny

Ocena liczbowa jest orientacyjna i nie zastępuje uzasadnienia w sekcjach wymiarowych.

- `90-100` - skill kompletny, spójny, wykonalny, bezpieczny, gotowy do repozytorium.
- `70-89` - skill zasadniczo kompletny, ale zawiera luki, drobne braki lub niespójności.
- `40-69` - skill częściowo kompletny, ma istotne braki sekcji, niespójności lub problemy wykonalności.
- `0-39` - skill niekompletny, niespójny, niewykonalny lub niebezpieczny - wymaga gruntownej przebudowy.

## Procedura

1. Odczytaj `SKILL DO AUDYTU` i rozpoznaj, czy jest plikiem SKILL.md.
2. Ustal `TRYB AUDYTU`; jeśli nie podano, użyj trybu `pełny`.
3. Sprawdź kompletność wejścia i w razie braków wstrzymaj pełny audyt.
4. Oceń frontmatter YAML (wymiar 1).
5. Oceń kompletność sekcji (wymiar 2).
6. Oceń spójność z pojęciem umiejętności (wymiar 3).
7. Oceń wykonalność (wymiar 4).
8. Oceń adaptacyjność (wymiar 5).
9. Oceń kryteria oceny (wymiar 6).
10. Oceń zgodność z `_shared` i regułami globalnymi (wymiar 7).
11. Oceń bezpieczeństwo (wymiar 8).
12. Oceń powtarzalność i transfer (wymiar 9).
13. Wystaw ocenę liczbową tylko wtedy, gdy materiał jest wystarczający.
14. Zaproponuj minimalną poprawkę, która usuwa najważniejsze problemy.
15. Przy statusie `niemożliwy` wskaż, czego brakuje, zamiast przepisywać treść z domysłów.

## Format wyniku

### Format trybu `szybki`

W trybie `szybki` zwróć tylko:
- `STATUS AUDYTU`
- `TRYB AUDYTU`
- `OCENA CAŁKOWITA`
- `WERDYKT`
- maksymalnie 3 najważniejsze problemy
- `ZALECANA POPRAWKA`

### Gdy audyt jest pełny albo ograniczony

```text
STATUS AUDYTU: [pełny|ograniczony]
TRYB AUDYTU: [szybki|pełny|konwencja|umiejętność|wykonalność|bezpieczeństwo]
OCENA CAŁKOWITA: [0-100 albo nieustalona]
OGRANICZENIA AUDYTU: [opis albo "Brak istotnych ograniczeń"]

WERDYKT: [krótka ocena skilla]

ZGODNOŚĆ Z KONWENCJĄ FRONTMATTER: [problemy albo "Brak stwierdzonych problemów"]
KOMPLETNOŚĆ SEKCJI: [brakujące sekcje z priorytetem albo "Brak stwierdzonych problemów"]
SPÓJNOŚĆ Z POJĘCIEM UMIEJĘTNOŚCI: [brakujące składniki funkcjonalne albo "Brak stwierdzonych problemów"]
WYKONALNOŚĆ: [problemy wykonalności albo "Brak stwierdzonych problemów"]
ADAPTACYJNOŚĆ: [problemy adaptacji albo "Brak stwierdzonych problemów"]
KRYTERIA OCENY: [brakujące kryteria albo "Brak stwierdzonych problemów"]
ZGODNOŚĆ Z _SHARED I REGUŁAMI GLOBALNYMI: [niespójności albo "Brak stwierdzonych problemów"]
BEZPIECZEŃSTWO: [ryzyka albo "Brak stwierdzonych problemów"]
POWTARZALNOŚĆ I TRANSFER: [problemy albo "Brak stwierdzonych problemów"]

NAJWAŻNIEJSZE PROBLEMY:
| priorytet | sekcja | problem | dlaczego to problem | minimalna poprawka |
| --- | --- | --- | --- | --- |
| ... | ... | ... | ... | ... |

SKILL PO POPRAWKACH:
[poprawiona wersja skilla z zastosowanymi minimalnymi poprawkami albo informacja, że skill nie wymaga korekty]
```

### Gdy audyt jest niemożliwy

```text
STATUS AUDYTU: niemożliwy
BRAKUJĄCE DANE: [lista]
POWÓD WSTRZYMANIA: [krótki opis]
PYTANIE UZUPEŁNIAJĄCE: [jedno precyzyjne pytanie]
```

## Przykład

### Wejście

```text
SKILL DO AUDYTU:
---
name: eksport-danych
description: Eksportuje dane do CSV.
version: 1.0
triggers:
  - user
---

# Eksport danych

## Rola
Jesteś ekspertem od eksportu danych.

## Instrukcja
Wyeksportuj dane do pliku CSV.
```

### Wyjście skrócone

```text
STATUS AUDYTU: ograniczony
TRYB AUDYTU: pełny
OCENA CAŁKOWITA: 35
OGRANICZENIA AUDYTU: Skill nie zawiera większości wymaganych sekcji.

WERDYKT: Skill jest niekompletny - brakuje kontraktu wejścia, kontroli, formatu wyniku, przykładu i większości sekcji. Wersja nie jest w formacie semver.

ZGODNOŚĆ Z KONWENCJĄ FRONTMATTER: Brak `argument-hint`; `version` nie jest semver (powinno być 1.0.0).
KOMPLETNOŚĆ SEKCJI: Brak: Kiedy stosować, Kiedy nie stosować, Język, Wejście, Kontrola wejścia, Tryby, Źródła prawdy, Narzędzia lokalne, Zasady wykonania, Format wyniku, Przykład (priorytet: krytyczny).
SPÓJNOŚĆ Z POJĘCIEM UMIEJĘTNOŚCI: Brak: rozpoznanie sytuacji, wiedza operacyjna, kontrola, korekta, adaptacja.
WYKONALNOŚĆ: Instrukcja jest zbyt ogólna - "Wyeksportuj dane do pliku CSV" bez kroków, źródeł danych, formatu.
[pozostałe wymiary]

NAJWAŻNIEJSZE PROBLEMY:
| priorytet | sekcja | problem | dlaczego to problem | minimalna poprawka |
| --- | --- | --- | --- | --- |
| krytyczny | Instrukcja | Brak procedury kroków | Agent nie wie, jak wykonać eksport | Dodaj sekwencję kroków z rozpoznaniem źródła danych |
| krytyczny | Wejście | Brak kontraktu wejścia | Agent nie wie, jakie dane wejściowe są wymagane | Dodaj sekcję Wejście z polami wymaganymi i opcjonalnymi |
| krytyczny | Format wyniku | Brak formatu wyjścia | Agent nie wie, jak ma wyglądać rezultat | Dodaj sekcję Format wyniku z oznaczaniem sekcji |

SKILL PO POPRAWKACH:
[poprawiona wersja skilla]
````

---

## 5. Wyjaśnienia kluczowych decyzji projektowych

### 5.1. Dlaczego prompt opiera się na pojęciu umiejętności

Pojęcie umiejętności z `_pojecie_umiejetnosci.md` dostarcza kanonicznej definicji, składników funkcjonalnych, architektury działania i kryteriów oceny. Skill jest operacyjną instancją umiejętności w domenie agenta AI. Opierając prompt na tym pojęciu, zapewnia się, że każdy skill będzie kompletną umiejętnością, a nie tylko jednorazowym promptem.

Mapowanie pięciu elementów definicji umiejętności (podmiot, działanie, cel, warunki, kryterium) na strukturę skilla gwarantuje, że skill definiuje:

- kto wykonuje (agent),
- co wykonuje (zadanie),
- po co (rezultat),
- w jakich warunkach (wejście, kontekst, narzędzia),
- według jakich kryteriów (zasady, format wyniku).

### 5.2. Dlaczego prompt wymaga referencji do `_shared`

Repozytorium skilli współdzieli sekcje `Źródła prawdy` i `Narzędzia lokalne` przez `_shared/zrodla-i-narzedzia.md`. Duplikowanie pełnych tabel w każdym skillu prowadziłoby do niespójności przy aktualizacji. Referencja do `_shared` zapewnia, że aktualizacja tabel i workflow w jednym pliku wystarczy do zsynchronizowania wszystkich skilli.

Prompt A wymaga wstawienia kompaktowej listy z referencją, a Prompt B weryfikuje, czy referencja jest obecna i czy skill nie duplikuje pełnych tabel.

### 5.3. Dlaczego prompt wymaga sekcji "Kiedy nie stosować"

Sekcja "Kiedy nie stosować" odpowiada składnikowi "rozpoznanie sytuacji" w pojęciu umiejętności. Bez niej skill może być wywołany poza zakresem, co prowadzi do nieprawidłowych rezultatów. Sekcja musi odróżniać skill od pokrewnych skilli w repozytorium, aby uniknąć nakładania się zakresów.

### 5.4. Dlaczego prompt wymaga kontroli wejścia

Kontrola kompletności wejścia odpowiada składnikowi "rozpoznanie sytuacji" i zapobiega wykonaniu skilla na niepełnych lub niejednoznacznych danych. Bez niej agent może wykonać zadanie na podstawie domysłów, co narusza zasadę "nie zgaduj brakujących danych" z reguł globalnych.

### 5.5. Dlaczego prompt wymaga trybów działania

Tryby działania odpowiadają składnikom "korekta" i "adaptacja" w pojęciu umiejętności. Pozwalają na dostosowanie głębokości i profilu działania do wariantów wejścia. Bez trybów skill jest albo zbyt sztywny (mechaniczne stosowanie wszystkich sekcji), albo zbyt ogólny (utrata powtarzalności).

### 5.6. Dlaczego prompt wymaga przykładu

Przykład demonstruje typowe wejście i wyjście, co umożliwia:

- walidację skilla (czy rezultat jest osiągalny przez procedurę),
- powtarzalność (czy podobne wejście daje podobny rezultat),
- transfer (czy struktura nadaje się do podobnych zadań).

Bez przykładu skill jest trudny do audytu i weryfikacji.

### 5.7. Dlaczego Prompt B weryfikuje spójność z pojęciem umiejętności

Wymiar 3 audytu (spójność z pojęciem umiejętności) weryfikuje, czy skill zawiera wszystkie składniki funkcjonalne umiejętności. Jest to wymiar unikalny dla audytu skilli, nieobecny w ogólnym audytorze odpowiedzi AI (`sprawdzenie/SKILL.md`). Bez tego wymiaru skill może być kompletny strukturalnie, ale niekompletny funkcjonalnie (np. brak kontroli, brak adaptacji).

### 5.8. Dlaczego Prompt B weryfikuje bezpieczeństwo

Skille mogą mieć efekty uboczne (modyfikacja plików, wywołanie narzędzi, generowanie kodu). Wymiar 8 audytu (bezpieczeństwo) weryfikuje, czy skill nie prowadzi do destrukcyjnych działań bez ostrzeżenia i potwierdzenia, czy nie ujawnia sekretów i czy kontrola wejścia zapobiega wykonaniu na niebezpiecznych danych. Jest to zgodne z zasadami bezpieczeństwa z reguł globalnych.

### 5.9. Dlaczego ocena liczbowa jest orientacyjna

Ocena liczbowa jest orientacyjna i nie zastępuje uzasadnienia w sekcjach wymiarowych, zgodnie z konwencją z `sprawdzenie/SKILL.md`. Ocenę wystawia się tylko wtedy, gdy materiał jest wystarczający do rzetelnego audytu. Przy statusie `ograniczony` lub `niemożliwy` ocena może być nieustalona.

### 5.10. Dlaczego prompt dopuszcza adaptację struktury do typu zadania

Zgodnie z zasadą adaptacji z `analiza/SKILL.md`, skill nie powinien mechanicznie stosować wszystkich sekcji, lecz adaptować strukturę do typu zadania. Prompt A wymusza obecność wszystkich składników funkcjonalnych umiejętności, ale dopuszcza adaptację sekcji merytorycznych do typu zadania (np. wymiary audytu dla skilla audytowego, sekcje analizy dla skilla analitycznego).

### 5.11. Relacja Promptu A i Promptu B do istniejących skilli

Prompt A (tworzenie skilli) i Prompt B (sprawdzanie skilli) są komplementarne:

- Prompt A tworzy skill zgodny z konwencją i pojęciem umiejętności,
- Prompt B audytuje skill pod kątem zgodności z konwencją i pojęciem umiejętności.

Oba prompty współpracują z istniejącymi skillami:

- `analiza/SKILL.md` - dostarcza wzorzec struktury dla skilli analitycznych,
- `sprawdzenie/SKILL.md` - dostarcza wzorzec struktury dla skilli audytowych i wzorzec wymiarów audytu dla Promptu B,
- `_shared/zrodla-i-narzedzia.md` - dostarcza kanoniczną hierarchię źródeł i narzędzi,
- `_pojecie_umiejetnosci.md` - dostarcza definicję umiejętności i składników funkcjonalnych.

Prompt B nie zastępuje skilla `sprawdzenie` - `sprawdzenie` audytuje odpowiedzi AI, a Prompt B audytuje skille (artefakty repozytorium). Zakresy są rozłączne.

### 5.12. Dlaczego prompty nie są skillami w repozytorium

Prompty A i B są zapisane w `_propmpt_tworzenia_skill.md` jako dokument referencyjny, a nie jako skille w osobnych katalogach. Powody:

- prompty są meta-skillami (tworzą i audytują skille), a nie skillami operacyjnymi dla zadań domenowych,
- umieszczenie ich w osobnych katalogach mogłoby sugerować, że są skillami domenowymi,
- dokument referencyjny jest łatwiejszy do utrzymania i aktualizacji.

Jeśli w przyszłości prompty mają być wywoływalne jako skille, można je przenieść do katalogów `tworzenie-skilla/` i `sprawdzanie-skilla/` z plikami SKILL.md zgodnymi z konwencją.
