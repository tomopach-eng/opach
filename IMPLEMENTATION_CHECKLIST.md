# Implementation Checklist - SSL/HTTPS Setup

Use this checklist to enable free SSL/HTTPS for opach.online.

## ✅ Preparation Phase (Already Done)

- [x] CNAME file configured in repository
- [x] Sitemap updated to use HTTPS URLs
- [x] Documentation created
- [x] Lighthouse workflow prepared for HTTPS

## 📋 User Action Required

### Step 1: Configure DNS (30 minutes)

- [ ] Identify your DNS provider (where you registered opach.online)
- [ ] Open [DNS_CONFIGURATION_GUIDE.md](DNS_CONFIGURATION_GUIDE.md) and find your provider
- [ ] Create CNAME record:
  - Type: CNAME
  - Name: `1`
  - Value: `tomopach-eng.github.io`
- [ ] Save the DNS record
- [ ] Verify DNS propagation (wait 5-30 minutes):
  ```bash
  nslookup 1.opach.online
  ```
  Should return: `tomopach-eng.github.io`

### Step 2: Enable HTTPS in GitHub Pages (5 minutes)

- [ ] Go to repository settings: https://github.com/tomopach-eng/opach/settings/pages
- [ ] Under "Custom domain", verify: `1.opach.online` shows with ✅ green checkmark
- [ ] If DNS check failed, wait longer for propagation (up to 48 hours)
- [ ] Once DNS is verified, check the box: ☑ **Enforce HTTPS**
- [ ] GitHub will start provisioning SSL certificate

### Step 3: Wait for Certificate (Up to 24 hours)

- [ ] Check back periodically at GitHub Pages settings
- [ ] Look for message: "Your site is published at https://1.opach.online"
- [ ] Status will change from "Provisioning certificate..." to "Certificate active"

### Step 4: Verify HTTPS is Working (5 minutes)

- [ ] Visit: https://1.opach.online
- [ ] Check for 🔒 padlock icon in browser address bar
- [ ] Click padlock to view certificate details
- [ ] Verify certificate is issued by "Let's Encrypt"
- [ ] Test all subpages work with HTTPS

### Step 5: Enable Lighthouse CI (Optional)

- [ ] Edit `.github/workflows/lighthouse.yml`
- [ ] Uncomment the push trigger:
  ```yaml
  on:
    push:
      branches: [ main, master ]
    workflow_dispatch:
  ```
- [ ] Commit and push the change
- [ ] Lighthouse will run on every push to test site performance

## 🔍 Verification Commands

### Check DNS:
```bash
# Using nslookup
nslookup 1.opach.online

# Using dig
dig 1.opach.online CNAME +short

# Expected: tomopach-eng.github.io
```

### Check HTTPS:
```bash
# Test HTTPS connection
curl -I https://1.opach.online

# Should return: HTTP/2 200 with no SSL errors
```

### Check SSL Certificate:
```bash
# View certificate details
openssl s_client -connect 1.opach.online:443 -servername 1.opach.online < /dev/null | openssl x509 -noout -text | grep -A 2 "Issuer:"

# Should show: Let's Encrypt
```

## 📚 Documentation Reference

- **Main Guide:** [SSL_SETUP.md](SSL_SETUP.md) - Detailed instructions with troubleshooting
- **DNS Help:** [DNS_CONFIGURATION_GUIDE.md](DNS_CONFIGURATION_GUIDE.md) - Provider-specific guides
- **Project Info:** [README.md](README.md) - Project overview

## ⚠️ Troubleshooting

### DNS Check Fails
1. Verify CNAME record is correct
2. Wait 24-48 hours for full propagation
3. Clear your DNS cache
4. Check with online tools: https://www.whatsmydns.net

### Certificate Not Provisioning
1. Remove custom domain from GitHub Pages
2. Wait 5 minutes
3. Re-add custom domain
4. Enable "Enforce HTTPS" again

### Site Shows "Not Secure"
1. Certificate might still be provisioning (wait)
2. Check GitHub Pages settings for status
3. Verify domain matches CNAME file exactly

## 🎉 Success Criteria

Your SSL setup is complete when:
- ✅ https://1.opach.online loads without warnings
- ✅ Browser shows 🔒 padlock icon
- ✅ Certificate is from "Let's Encrypt"
- ✅ All pages work with HTTPS
- ✅ HTTP automatically redirects to HTTPS

## 📞 Need Help?

If you encounter issues:
1. Check the troubleshooting section in [SSL_SETUP.md](SSL_SETUP.md)
2. Verify DNS configuration with online tools
3. Review GitHub Pages documentation
4. Contact GitHub Support if certificate fails after 24 hours

## 🚀 After SSL is Enabled

Optional improvements:
- [ ] Update Google Search Console with HTTPS URL
- [ ] Update any external links to use HTTPS
- [ ] Monitor site with Lighthouse CI for performance
- [ ] Consider adding Content Security Policy headers

---

**Estimated Total Time:** 30 minutes of active work + up to 24 hours waiting time

**Difficulty Level:** Beginner-friendly with detailed guides

**Cost:** Free (GitHub Pages + Let's Encrypt)
