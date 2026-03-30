# VECVO Deployment Guide

Complete walkthrough for deploying your longevity research hub to the web.

## Prerequisites

- GitHub account
- Domain name (vecvo.com) - already purchased via Namecheap
- Git installed on your computer
- Text editor (VS Code recommended)

---

## Option 1: GitHub Pages (Recommended First Step)

### Step 1: Create GitHub Repository

```bash
# Navigate to your projects folder
cd ~/projects

# Create new directory
mkdir vecvo-longevity-hub
cd vecvo-longevity-hub

# Initialize git
git init
git branch -M main

# Create repository on GitHub
# Go to https://github.com/new
# Repository name: vecvo-longevity-hub
# Public repository
# Don't initialize with README (we already have files)
```

### Step 2: Add Your Files

```bash
# Copy the three main files into the repository folder:
# - vecvo-hub.html
# - interventions-database.json
# - papers-database.json
# - README.md

# Add all files
git add .

# Commit
git commit -m "Initial commit: Academic longevity research hub

- Evidence-based hallmarks of aging documentation
- Interventions database (pharmacological, cellular, lifestyle)
- Key papers database with citations
- Clean academic design with proper evidence hierarchy"

# Link to your GitHub repository
git remote add origin https://github.com/[YOUR-USERNAME]/vecvo-longevity-hub.git

# Push to GitHub
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (top right)
3. Click **Pages** (left sidebar)
4. Under "Source":
   - Branch: `main`
   - Folder: `/ (root)`
   - Click **Save**
5. Wait 2-3 minutes
6. Your site will be live at:  
   `https://[YOUR-USERNAME].github.io/vecvo-longevity-hub/vecvo-hub.html`

### Step 4: Test Your Site

Visit the URL and verify:
- [ ] Page loads correctly
- [ ] Navigation works (click each section link)
- [ ] Tabs switch properly (Interventions section)
- [ ] Mobile view displays correctly
- [ ] All fonts load (EB Garamond, JetBrains Mono)

---

## Option 2: Custom Domain (vecvo.com)

You already own vecvo.com via Namecheap. Here's how to point it to GitHub Pages.

### Step 1: Configure GitHub Pages for Custom Domain

1. In your repository, go to **Settings → Pages**
2. Under "Custom domain", enter: `vecvo.com`
3. Click **Save**
4. GitHub will create a `CNAME` file in your repository
5. Check "Enforce HTTPS" (after DNS propagates, ~24 hours)

### Step 2: Configure Namecheap DNS

1. Log in to Namecheap
2. Find vecvo.com in your domain list
3. Click **Manage**
4. Go to **Advanced DNS** tab
5. Delete any existing A/CNAME records for `@` and `www`

6. Add these records:

**For root domain (vecvo.com):**
```
Type: A Record
Host: @
Value: 185.199.108.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.109.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.110.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.111.153
TTL: Automatic
```

**For www subdomain (www.vecvo.com):**
```
Type: CNAME Record
Host: www
Value: [YOUR-USERNAME].github.io.
TTL: Automatic
```

7. Click **Save All Changes**

### Step 3: Wait for DNS Propagation

- DNS changes take 10 minutes to 24 hours
- Check status: https://dnschecker.org (enter vecvo.com)
- When A records point to GitHub's IPs, you're good

### Step 4: Enable HTTPS

1. After DNS propagates, go back to GitHub Pages settings
2. Check **Enforce HTTPS**
3. Wait for certificate provisioning (~10 minutes)
4. Visit `https://vecvo.com` — should work!

---

## Option 3: Netlify (Alternative to GitHub Pages)

If you want better performance and easier deployment:

### Quick Deploy

1. Go to https://app.netlify.com
2. Sign in with GitHub
3. Click **Add new site → Import an existing project**
4. Choose GitHub → Select `vecvo-longevity-hub` repository
5. Build settings:
   - Build command: (leave blank)
   - Publish directory: `/`
6. Click **Deploy site**

### Custom Domain on Netlify

1. Click **Domain settings**
2. Click **Add custom domain**
3. Enter `vecvo.com`
4. Netlify will give you nameservers
5. In Namecheap:
   - Go to **Domain → Nameservers**
   - Select "Custom DNS"
   - Paste Netlify nameservers
6. Wait for propagation (~24 hours)
7. Netlify auto-provisions SSL certificate

**Benefits over GitHub Pages:**
- Faster CDN
- Automatic HTTPS
- Better analytics
- Form handling (if you add contact form later)
- Deploy previews for branches

---

## Updating Your Site

### Method 1: Direct File Edit (Simple Changes)

On GitHub website:
1. Navigate to `vecvo-hub.html`
2. Click pencil icon (Edit)
3. Make changes
4. Click **Commit changes**
5. GitHub Pages auto-deploys in ~1 minute

### Method 2: Local Development (Major Changes)

```bash
# Make changes to files locally
# Test by opening vecvo-hub.html in browser

# Stage changes
git add .

# Commit with descriptive message
git commit -m "Update: Added fisetin to senolytic interventions

- New evidence from Mayo Clinic trial (NCT03675724)
- Updated evidence level to 'moderate'
- Added safety profile and dosing information"

# Push to GitHub
git push origin main

# Site updates automatically
```

---

## Content Update Checklist

When adding new research or updating evidence:

### For New Interventions:
- [ ] Research completed (min. 2-3 primary papers)
- [ ] Evidence quality assessed (mouse, human, safety)
- [ ] Translation gap evaluated
- [ ] Added to `interventions-database.json`
- [ ] Updated HTML section with proper badge
- [ ] All claims have citations (DOI/PMID)
- [ ] Recommendation is evidence-based and honest

### For Evidence Updates:
- [ ] New trial results verified (check ClinicalTrials.gov)
- [ ] Evidence level adjusted if warranted
- [ ] Safety profile updated if new data
- [ ] Recommendation revised based on totality of evidence
- [ ] `last_updated` timestamp changed
- [ ] Changelog note in commit message

### For New Papers:
- [ ] Paper meets inclusion criteria (peer-reviewed, impactful)
- [ ] Metadata extracted accurately
- [ ] Abstract and key findings summarized
- [ ] Added to `papers-database.json`
- [ ] Tags applied for categorization
- [ ] VECVO notes provide context and assessment

---

## SEO Optimization

### Current Meta Tags (Already Included)

```html
<title>VECVO — Longevity Science Research Hub</title>
<meta name="description" content="Systematic documentation of aging biology, lifespan-extending interventions, and translational research. Evidence-based longevity science compilation.">
```

### Recommended Additions

Add to `<head>` section:

```html
<!-- Open Graph (for social sharing) -->
<meta property="og:title" content="VECVO — Longevity Science Research Hub">
<meta property="og:description" content="Evidence-based documentation of aging biology, interventions, and translational research.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://vecvo.com">
<meta property="og:image" content="https://vecvo.com/assets/og-image.png">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="VECVO — Longevity Science Research Hub">
<meta name="twitter:description" content="Evidence-based aging biology and intervention documentation.">
<meta name="twitter:image" content="https://vecvo.com/assets/twitter-image.png">

<!-- Schema.org for Google -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "VECVO",
  "url": "https://vecvo.com",
  "description": "Evidence-based longevity science research hub",
  "author": {
    "@type": "Person",
    "name": "Alice Frolov",
    "identifier": "https://orcid.org/0009-0006-2567-1734"
  }
}
</script>
```

### Create robots.txt

In repository root, create `robots.txt`:

```
User-agent: *
Allow: /

Sitemap: https://vecvo.com/sitemap.xml
```

### Create sitemap.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://vecvo.com/</loc>
    <lastmod>2026-03-29</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

---

## Performance Optimization

### Image Optimization (When You Add Images)

```bash
# Install optimizer
npm install -g sharp-cli

# Optimize images
sharp -i original.png -o optimized.png --quality 80 --format webp
```

### Font Loading

Already optimized with:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

### Minification (Optional)

For production, minify HTML:
```bash
npm install -g html-minifier

html-minifier vecvo-hub.html \
  --collapse-whitespace \
  --remove-comments \
  --minify-css true \
  --minify-js true \
  -o vecvo-hub.min.html
```

---

## Analytics Setup (Optional)

### Google Analytics 4

1. Create GA4 property at https://analytics.google.com
2. Get Measurement ID (G-XXXXXXXXXX)
3. Add to `<head>`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### Privacy-Focused Alternative: Plausible

```html
<script defer data-domain="vecvo.com" src="https://plausible.io/js/script.js"></script>
```

**Benefits:**
- No cookies
- GDPR compliant by default
- Simple, clean interface
- $9/month for 10k pageviews

---

## Backup Strategy

### Automated Backups

GitHub already stores your code. For additional safety:

```bash
# Create automated backup script
# backup.sh

#!/bin/bash
DATE=$(date +%Y-%m-%d)
git clone https://github.com/[USERNAME]/vecvo-longevity-hub.git backup-$DATE
zip -r vecvo-backup-$DATE.zip backup-$DATE
rm -rf backup-$DATE
echo "Backup created: vecvo-backup-$DATE.zip"
```

Run monthly or after major updates.

---

## Troubleshooting

### Site Not Loading

**Check:**
1. DNS propagation complete? → https://dnschecker.org
2. GitHub Pages enabled? → Settings → Pages
3. CNAME file present? → Repository root
4. A records correct? → 185.199.108-111.153

### HTTPS Not Working

**Solutions:**
1. Wait 24 hours after DNS changes
2. Uncheck and re-check "Enforce HTTPS"
3. Clear browser cache (Ctrl+Shift+Delete)
4. Try incognito window

### Fonts Not Loading

**Check:**
1. Internet connection stable?
2. Google Fonts accessible? → Open fonts.googleapis.com
3. Console errors? → F12 → Console tab

### Mobile Display Issues

**Debug:**
1. F12 → Toggle device toolbar
2. Test various screen sizes
3. Check viewport meta tag present
4. Validate responsive CSS

---

## Next Steps After Deployment

1. **Add Your OSF Publications**
   - Update Publications section with real DOIs
   - Link to actual OSF repository

2. **Expand Interventions Database**
   - Add fisetin, spermidine, acarbose
   - More lifestyle interventions
   - Emerging cellular therapies

3. **Create Visual Assets**
   - Logo/favicon (VECVO mark)
   - OG image for social sharing
   - Scientific illustrations

4. **Build Citation Network**
   - Interactive D3.js visualization
   - Show paper connections
   - Filter by topic/year

5. **Integrate OSF API**
   - Auto-fetch your publications
   - Display latest research notes
   - Keep bibliography current

6. **Add Search Functionality**
   - Intervention search
   - Paper search
   - Tag-based filtering

---

## Support

**Issues:** https://github.com/[USERNAME]/vecvo-longevity-hub/issues  
**Email:** [your contact email]  
**ORCID:** https://orcid.org/0009-0006-2567-1734

---

**Guide Version:** 1.0  
**Last Updated:** March 29, 2026