# DNS Configuration Guide for Common Providers

This guide shows how to configure DNS for `1.opach.online` with popular domain registrars and DNS providers.

## Required Configuration

**You need to create a CNAME record:**
- **Type:** CNAME
- **Name/Host:** `1` (or `1.opach.online` depending on provider)
- **Value/Target:** `tomopach-eng.github.io`
- **TTL:** 3600 (or default/automatic)

---

## Provider-Specific Instructions

### 1. Cloudflare

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Select your domain `opach.online`
3. Go to **DNS** → **Records**
4. Click **Add record**
5. Fill in:
   - **Type:** CNAME
   - **Name:** `1`
   - **Target:** `tomopach-eng.github.io`
   - **Proxy status:** 🟠 DNS only (disable proxy for GitHub Pages)
   - **TTL:** Auto
6. Click **Save**

**Important:** Disable Cloudflare proxy (orange cloud) for GitHub Pages to work correctly with SSL!

---

### 2. GoDaddy

1. Log in to [GoDaddy](https://www.godaddy.com)
2. Go to **My Products** → **DNS**
3. Find your domain `opach.online`
4. Click **Manage DNS**
5. Under **Records**, click **Add**
6. Fill in:
   - **Type:** CNAME
   - **Name:** `1`
   - **Value:** `tomopach-eng.github.io`
   - **TTL:** 1 hour (or default)
7. Click **Save**

---

### 3. Namecheap

1. Log in to [Namecheap](https://www.namecheap.com)
2. Go to **Domain List** → Select `opach.online`
3. Click **Manage** → **Advanced DNS**
4. Under **Host Records**, click **Add New Record**
5. Fill in:
   - **Type:** CNAME Record
   - **Host:** `1`
   - **Value:** `tomopach-eng.github.io`
   - **TTL:** Automatic
6. Click the green checkmark to save

---

### 4. Google Domains / Google Cloud DNS

1. Log in to [Google Domains](https://domains.google.com)
2. Select your domain `opach.online`
3. Go to **DNS** in the left menu
4. Scroll to **Custom resource records**
5. Fill in:
   - **Name:** `1`
   - **Type:** CNAME
   - **TTL:** 1h
   - **Data:** `tomopach-eng.github.io`
6. Click **Add**

---

### 5. AWS Route 53

1. Log in to [AWS Console](https://console.aws.amazon.com/route53)
2. Go to **Hosted zones**
3. Select your domain `opach.online`
4. Click **Create record**
5. Fill in:
   - **Record name:** `1`
   - **Record type:** CNAME
   - **Value:** `tomopach-eng.github.io`
   - **TTL:** 300 (or default)
   - **Routing policy:** Simple routing
6. Click **Create records**

---

### 6. OVH

1. Log in to [OVH Manager](https://www.ovh.com/manager/)
2. Go to **Web Cloud** → **Domain names**
3. Select `opach.online`
4. Go to **DNS zone** tab
5. Click **Add an entry**
6. Select **CNAME**
7. Fill in:
   - **Sub-domain:** `1`
   - **Target:** `tomopach-eng.github.io.` (note the trailing dot)
   - **TTL:** default
8. Click **Next** → **Confirm**

---

### 7. DigitalOcean

1. Log in to [DigitalOcean Control Panel](https://cloud.digitalocean.com)
2. Go to **Networking** → **Domains**
3. Select `opach.online`
4. Under **Create new record**, select **CNAME**
5. Fill in:
   - **Hostname:** `1`
   - **Will direct to:** `tomopach-eng.github.io`
   - **TTL:** 3600
6. Click **Create Record**

---

### 8. Domain.com

1. Log in to [Domain.com](https://www.domain.com)
2. Go to **My Account** → **Manage Domains**
3. Select `opach.online`
4. Click **DNS & Nameservers** → **DNS Records**
5. Click **Add DNS Record**
6. Fill in:
   - **Type:** CNAME
   - **Name:** `1`
   - **Content:** `tomopach-eng.github.io`
   - **TTL:** 3600
7. Click **Add Record**

---

### 9. Hover

1. Log in to [Hover](https://www.hover.com)
2. Select your domain `opach.online`
3. Go to **DNS** tab
4. Click **Add a record**
5. Fill in:
   - **Type:** CNAME
   - **Hostname:** `1`
   - **Target:** `tomopach-eng.github.io`
6. Click **Save**

---

### 10. Other Providers

For other DNS providers, look for:
- "DNS Management" or "DNS Records" section
- Option to add a new record
- Choose "CNAME" as the record type
- Enter the subdomain and target as specified above

---

## Verification

After adding the CNAME record, verify it's working:

### Using nslookup (Windows/Mac/Linux):
```bash
nslookup 1.opach.online
```

Expected output should show:
```
1.opach.online canonical name = tomopach-eng.github.io.
```

### Using dig (Mac/Linux):
```bash
dig 1.opach.online CNAME +short
```

Expected output:
```
tomopach-eng.github.io.
```

### Online Tools:
- [DNS Checker](https://dnschecker.org/) - Check propagation worldwide
- [What's My DNS](https://www.whatsmydns.net/) - Global DNS propagation checker
- [MXToolbox](https://mxtoolbox.com/DNSLookup.aspx) - DNS lookup tool

---

## Propagation Time

- **Local ISP:** 5 minutes - 2 hours
- **Worldwide:** 24-48 hours (worst case)
- **Most cases:** 1-4 hours

**Tip:** Clear your browser cache and DNS cache after changes:
- **Windows:** `ipconfig /flushdns`
- **macOS:** `sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder`
- **Linux:** `sudo systemd-resolve --flush-caches`

---

## Troubleshooting

### Issue: DNS not propagating
- Wait longer (up to 48 hours)
- Check if you saved the DNS record correctly
- Try from a different network or device
- Use incognito/private browsing mode

### Issue: "Too many CNAME records"
- Ensure you only have ONE CNAME record for subdomain `1`
- Remove any conflicting A, AAAA, or other CNAME records for `1.opach.online`

### Issue: Cloudflare proxy interfering
- Disable Cloudflare proxy (orange cloud → gray cloud)
- GitHub Pages cannot work with Cloudflare proxy enabled

---

## After DNS is Configured

Once DNS is working:
1. Go to [GitHub Pages Settings](https://github.com/tomopach-eng/opach/settings/pages)
2. Verify the custom domain shows `1.opach.online` with a green checkmark
3. Enable **"Enforce HTTPS"** checkbox
4. Wait for SSL certificate provisioning (up to 24 hours)
5. Visit `https://1.opach.online` to verify it works!

See [SSL_SETUP.md](SSL_SETUP.md) for detailed instructions.
