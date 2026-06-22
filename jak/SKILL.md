---
name: jak
description: Zasady odpowiedzi na pytanie jak.
version: 2.3.0
triggers:
  - user
  - model
trigger: always_on
updated: 19.06.2026
---

# Zasady odpowiedzi na pytanie jak

Celem workflowu jest rzetelna odpowiedź na pytanie JAK?

## Kiedy stosować

Stosuj przy zadaniach wymagających:
- decyzji architektonicznej lub implementacyjnej,
- przeszukiwania kodu źródłowego lub bazy wiedzy projektu,
- ustalenia składni, API lub konfiguracji biblioteki,
- planowania zmian w plikach lub symbolach kodu,
- analizy relacji między encjami, mapy zależności lub grafu wywołań.

Nie stosuj przy:
- zadaniach czysto konwersacyjnych niezwiązanych z projektem,
- czystej edycji bez potrzeby decyzji architektonicznej lub implementacyjnej,
- zadaniach czysto operacyjnych (uruchom komendę, zrestartuj usługę), gdzie nie ma pytania o sposób realizacji.

## Zasady podejmowania decyzji

1. Najpierw korzystaj ze źródeł prawdy (patrz Źródła prawdy).
2. Jeśli ustalisz coś przez Context7 lub notebooklm-mcp, zapisz to bezwzględnie i w pierwszej kolejności do `.ai-kb`.
3. Jeśli dokumentacja projektu nie zawiera wprost informacji, nie zgaduj - sięgnij po Context7 lub notebooklm-mcp.
4. Przy analizie relacji i zależności między encjami użyj Memgraph MCP (warstwa grafowa).

## Źródła prawdy

1. Dokumentacja projektu w `.ai-kb`
2. Context7 - oficjalna dokumentacja bibliotek i frameworków
3. notebooklm-mcp - uzupełnianie braków z notebooków i źródeł badawczych
4. Memgraph MCP - warstwa grafowa: relacje między encjami, mapa zależności, graf wywołań, analiza architektury przez Cypher

### Hierarchia i konflikty źródeł

Stosuj źródła w podanej kolejności; niższe poziomy uruchamiaj dopiero, gdy wyższe nie dają odpowiedzi.

Gdy źródła się sprzeczają:
- dla faktów projektu (architektura, konwencje, decyzje) pierwszeństwo ma `.ai-kb`,
- dla składni i API bibliotek oraz frameworków pierwszeństwo ma Context7,
- konflikt zgłaszaj użytkownikowi z propozycją aktualizacji starszego źródła.

## Lokalne przeszukiwanie kodu i bazy wiedzy

Do lokalnego przeszukiwania kodu źródłowego i plików bazy wiedzy (`.ai-kb`, `docs`) używaj `desktop-commander`.

Stosuj gdy:
- szukasz fragmentów kodu, symboli, wzorców lub wartości w plikach lokalnych,
- przeszukujesz katalogi projektu (grep, find, odczyt plików),
- sprawdzasz zawartość `.ai-kb` lub `docs` bez pełnego odczytu katalogu,
- Serena MCP jest niedostępna lub nie obsługuje danego typu pliku.

Nie używaj `desktop-commander` do dokumentacji zewnętrznych bibliotek - do tego służy Context7.

Narzędzia `desktop-commander` do lokalnego przeszukiwania:

| Narzędzie | Kiedy używać |
| --- | --- |
| `read_file` | odczytaj plik (wspiera offset/length do stronicowania) |
| `read_multiple_files` | odczytaj kilka plików równocześnie |
| `list_directory` | wylistuj zawartość katalogu |
| `get_file_info` | sprawdź metadane pliku (rozmiar, data modyfikacji) |
| `start_search` | wyszukaj pattern w plikach (odpowiednik grep/rg) |
| `get_more_search_results` | pobierz kolejną stronę wyników wyszukiwania |

Narzędzia `desktop-commander` do edycji plików (mutujące):

| Narzędzie | Kiedy używać |
| --- | --- |
| `edit_block` | edytuj fragment pliku przez old_string/new_string |
| `write_file` | zapisz plik (gdy brak dostępu przez standardowy edytor) |

Workflow przeszukiwania:
1. `list_directory` - sprawdź strukturę katalogu projektu lub `.ai-kb`
2. `start_search` - znajdź pattern, nazwę klasy lub fragment kodu
3. `read_file` z `offset`/`length` - odczytaj tylko istotny fragment dużego pliku
4. `get_file_info` - zweryfikuj datę modyfikacji przed edycją

## Warstwa grafowa (Memgraph MCP)

Memgraph stanowi warstwę grafową uzupełniającą pamięć tekstową Serena. Służy do analizy relacji między encjami, mapy zależności, grafu wywołań i architektury przez Cypher.

Stosuj gdy:
- analizujesz relacje między encjami i zależności między modułami,
- budujesz graf wywołań lub mapę zależności,
- potrzebujesz algorytmów grafowych (PageRank, betweenness centrality, sąsiedztwo węzła),
- weryfikujesz spójność architektury na poziomie powiązań.

Narzędzia Memgraph MCP:

| Narzędzie | Kiedy używać |
| --- | --- |
| `get_configuration` | sprawdź połączenie i konfigurację przed pierwszym użyciem |
| `list_databases` / `use_database` | wybierz aktywną bazę w sesji |
| `get_schema` | sprawdź schemat grafu przed zapytaniem |
| `run_query` | wykonaj zapytanie Cypher (odczyt/zapis) |
| `get_node_neighborhood` | znajdź węzły w zadanej odległości od węzła |
| `get_page_rank` / `get_betweenness_centrality` | analiza centralności węzłów |
| `get_procedures` | listuj dostępne procedury MAGE i moduły zapytań |
| `get_index` / `get_constraint` / `get_storage` / `get_triggers` | metadane grafu |

Workflow grafowy:
1. `get_configuration` - zweryfikuj połączenie z bazą
2. `get_schema` - sprawdź schemat przed zapytaniem
3. `run_query` - wykonaj Cypher dopasowany do pytania
4. W razie błędu połączenia wskaż konieczność uruchomienia bazy przez `docker compose up -d` w katalogu instalacji Memgraph (domyślnie `~/.local/share/memgraph/`, ścieżka zależy od instalacji).

Memgraph nie zastępuje Serena memory (wiedza deklaratywna) ani Context7 (dokumentacja zewnętrzna) - uzupełnia je o relacje i analizę strukturalną.

## Zapis do `.ai-kb`

Gdy ustalisz coś przez Context7 lub notebooklm-mcp, zapisz to bezwzględnie i w pierwszej kolejności do `.ai-kb`.

Workflow zapisu:
1. Wybierz kategorię pliku w `.ai-kb`: `architecture`, `conventions`, `decisions`, `pitfalls` (lub inną istniejącą w projekcie).
2. Sprawdź przez `desktop-commander`, czy plik kategorii istnieje.
3. Jeśli istnieje - dopisz nową sekcję z nagłówkiem, datą i źródłem (Context7 / notebooklm-mcp / inne).
4. Jeśli nie istnieje - utwórz plik z krótkim opisem kategorii i pierwszą sekcją.
5. Każda sekcja zawiera: datę, źródło, treść ustalenia, ewentualne ograniczenia.

## Przykład użycia end-to-end

Pytanie: Jak skonfigurować kolejkowanie zadań w Laravel w tym projekcie?

1. Sprawdź `.ai-kb` (np. `architecture/queue.md`) - czy projekt już opisuje kolejkowanie.
2. Jeśli brak - sprawdź kod projektu przez `desktop-commander` (`start_search` po `Queue::` lub `ShouldQueue`).
3. Jeśli kod nie daje pełnej odpowiedzi - pobierz dokumentację Laravel Queue przez Context7.
4. Jeśli pojawia się decyzja (np. wybór drivera) - zapisz ją do `.ai-kb/decisions/queue-driver.md` z datą i źródłem.
5. Jeśli pytanie dotyczy relacji jobów do encji - użyj Memgraph do analizy grafu zależności.
