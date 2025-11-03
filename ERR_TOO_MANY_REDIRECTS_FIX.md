# Fix for ERR_TOO_MANY_REDIRECTS on opach.online

## Problem Statement
The website **opach.online** was experiencing the error:
```
Ta strona nie działa
Strona opach.online spowodowała zbyt wiele przekierowań.
Usuń pliki cookie.
ERR_TOO_MANY_REDIRECTS
```

This issue was preventing users from accessing pages on the website, particularly the Podstrona subpages.

## Root Cause
The **`<base href="/">`** HTML tag in multiple pages was causing redirect loops in the GitHub Pages hosting environment. This tag instructs the browser to resolve all relative URLs from the root of the website, which creates conflicts with subdirectory routing on GitHub Pages.

### Technical Details
When a page like `/Podstrona-1/` is accessed:
1. The browser loads `/Podstrona-1/index.html`
2. The `<base href="/">` tag tells the browser to resolve all URLs from `/`
3. This causes relative links and resources to be resolved incorrectly
4. The server attempts to redirect to correct the path
5. The redirect creates a loop, resulting in ERR_TOO_MANY_REDIRECTS

## Solution
Remove the `<base href="/">` tag from all pages and ensure all resource paths are absolute (starting with `/`).

## Pages Fixed

### Podstrona-1 (Kim jesteśmy?)
- **File:** `Podstrona-1/index.html`
- **Line 9:** Removed `<base href="/">`
- **Image paths:** Converted 8 relative paths from `../images/` to `/images/`

### Podstrona-2 (Inspiracje)
- **File:** `Podstrona-2/index.html`
- **Line 9:** Removed `<base href="/">`
- **Image paths:** Converted 10 relative paths from `../images/` to `/images/`

### Podstrona-3 (Poradniki)
- **File:** `Podstrona-3/index.html`
- **Line 9:** Removed `<base href="/">`
- **Image paths:** Converted 7 relative paths from `../images/` to `/images/`

### Podstrona-4 (Kontakt i współpraca)
- **File:** `Podstrona-4/index.html`
- **Status:** Already fixed in previous commit (see PODSTRONA4_REDIRECT_FIX.md)

## Changes Made

### Before:
```html
<head>
  <meta content="Webflow" name="generator">
  <base href="/">
  <link href="/Podstrona-1/css/normalize.css" rel="stylesheet" type="text/css">
  ...
  <img loading="lazy" src="../images/photo.png" alt="">
</head>
```

### After:
```html
<head>
  <meta content="Webflow" name="generator">
  <link href="/Podstrona-1/css/normalize.css" rel="stylesheet" type="text/css">
  ...
  <img loading="lazy" src="/images/photo.png" alt="">
</head>
```

## Verification Steps

### 1. Confirm base href tags are removed:
```bash
grep -r "base href" --include="*.html" .
# Should return nothing
```

### 2. Verify no relative paths remain:
```bash
grep -E 'src="\.\.|href="\.\.' Podstrona-*/index.html
# Should return nothing
```

### 3. Check absolute paths are correct:
```bash
grep -E 'href="/Podstrona-|src="/images/' Podstrona-1/index.html
# Should show all paths starting with /
```

## Expected Results

After deploying these changes, the website should:

- ✅ Load all pages without redirect errors
- ✅ Display all images correctly
- ✅ Maintain proper navigation between pages
- ✅ Load CSS and JavaScript resources correctly
- ✅ Work correctly on GitHub Pages with custom domain (opach.online)

## Testing

Once deployed to GitHub Pages:

1. **Test each page directly:**
   - https://opach.online/
   - https://opach.online/Podstrona-1/
   - https://opach.online/Podstrona-2/
   - https://opach.online/Podstrona-3/
   - https://opach.online/Podstrona-4/

2. **Verify navigation:**
   - Click through all navigation links
   - Ensure no redirect loops occur
   - Confirm all pages load within 2-3 seconds

3. **Check resources:**
   - Open browser developer tools (F12)
   - Navigate to Network tab
   - Verify all resources (CSS, JS, images) load with 200 status codes
   - Ensure no 404 or redirect errors

4. **Clear cookies and cache:**
   - Test with fresh browser session
   - Verify no cached redirect issues

## Prevention Guidelines

To prevent this issue in the future:

### ❌ Don't Do:
- Don't use `<base href="/">` tags in subdirectory pages
- Don't use relative paths like `../images/` or `images/` in subdirectories
- Don't place HTML files in asset directories

### ✅ Do:
- Use absolute paths starting with `/` for all resources
- Test subdirectory pages locally before deployment
- Review HTML for base tags when troubleshooting redirect issues
- Keep documentation updated when making path changes

## Files Modified

| File | Changes | Lines Changed |
|------|---------|---------------|
| `Podstrona-1/index.html` | Removed base tag, fixed 8 image paths | 17 |
| `Podstrona-2/index.html` | Removed base tag, fixed 10 image paths | 21 |
| `Podstrona-3/index.html` | Removed base tag, fixed 7 image paths | 15 |
| **Total** | | **53** |

## Related Documentation

- [PODSTRONA4_REDIRECT_FIX.md](./PODSTRONA4_REDIRECT_FIX.md) - Previous fix for Podstrona-4
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [MDN: base element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base)

## Commit History

1. `Remove base href tags and fix relative paths in all Podstrona pages` - Main fix commit
2. `Initial analysis of ERR_TOO_MANY_REDIRECTS issue` - Analysis and planning

## Notes

- This fix applies the same solution that was previously used for Podstrona-4
- The main index.html does not have a base href tag, so it was not affected
- All CSS and JavaScript files already use absolute paths
- The CNAME file is correctly configured with `opach.online`

---

**Date:** November 3, 2025  
**Issue:** ERR_TOO_MANY_REDIRECTS across all Podstrona pages  
**Status:** ✅ Fixed and ready for deployment
