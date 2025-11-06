# Opach - Podróże

Strona internetowa poświęcona podróżom i przygódom rodzinnym.

## Export Plików (Backup)

Ten projekt zawiera workflow GitHub Actions do eksportu wszystkich plików z repozytorium jako backup na dysk lokalny.

### Jak wyeksportować pliki

1. Przejdź do zakładki "Actions" w repozytorium GitHub
2. Wybierz workflow "Export Files (Backup)" z listy po lewej stronie
3. Kliknij przycisk "Run workflow" (zielony przycisk)
4. Poczekaj, aż workflow się zakończy (zazwyczaj zajmuje to mniej niż minutę)
5. Przewiń w dół do sekcji "Artifacts" u dołu strony workflow
6. Kliknij nazwę artefaktu, aby pobrać archiwum .tar.gz

### Rozpakowanie archiwum

**Linux/Mac:**
```bash
tar -xzf opach-backup-YYYYMMDD-HHMMSS.tar.gz
```

**Windows:**
- Użyj programu 7-Zip lub WinRAR do rozpakowania archiwum
- Lub użyj wbudowanego narzędzia do rozpakowywania plików .tar.gz w Windows 10/11

### Informacje dodatkowe

- Archiwum zawiera wszystkie pliki śledzone przez Git
- Artefakty są przechowywane przez 90 dni na GitHubie
- Możesz uruchomić workflow w dowolnym momencie, aby utworzyć nową kopię zapasową
- Nazwa pliku zawiera datę i czas utworzenia backupu

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
