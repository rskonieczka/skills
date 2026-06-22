---
name: context7
description: Pobiera aktualną dokumentację i przykłady kodu dla dowolnej biblioteki za pomocą Context7 MCP server
triggers:
  - user
  - model
trigger: always_on
---

## Polecenie: "use context7"

Gdy użytkownik napisze **"use context7"** lub w regułach globalnych pojawi się taka dyrektywa, należy traktować dokumentację pobraną przez Context7 jako **domyślne i preferowane źródło prawdy** dla bibliotek i frameworków.

1. **Przed odpowiedzią o API biblioteki, napisaniem kodu zależnego od zewnętrznej biblioteki lub zaproponowaniem składni** wywołać `mcp3_resolve-library-id`, aby uzyskać Context7-compatible library ID.
2. **Następnie obowiązkowo** wywołać `mcp3_query-docs` z uzyskanym ID i konkretnym pytaniem, aby pobrać aktualną dokumentację i snippety kodu.
3. **Oprzeć odpowiedź w pierwszej kolejności na dokumentacji Context7**, a wiedzy własnej modelu używać wyłącznie pomocniczo.
4. **Jeśli dokumentacja nie odpowiada wprost na pytanie lub biblioteki nie da się rozpoznać**, użyć najlepszych dostępnych informacji jako fallback i jasno zaznaczyć, że odpowiedź nie opiera się bezpośrednio na dokumentacji Context7.

### Kiedy używać:
- Przy implementacji nowych funkcji z użyciem zewnętrznych bibliotek (np. TipTap, Tauri, React).
- Przy debugowaniu problemów z API bibliotek.
- Gdy nie ma pewności co do aktualnej składni lub best practices danej wersji.

### Zasady:
- Dokumentacja Context7 ma pierwszeństwo przed wiedzą własną modelu wszędzie tam, gdzie można ją pobrać.
- Maksymalnie **3 wywołania** `mcp3_resolve-library-id` i **3 wywołania** `mcp3_query-docs` na pytanie.
- Nie wysyłaj wrażliwych danych (klucze API, hasła) w zapytaniach.
- Jeśli po 3 próbach nie znajdziesz odpowiedzi, użyj najlepszych dostępnych informacji i oznacz to jako fallback względem dokumentacji.

## Źródła prawdy

1. `.ai-kb` - dokumentacja projektu: architektura, konwencje, decyzje, pułapki.
2. Context7 - dokumentacja bibliotek, frameworków i zewnętrznych API (główne źródło tego skillu).
3. notebooklm-mcp - notebooki i źródła badawcze użytkownika.
4. Memgraph MCP - warstwa grafowa: relacje, mapa zależności, graf wywołań, analiza architektury przez Cypher.

Stosuj w podanej kolejności; niższe poziomy uruchamiaj dopiero, gdy wyższe nie dają odpowiedzi. Konflikty źródeł i hierarchia: patrz `_shared/zrodla-i-narzedzia.md`.

## Narzędzia lokalne

- `desktop-commander` (pełne) - lokalne przeszukiwanie kodu, `.ai-kb`, `docs`, formaty binarne, sesje REPL.
- `Memgraph MCP` (warstwa grafowa) - relacje między encjami, graf zależności, analiza architektury przez Cypher.

Tabele narzędzi, workflow przeszukiwania i workflow grafowy: patrz `_shared/zrodla-i-narzedzia.md`.
