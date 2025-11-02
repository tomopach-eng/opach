# opach.online - Blog Podróżniczy / Travel Blog

Strona internetowa dla bloga podróżniczego opach.online.

## 🌐 Strona online / Live Site

- **Domena:** [1.opach.online](https://1.opach.online) (lub [opach.online](https://opach.online))
- **Hosting:** GitHub Pages
- **SSL/HTTPS:** Darmowy certyfikat Let's Encrypt

## 🔒 Konfiguracja SSL/HTTPS

**Aby włączyć darmowy SSL (HTTPS) dla tej strony, przeczytaj:**

👉 **[SSL_SETUP.md](SSL_SETUP.md)** - Kompletny przewodnik krok po kroku (PL/EN)

### Szybki start:
1. Skonfiguruj rekord DNS CNAME wskazujący na `tomopach-eng.github.io`
2. Włącz "Enforce HTTPS" w ustawieniach GitHub Pages
3. Poczekaj na automatyczne przydzielenie certyfikatu (do 24h)

## 📁 Struktura projektu / Project Structure

```
├── index.html              # Strona główna
├── Podstrona-1/           # Kim jesteśmy?
├── Podstrona-2/           # Inspiracje
├── Podstrona-3/           # Poradniki
├── Podstrona-4/           # Kontakt
├── css/                   # Style CSS
├── js/                    # Pliki JavaScript
├── images/                # Obrazy
├── CNAME                  # Konfiguracja domeny
├── sitemap.xml            # Mapa strony dla SEO
└── robots.txt             # Konfiguracja dla robotów wyszukiwarek
```

## 🚀 Technologie / Technologies

- **HTML5** - Struktura strony
- **CSS3** - Stylizacja (Webflow CSS)
- **JavaScript** - Interaktywność (Webflow JS)
- **GitHub Pages** - Hosting
- **Let's Encrypt** - Darmowe certyfikaty SSL

## 📊 Monitoring jakości / Quality Monitoring

- **Lighthouse CI** - Automatyczne testy wydajności i jakości
  - Workflow: `.github/workflows/lighthouse.yml`
  - Włącza się automatycznie po skonfigurowaniu SSL

## 🔧 Rozwój / Development

### Lokalne testowanie
```bash
# Serwer lokalny (Python)
python -m http.server 8000

# Lub użyj dowolnego serwera HTTP
# Otwórz http://localhost:8000 w przeglądarce
```

### Publikacja zmian
1. Wprowadź zmiany w plikach
2. Commit i push do gałęzi `main`
3. GitHub Pages automatycznie zaktualizuje stronę (2-3 minuty)

## 📝 Dokumentacja / Documentation

- [SSL_SETUP.md](SSL_SETUP.md) - Instrukcja konfiguracji HTTPS (PL/EN)
- [WEBSITE_CHECK_REPORT.md](WEBSITE_CHECK_REPORT.md) - Raport techniczny strony
- [HTML_VALIDATION_REPORT.md](HTML_VALIDATION_REPORT.md) - Raport walidacji HTML

## 🐛 Zgłaszanie problemów / Issues

Jeśli znajdziesz problem, utwórz nowe issue w repozytorium GitHub.

## 📄 Licencja / License

Treść i design © Opach.online. Wszelkie prawa zastrzeżone.
