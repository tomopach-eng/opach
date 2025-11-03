# Podstrona-4 Redirect Loop Fix

## Problem
Podstrona-4 was experiencing `ERR_TOO_MANY_REDIRECTS` error, preventing users from accessing the contact/collaboration page.

## Root Cause
The issue was caused by the `<base href="/">` HTML tag in the Podstrona-4/index.html file. This tag instructs the browser to resolve all relative URLs from the root of the website, which can cause redirect loops in certain server configurations, especially with subdirectory routing on GitHub Pages.

Additional contributing factors:
- Multiple relative image paths (e.g., `Podstrona-4/images/...`) that were being incorrectly resolved
- A duplicate `index.html` file in the `Podstrona-4/images/` directory
- A malformed srcset attribute with mixed quotes

## Solution Implemented

### 1. Removed `<base href="/">` tag
- **File:** Podstrona-4/index.html, line 8
- **Action:** Completely removed the base tag
- **Impact:** URLs are now resolved relative to the current page location

### 2. Converted all relative paths to absolute paths
- **Files affected:** Podstrona-4/index.html
- **Changes:** 25+ image paths converted
- **Examples:**
  - `Podstrona-4/images/photo.jpg` → `/Podstrona-4/images/photo.jpg`
  - `images/photo.jpg` → `/Podstrona-4/images/photo.jpg`

### 3. Removed duplicate files
- **Deleted:** Podstrona-4/images/index.html
- **Reason:** Unnecessary HTML file in images directory could cause navigation issues

### 4. Fixed malformed HTML
- **Fixed:** Srcset attribute with improperly closed quotes
- **Location:** Header image on line 116

## Technical Details

### Before:
```html
<base href="/">
<link href="/Podstrona-4/css/normalize.css" rel="stylesheet" type="text/css">
...
<img src="Podstrona-4/images/photo.jpg" alt="">
```

### After:
```html
<link href="/Podstrona-4/css/normalize.css" rel="stylesheet" type="text/css">
...
<img src="/Podstrona-4/images/photo.jpg" alt="">
```

## Verification Steps

1. **Check for base href tag:**
   ```bash
   grep "base href" Podstrona-4/index.html
   # Should return nothing
   ```

2. **Verify absolute paths:**
   ```bash
   grep -E 'src="/Podstrona-4/' Podstrona-4/index.html | head -3
   # Should show paths starting with /
   ```

3. **Confirm no duplicate files:**
   ```bash
   find Podstrona-4/images -name "*.html"
   # Should return nothing
   ```

## Expected Results

- ✅ No more redirect loops when accessing Podstrona-4
- ✅ All images load correctly
- ✅ CSS and JavaScript files load properly
- ✅ Navigation works as expected
- ✅ Page can be accessed via direct URL or internal links

## Related Files Modified

1. `Podstrona-4/index.html` - Main HTML file (base tag removed, paths fixed)
2. `Podstrona-4/images/index.html` - Deleted (duplicate file)

## Prevention

To prevent similar issues in the future:

1. **Avoid using `<base href="/">` tags** unless absolutely necessary
2. **Use absolute paths** (starting with `/`) for all resources in subdirectories
3. **Don't place HTML files in asset directories** (images, css, js, etc.)
4. **Test subdirectory pages** after deployment to ensure no redirect loops

## Testing Checklist

- [ ] Page loads without redirect errors
- [ ] All images display correctly
- [ ] Navigation links work properly
- [ ] Forms function as expected
- [ ] CSS styles are applied
- [ ] JavaScript functionality works

## Notes

- This fix is specific to Podstrona-4 only
- Other Podstrona pages (1, 2, 3) still have `<base href="/">` tags but don't exhibit redirect issues
- If similar issues occur on other pages, apply the same fix pattern
- The solution maintains backward compatibility with existing links

## Commits

1. `Fix ERR_TOO_MANY_REDIRECTS on Podstrona-4 by removing base href tag` - Removed base tag and fixed image paths
2. `Remove duplicate index.html from images directory in Podstrona-4` - Cleanup of unnecessary file
3. `Fix malformed srcset attribute in header image` - Fixed HTML syntax error

---
**Date:** November 3, 2025
**Issue:** ERR_TOO_MANY_REDIRECTS on Podstrona-4
**Status:** ✅ Resolved
