# VECVO — Longevity Science Research Hub

Evidence-based documentation of aging biology, lifespan-extending interventions, and translational research.

## Overview

VECVO is an academic research compilation project focused on systematic documentation of:
- The 12 hallmarks of aging (López-Otín et al. 2023 framework)
- Pharmacological, cellular, and lifestyle interventions with human evidence
- Historical research timeline and key publications
- Translational barriers between model organisms and humans

**Core principles:**
- Evidence hierarchy explicitly stated
- Honest uncertainty acknowledgment
- No hype language or speculative claims
- Primary literature citations for all claims
- Maintained by Alice Frolov (ORCID: 0009-0006-2567-1734)

## Project Structure

```
vecvo-hub/
├── vecvo-hub.html              # Main website (standalone)
├── interventions-database.json # Structured intervention data
├── papers-database.json        # Key publications database
├── README.md                   # This file
└── assets/ (future)
    ├── images/
    ├── icons/
    └── pdf/
```

## File Descriptions

### `vecvo-hub.html`
Standalone HTML file with embedded CSS and JavaScript. No build process required.

**Sections:**
- Hero: Mission statement and project metadata
- Hallmarks: 12 hallmarks of aging with evidence badges
- Interventions: Pharmacological, cellular, lifestyle, experimental (tabbed interface)
- Timeline: Historical milestones (1935-2025) with citations
- Publications: Open-access research notes and OSF integration
- About: Project methodology and maintainer info

**Features:**
- Fully responsive (mobile-first design)
- Smooth scroll navigation
- Tab-based intervention filtering
- Evidence level badges (high/medium/low/preliminary)
- Clean academic aesthetic (EB Garamond + JetBrains Mono)

### `interventions-database.json`
Structured data for all documented interventions.

**Schema:**
```json
{
  "id": "unique-identifier",
  "name": "Intervention Name",
  "category": "pharmacological|cellular|lifestyle|experimental",
  "mechanism": {
    "primary": "Main mechanism",
    "secondary": ["Supporting mechanisms"],
    "pathway": "Relevant hallmark"
  },
  "evidence": {
    "mouse": {
      "effect_size": "Quantified result",
      "studies": [{citation, result, quality}],
      "evidence_level": "high|moderate|low"
    },
    "human": {
      "status": "Trial status",
      "trials": [{nct, name, status}],
      "evidence_level": "..."
    }
  },
  "safety": {
    "profile": "Safety summary",
    "concerns": ["Risk 1", "Risk 2"],
    "long_term_data": "Duration of safety data"
  },
  "practical": {
    "dosing": "Protocol",
    "cost": "Estimate",
    "accessibility": "How to obtain"
  },
  "translation_gap": "none|moderate|high|very_high",
  "recommendation": "Evidence-based assessment"
}
```

**Current interventions:** 9 (rapamycin, metformin, NAD+, senolytics, exercise, caloric restriction, partial reprogramming, young plasma, more to be added)

### `papers-database.json`
Key publications in longevity research.

**Schema:**
```json
{
  "id": "author-year",
  "title": "Paper title",
  "authors": ["Author 1", "Author 2"],
  "journal": "Journal name",
  "year": 2023,
  "doi": "10.xxxx/xxxxx",
  "pmid": "12345678",
  "type": "review|research_article|cohort_study|clinical_trial",
  "evidence_level": "landmark|very_high|high|moderate|preliminary",
  "key_findings": ["Finding 1", "Finding 2"],
  "abstract": "Full abstract text",
  "vecvo_notes": "Contextual assessment",
  "tags": ["tag1", "tag2"]
}
```

**Current papers:** 12 landmark studies (hallmarks framework, rapamycin ITP, Kenyon age-1, Horvath clock, senolytics, partial reprogramming, exercise cohorts, TRIIM trial)

## Deployment Options

### Option 1: Static Hosting (Simplest)
Host `vecvo-hub.html` on any static hosting service.

**GitHub Pages:**
```bash
# Create repository
gh repo create vecvo-longevity-hub --public

# Add files
git add vecvo-hub.html interventions-database.json papers-database.json
git commit -m "Initial commit: Academic longevity research hub"
git push origin main

# Enable GitHub Pages
# Settings → Pages → Source: main branch → Save
# Site will be live at: https://[username].github.io/vecvo-longevity-hub/vecvo-hub.html
```

**Netlify/Vercel:**
```bash
# Drag and drop vecvo-hub.html to Netlify dashboard
# Or: Connect GitHub repo and auto-deploy
# Custom domain: vecvo.com
```

### Option 2: Dynamic Site with Data (Better)
Convert to Next.js/React for dynamic data loading and better SEO.

**Benefits:**
- Load interventions from JSON dynamically
- Search/filter functionality
- Server-side rendering for SEO
- Easier content updates

**Implementation outline:**
```bash
npx create-next-app vecvo-hub
cd vecvo-hub

# Copy JSON files to /public/data/
# Create components for each section
# Fetch JSON data at build time
# Deploy to Vercel with one command
```

### Option 3: Full CMS Integration (Best for Scale)
Use headless CMS for content management.

**Recommended stack:**
- Next.js frontend
- Sanity.io or Strapi for CMS
- Vercel deployment
- OSF API integration for publications

**Benefits:**
- Non-technical content updates
- Versioning and editorial workflow
- Automatic paper import from PubMed/OSF
- Collaborative editing

## Content Update Workflow

### Adding New Interventions
1. Research primary literature
2. Assess evidence quality (mouse, human, safety)
3. Add entry to `interventions-database.json`
4. Update HTML table/cards in `vecvo-hub.html`
5. Commit with citation

### Adding New Papers
1. Identify landmark/high-impact paper
2. Extract metadata (DOI, PMID, authors, etc.)
3. Add entry to `papers-database.json`
4. Update Publications section if featured
5. Commit with proper attribution

### Updating Evidence Levels
When new trials complete:
1. Update relevant intervention evidence section
2. Add trial NCT and results
3. Adjust evidence_level if warranted
4. Update recommendation based on new data
5. Note last_updated timestamp

## Future Enhancements

### Phase 1: Enhanced Interactivity
- [ ] JavaScript-powered intervention filtering (by evidence level, category)
- [ ] Search functionality for papers and interventions
- [ ] Sortable evidence table
- [ ] Expandable intervention details

### Phase 2: Data Automation
- [ ] PubMed API integration for auto-updating citations
- [ ] ClinicalTrials.gov API for trial status tracking
- [ ] OSF API for automatic publication imports
- [ ] Scheduled weekly data refreshes

### Phase 3: Advanced Features
- [ ] Interactive citation network visualization (D3.js)
- [ ] Evidence strength calculator (custom algorithm)
- [ ] Personalized intervention recommendations (with disclaimers)
- [ ] Comparison tool (intervention A vs B side-by-side)

### Phase 4: Community Features
- [ ] GitHub issues for corrections/suggestions
- [ ] Contributor guidelines
- [ ] Public changelog
- [ ] API for programmatic access to databases

## Evidence Level System

**Very High:** Multiple large RCTs or highly consistent cohort studies  
**High:** Well-designed RCTs or large observational studies  
**Moderate:** Limited RCT data or smaller cohort studies  
**Low:** Animal data only or very limited human data  
**Preliminary:** Early-stage research, surrogate endpoints, or small n

## Translation Gap Assessment

**None:** Direct human evidence; no model organism translation required  
**Moderate:** Some human data; animal models supportive  
**High:** Strong animal data; limited or absent human data  
**Very High:** Dramatic animal results; human translation questionable or failed

## Content Standards

### All Claims Must:
- Be referenced to primary literature (DOI or PMID)
- State evidence level explicitly
- Acknowledge uncertainty where it exists
- Distinguish correlation from causation
- Note limitations and confounders

### Forbidden Language:
- "Cure aging" / "defeat death" / "immortality"
- "Breakthrough" without justification
- Definitive claims about unproven interventions
- Marketing language or product endorsements
- Speculation presented as fact

### Required Disclosures:
- Conflicts of interest (none currently)
- Funding sources (unfunded personal project)
- Data limitations and gaps
- Translation uncertainty from animal models

## Contribution Guidelines

Contributions welcome via:
1. GitHub issues (corrections, updates, suggestions)
2. Pull requests (with supporting citations)
3. Email: [contact via vecvo.com]

**Criteria for inclusion:**
- Peer-reviewed publication in reputable journal
- Mechanistic understanding or clinical relevance
- Contribution to hallmarks framework understanding
- Novel intervention with preliminary evidence
- Important negative result (e.g., failed translation)

**Review process:**
- Evidence quality assessment
- Citation verification
- Clarity and accuracy review
- Integration with existing content
- Acknowledgment of contributor

## License

**Content:** Creative Commons Attribution 4.0 (CC BY 4.0)  
**Code:** MIT License  
**Databases:** CC0 (public domain dedication)

You may:
- Use, modify, and distribute content with attribution
- Build upon databases for any purpose
- Fork and create derivative works

Attribution: "VECVO — Alice Frolov — vecvo.com"

## Contact

**Maintainer:** Alice Frolov  
**ORCID:** [0009-0006-2567-1734](https://orcid.org/0009-0006-2567-1734)  
**OSF:** [Profile link]  
**Website:** [vecvo.com](https://vecvo.com)  
**LinkedIn:** [Profile link]

## Acknowledgments

Framework based on:
- López-Otín C et al. Hallmarks of aging: An expanding universe. Cell. 2023;186(2):243-278.
- NIH Interventions Testing Program
- Open access longevity research community

---

**Last Updated:** March 29, 2026  
**Version:** 1.0  
**Status:** Active development