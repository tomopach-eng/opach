# Opach - Podróże

Strona internetowa poświęcona podróżom i przygódom rodzinnym.

## Lighthouse CI Workflow

Ten projekt zawiera zautomatyzowany workflow GitHub Actions do uruchamiania testów Lighthouse CI.

### Jak używać

Workflow można uruchomić ręcznie poprzez:

1. Przejście do zakładki "Actions" w repozytorium GitHub
2. Wybór workflow "Lighthouse CI" z listy po lewej stronie
3. Kliknięcie przycisku "Run workflow"

### Co robi workflow

1. **Czeka na dostępność HTTPS** - Sprawdza czy strona https://opach.online jest dostępna i ma ważny certyfikat SSL
2. **Uruchamia Lighthouse** - Przeprowadza testy wydajności, dostępności, SEO i najlepszych praktyk
3. **Zbiera raporty** - Znajduje i pakuje wszystkie wygenerowane raporty Lighthouse
4. **Zapisuje artefakty** - Udostępnia raporty jako artefakty do pobrania

### Konfiguracja

Workflow jest skonfigurowany do:
- Uruchamiania ręcznego (workflow_dispatch)
- Testowania strony https://opach.online
- Oczekiwania do 15 minut na dostępność strony
- Wykonania jednego testu Lighthouse

### Wyniki

Po zakończeniu workflow:
- Raporty Lighthouse są dostępne jako artefakty w zakładce "Actions"
- Nazwa artefaktu: `lighthouse-reports-{RUN_ID}`
- Artefakty zawierają pliki HTML i JSON z wynikami testów
