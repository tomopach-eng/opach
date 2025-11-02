# Jak dodać darmowy SSL do strony (HTTPS) / How to Add Free SSL (HTTPS)

[Polish version below | Wersja polska poniżej]

---

## 🇬🇧 English Version

### Overview

GitHub Pages provides **free SSL certificates** automatically through Let's Encrypt for custom domains. This guide will help you enable HTTPS for `1.opach.online`.

### Prerequisites

- Your domain `1.opach.online` must point to GitHub Pages servers
- You must have admin access to the GitHub repository
- DNS changes can take 24-48 hours to propagate

---

## Step-by-Step Instructions

### Step 1: Verify DNS Configuration

Your domain needs to be configured with the following DNS records:

#### For subdomain (1.opach.online):

Create a **CNAME record**:
```
Type: CNAME
Name: 1
Value: tomopach-eng.github.io
TTL: 3600 (or default)
```

**Important:** Do NOT use an A record for subdomains. Use CNAME only.

#### How to check your current DNS:
```bash
# Check CNAME record
nslookup 1.opach.online

# Or use dig
dig 1.opach.online CNAME +short
```

Expected result: Should show `tomopach-eng.github.io`

---

### Step 2: Verify CNAME File in Repository

✅ Your repository already has the correct CNAME file with content: `1.opach.online`

This file tells GitHub Pages which custom domain to use.

---

### Step 3: Enable HTTPS in GitHub Pages Settings

1. Go to your repository: `https://github.com/tomopach-eng/opach`
2. Click on **Settings** (top menu)
3. In the left sidebar, click on **Pages**
4. Under "Custom domain", you should see: `1.opach.online`
5. Wait for the DNS check to complete (green checkmark appears)
6. Once DNS is verified, check the box: **☑ Enforce HTTPS**

---

### Step 4: Wait for Certificate Provisioning

After enabling "Enforce HTTPS":
- GitHub automatically requests a free SSL certificate from Let's Encrypt
- This process can take from a few minutes up to **24 hours**
- You'll see a status message in the Pages settings during this time

**During provisioning:**
- ⏳ "Waiting for certificate provisioning..."
- ✅ "Your site is published at https://1.opach.online" (when complete)

---

### Step 5: Verify HTTPS is Working

Once the certificate is provisioned:

1. Visit: `https://1.opach.online` (note the 'https')
2. Check for the padlock icon 🔒 in your browser's address bar
3. Click the padlock to view certificate details

**Test with command line:**
```bash
curl -I https://1.opach.online
```

You should see `HTTP/2 200` and no SSL errors.

---

## Troubleshooting

### Problem: "DNS check failed"

**Solutions:**
1. Verify your DNS CNAME record points to `tomopach-eng.github.io`
2. Wait 24-48 hours for DNS propagation
3. Clear DNS cache: `ipconfig /flushdns` (Windows) or `sudo dscacheutil -flushcache` (macOS)
4. Check DNS propagation: https://www.whatsmydns.net

### Problem: "Certificate provisioning failed"

**Solutions:**
1. Remove the custom domain from GitHub Pages settings
2. Wait 5 minutes
3. Re-add the custom domain
4. Wait for certificate provisioning to retry

### Problem: "Mixed content" warnings after enabling HTTPS

**Solution:**
- Ensure all resources (images, CSS, JS) use HTTPS URLs
- Update any `http://` links to `https://` or use protocol-relative URLs (`//`)

### Problem: Certificate not provisioning after 24 hours

**Solutions:**
1. Check that ONLY a CNAME record exists (remove any A or AAAA records for the subdomain)
2. Ensure CAA records (if any) allow Let's Encrypt: `0 issue "letsencrypt.org"`
3. Contact GitHub Support: https://support.github.com

---

## Security Best Practices

Once HTTPS is enabled:

1. ✅ **Always use HTTPS URLs** in your content
2. ✅ **Enable "Enforce HTTPS"** to redirect HTTP to HTTPS automatically
3. ✅ **Update all internal links** to use HTTPS
4. ✅ **Update Google Search Console** with HTTPS version
5. ✅ **Update sitemap.xml** to use HTTPS URLs

---

## Additional Resources

- [GitHub Pages Custom Domain Docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Troubleshooting HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
- [Let's Encrypt Information](https://letsencrypt.org/)

---
---

## 🇵🇱 Wersja Polska

### Przegląd

GitHub Pages zapewnia **darmowe certyfikaty SSL** automatycznie poprzez Let's Encrypt dla domen niestandardowych. Ten przewodnik pomoże Ci włączyć HTTPS dla `1.opach.online`.

### Wymagania wstępne

- Twoja domena `1.opach.online` musi wskazywać na serwery GitHub Pages
- Musisz mieć uprawnienia administratora do repozytorium GitHub
- Zmiany DNS mogą zająć 24-48 godzin, aby się rozpropagować

---

## Instrukcje krok po kroku

### Krok 1: Weryfikacja konfiguracji DNS

Twoja domena musi być skonfigurowana z następującymi rekordami DNS:

#### Dla subdomeny (1.opach.online):

Utwórz rekord **CNAME**:
```
Typ: CNAME
Nazwa: 1
Wartość: tomopach-eng.github.io
TTL: 3600 (lub domyślny)
```

**Ważne:** NIE używaj rekordu A dla subdomen. Używaj tylko CNAME.

#### Jak sprawdzić obecną konfigurację DNS:
```bash
# Sprawdź rekord CNAME
nslookup 1.opach.online

# Lub użyj dig
dig 1.opach.online CNAME +short
```

Oczekiwany rezultat: Powinien pokazać `tomopach-eng.github.io`

---

### Krok 2: Weryfikacja pliku CNAME w repozytorium

✅ Twoje repozytorium ma już poprawny plik CNAME z zawartością: `1.opach.online`

Ten plik informuje GitHub Pages, której domeny niestandardowej użyć.

---

### Krok 3: Włączenie HTTPS w ustawieniach GitHub Pages

1. Przejdź do swojego repozytorium: `https://github.com/tomopach-eng/opach`
2. Kliknij **Settings** (górne menu)
3. W lewym pasku bocznym kliknij **Pages**
4. W sekcji "Custom domain" powinieneś zobaczyć: `1.opach.online`
5. Poczekaj na zakończenie sprawdzenia DNS (pojawi się zielony znacznik)
6. Gdy DNS zostanie zweryfikowany, zaznacz pole: **☑ Enforce HTTPS**

---

### Krok 4: Oczekiwanie na przydzielenie certyfikatu

Po włączeniu "Enforce HTTPS":
- GitHub automatycznie żąda darmowego certyfikatu SSL z Let's Encrypt
- Ten proces może zająć od kilku minut do **24 godzin**
- W tym czasie zobaczysz komunikat o statusie w ustawieniach Pages

**Podczas przydzielania:**
- ⏳ "Waiting for certificate provisioning..." (Oczekiwanie na przydzielenie certyfikatu...)
- ✅ "Your site is published at https://1.opach.online" (gdy zakończone)

---

### Krok 5: Weryfikacja działania HTTPS

Gdy certyfikat zostanie przydzielony:

1. Odwiedź: `https://1.opach.online` (zauważ 'https')
2. Sprawdź ikonę kłódki 🔒 na pasku adresu przeglądarki
3. Kliknij kłódkę, aby zobaczyć szczegóły certyfikatu

**Test z linii poleceń:**
```bash
curl -I https://1.opach.online
```

Powinieneś zobaczyć `HTTP/2 200` i brak błędów SSL.

---

## Rozwiązywanie problemów

### Problem: "DNS check failed" (Sprawdzenie DNS nie powiodło się)

**Rozwiązania:**
1. Zweryfikuj, czy Twój rekord DNS CNAME wskazuje na `tomopach-eng.github.io`
2. Poczekaj 24-48 godzin na propagację DNS
3. Wyczyść cache DNS: `ipconfig /flushdns` (Windows) lub `sudo dscacheutil -flushcache` (macOS)
4. Sprawdź propagację DNS: https://www.whatsmydns.net

### Problem: "Certificate provisioning failed" (Nie udało się przydzielić certyfikatu)

**Rozwiązania:**
1. Usuń domenę niestandardową z ustawień GitHub Pages
2. Poczekaj 5 minut
3. Dodaj domenę niestandardową ponownie
4. Poczekaj, aż system ponowi próbę przydzielenia certyfikatu

### Problem: Ostrzeżenia o "mixed content" po włączeniu HTTPS

**Rozwiązanie:**
- Upewnij się, że wszystkie zasoby (obrazy, CSS, JS) używają URL-i HTTPS
- Zaktualizuj wszystkie linki `http://` na `https://` lub użyj URL-i względnych (`//`)

### Problem: Certyfikat nie przydziela się po 24 godzinach

**Rozwiązania:**
1. Sprawdź, czy istnieje TYLKO rekord CNAME (usuń wszelkie rekordy A lub AAAA dla subdomeny)
2. Upewnij się, że rekordy CAA (jeśli istnieją) zezwalają Let's Encrypt: `0 issue "letsencrypt.org"`
3. Skontaktuj się z obsługą GitHub: https://support.github.com

---

## Najlepsze praktyki bezpieczeństwa

Po włączeniu HTTPS:

1. ✅ **Zawsze używaj URL-i HTTPS** w swojej treści
2. ✅ **Włącz "Enforce HTTPS"**, aby automatycznie przekierowywać HTTP na HTTPS
3. ✅ **Zaktualizuj wszystkie linki wewnętrzne**, aby używały HTTPS
4. ✅ **Zaktualizuj Google Search Console** z wersją HTTPS
5. ✅ **Zaktualizuj sitemap.xml**, aby używał URL-i HTTPS

---

## Dodatkowe zasoby

- [Dokumentacja GitHub Pages dla domen niestandardowych](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Rozwiązywanie problemów z HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
- [Informacje o Let's Encrypt](https://letsencrypt.org/)

---

## Status implementacji

### Co jest już skonfigurowane ✅
- ✅ Plik CNAME w repozytorium (`1.opach.online`)
- ✅ Strona opublikowana na GitHub Pages
- ✅ Lighthouse CI workflow skonfigurowany dla HTTPS

### Co musisz zrobić 📋
1. Skonfiguruj rekord DNS CNAME u swojego dostawcy domeny
2. Włącz "Enforce HTTPS" w ustawieniach GitHub Pages
3. Poczekaj na przydzielenie certyfikatu (do 24h)
4. Zweryfikuj, że https://1.opach.online działa

### Po włączeniu HTTPS 🎉
- Lighthouse CI workflow będzie działać automatycznie
- Strona będzie zabezpieczona i zaufana przez przeglądarki
- SEO i ranking w wyszukiwarkach się poprawią
