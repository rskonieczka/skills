# Repozytorium skilli agenta

Zbiór skilli (promptów operacyjnych) dla agenta AI pracującego w środowisku Devin/Windsurf. Każdy skill znajduje się we własnym katalogu i jest opisany plikiem `SKILL.md` z frontmatterem YAML. Repozytorium zawiera również przykładowy artefakt wygenerowany przez skilla `analiza`.

## Struktura repozytorium

```text
.
├── _shared/                 # Wspoldzielone sekcje referencyjne dla skilli
│   └── zrodla-i-narzedzia.md  # Kanoniczna wersja: Zrodla prawdy + Narzedzia lokalne
├── analiza/                 # Uniwersalny prompt do analizy obiektow
│   └── SKILL.md
├── context7/                # Pobieranie aktualnej dokumentacji bibliotek
│   └── SKILL.md
├── jak/                     # Zasady odpowiedzi na pytanie "jak"
│   └── SKILL.md
├── sprawdzenie/             # Wielowymiarowy audyt odpowiedzi i artefaktow AI
│   └── SKILL.md
├── weryfikacja/             # Weryfikacja faktow, twierdzen i zrodel wzgledem hierarchii zrodel prawdy
│   └── SKILL.md
├── zmienne/                 # Uniwersalny kontrakt zmiennych dla agentow
│   └── SKILL.md
├── umiejetnosc_podstawy.md  # Przyklad analizy pojecia "umiejetnosc" (wyjatek: nie jest skillem)
└── README.md                # Niniejszy plik
```

## Wspoldzielone sekcje referencyjne

Plik `_shared/zrodla-i-narzedzia.md` zawiera kanoniczna wersje sekcji `Zrodla prawdy` i `Narzedzia lokalne` (hierarchia zrodel, tabele narzedzi `desktop-commander` i `Memgraph MCP`, workflow przeszukiwania i grafowy).

Skille `analiza`, `sprawdzenie`, `weryfikacja`, `zmienne` i `context7` zawieraja kompaktowa liste 4 zrodel prawdy i 2 narzedzi lokalnych inline oraz referencje do `_shared/zrodla-i-narzedzia.md` na szczegoly, tabele i workflowy. Aktualizacja tabel i workflow w `_shared/` wystarczy do zsynchronizowania wszystkich skilli.

Skill `jak` zachowuje pelne sekcje inline (jest wzorcem referencyjnym dla `_shared/`).

## Konwencja pliku SKILL.md

Kazdy skill musi zawierac plik `SKILL.md` z frontmatterem YAML. Obslugiwane pola frontmatter:

| Pole | Wymagane | Znaczenie |
| --- | --- | --- |
| `name` | tak | Nazwa techniczna skillu (stosowana w wywolaniach) |
| `description` | tak | Krotki opis dzialania skillu |
| `version` | nie | Wersja semantyczna skillu |
| `argument-hint` | nie | Podpowiedz argumentow przyjmowanych przez skill |
| `triggers` | tak | List wyzwalaczy: `user`, `model` |
| `trigger` | nie | Tryb zawsze wlaczony (`always_on`), jesli skill ma byc aktywny permanentnie |
| `subagent` | nie | `true`, jesli skill moze byc uruchamiany jako subagent |
| `updated` | nie | Data ostatniej aktualizacji |

Po frontmatterze nastepuje tresc instrukcji w jezyku polskim, zgodnie z globalnymi zasadami stylu.

## Katalog skillow

### analiza

- **Plik:** `analiza/SKILL.md`
- **Wersja:** 2.0.0
- **Opis:** Uniwersalny prompt do analizy obiektow. Prowadzi analize rzeczy fizycznych, procesow, pojec abstrakcyjnych, organizacji, systemow informatycznych i artefaktow informacyjnych.
- **Argument:** `[NAZWA OBIEKTU]`
- **Tryby analizy:** `szybki`, `pelny` (domyslny), `doglebny`
- **Sekcje analizy:** Rozpoznanie typu, Tozsamosc, Struktura, Relacje, Zachowanie, Ocena, Zastosowania.
- **Wspolpraca:** Context7 MCP (dokumentacja), Serena MCP (kod zrodlowy), NotebookLM (zrodla badawcze).

### context7

- **Plik:** `context7/SKILL.md`
- **Opis:** Pobiera aktualna dokumentacje i przyklady kodu dla bibliotek przez Context7 MCP. Aktywowany komenda `use context7` lub dyrektywa w regulach globalnych.
- **Tryb:** `always_on`
- **Narzedzia:** `mcp3_resolve-library-id`, `mcp3_query-docs`
- **Limity:** Maksymalnie 3 wywolania resolve i 3 wywolania query na pytanie.

### jak

- **Plik:** `jak/SKILL.md`
- **Wersja:** 2.3.0
- **Opis:** Zasady odpowiedzi na pytanie "jak". Definiuje hierarchie zrodel prawdy i workflow przeszukiwania kodu oraz bazy wiedzy projektu.
- **Tryb:** `always_on`
- **Zrodla prawdy:** `.ai-kb`, Context7, notebooklm-mcp, Memgraph MCP.
- **Narzedzia lokalne:** `desktop-commander` (przeszukiwanie plikow), Memgraph MCP (warstwa grafowa).
- **Zapis wiedzy:** Ustalenia z Context7 i notebooklm-mcp zapisywane do `.ai-kb`.

### sprawdzenie

- **Plik:** `sprawdzenie/SKILL.md`
- **Wersja:** 3.1.0
- **Opis:** Wielowymiarowy audyt odpowiedzi i artefaktow AI. Ocenia zgodnosc z pytaniem, kompletnosc, logike, zrodla, ontologie, bezpieczenstwo i uzytecznosc.
- **Argument:** `[PYTANIE ZRODLOWE] [ODPOWIEDZ DO OCENY albo ARTEFAKT DO AUDYTU] [opcjonalnie: TRYB AUDYTU, ZRODLA, KRYTERIA]`
- **Tryby audytu:** `szybki`, `pelny` (domyslny), `zrodlowy`, `logiczny`, `ontologiczny`, `techniczny`, `decyzyjny`, `bezpieczenstwa`, `instrukcyjny`.
- **Wymiary audytu:** Zgodnosc z pytaniem, Kompletnosc, Poprawnosc logiczna, Poprawnosc merytoryczna, Spojnosc pojeciowa, Bezpieczenstwo, Uzytecznosc.

### weryfikacja

- **Plik:** `weryfikacja/SKILL.md`
- **Wersja:** 1.0.0
- **Opis:** Weryfikuje fakty, twierdzenia, hipotezy i zrodla wzgledem hierarchii zrodel prawdy. Sprawdza status prawdziwosciowy twierdzen, oznacza konflikty zrodel i braki dowodowe.
- **Argument:** `[TWIERDZENIE LUB ZBIOR TWIERDZEN] [opcjonalnie: KRYTERIUM, ZRODLA, TRYB WERYFIKACJI]`
- **Tryby weryfikacji:** `szybki`, `pelny` (domyslny), `zrodlowy`, `techniczny`, `cross-source`.
- **Statusy werdyktu:** `potwierdzony`, `obalony`, `niezweryfikowany`, `sprzeczny`.
- **Odróżnienie od `sprawdzenie`:** `sprawdzenie` audytuje odpowiedz AI pod katem kompletnosci, logiki, ontologii i bezpieczenstwa; `weryfikacja` sprawdza status prawdziwosciowy konkretnych twierdzen wobec zrodel.
- **Wspolpraca:** Context7 MCP (dokumentacja bibliotek i API), Serena MCP (kod zrodlowy), desktop-commander (pliki lokalne), Memgraph MCP (warstwa grafowa).

### zmienne

- **Plik:** `zmienne/SKILL.md`
- **Opis:** Ekstrahuje, normalizuje i waliduje zmienne potrzebne do dalszej pracy agentow. Dziala jako warstwa posrednia miedzy wejsciem uzytkownika a dalsza praca (strategia, research, planowanie, generowanie tresci).
- **Argument:** `[cel zadania] [kontekst lub zrodla]`
- **Subagent:** tak
- **Typy zrodel:** `user_provided`, `verified_source`, `agent_inference`, `hypothesis`, `unavailable`
- **Typy zmiennych:** `fact`, `requirement`, `constraint`, `assumption`, `hypothesis`, `metric`, `entity`, `relationship`, `risk`, `decision`, `preference`, `unknown`
- **Tryby dzialania:** `analysis` (domyslny), `transformation`, `full`, `audit`

## Plik przykladu

### umiejetnosc_podstawy.md

Przykladowy artefakt wygenerowany przez skilla `analiza` dla obiektu "umiejetnosc". Demonstruje pelna strukture analizy: rozpoznanie typu, tozsamosc, struktura, relacje, zachowanie, ocena i zastosowania. Nie jest skillem i nie posiada frontmattera.

## Zalecenia eksploatacyjne

1. Nowe skille umieszczaj w osobnym katalogu z plikiem `SKILL.md` zgodnym z konwencja frontmatter.
2. Zachowaj jezyk polski w tresci skilli i artefaktach.
3. Wersjonuj skille polem `version` w formacie semver.
4. Skille `always_on` (`context7`, `jak`) sa aktywne permanentnie; pozostale wyzwalane na zadanie.
5. Skille wspolpracuja z MCP: Context7 (dokumentacja), Serena (pamiec i kod projektu), NotebookLM (zrodla badawcze), Memgraph (warstwa grafowa).
