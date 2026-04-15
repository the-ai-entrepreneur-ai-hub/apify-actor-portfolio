# Dental Practice Lead Finder - Complete Patient Acquisition Leads

Find dental practices that need marketing help. Get practice contacts, validated emails, social profiles, and lead scores ranked by opportunity size. Built for dental marketing agencies, dental supply reps, practice management consultants, and dental software companies.

## What You Get

Search for any dental specialty in any city and receive a scored lead list:

- **Practice data** from Google Maps (name, address, phone, rating, reviews, hours, specialty)
- **Contact enrichment** (office emails, social profiles, website tech stack)
- **Email validation** (every email checked before you send)
- **Dental-specific lead scoring** (0 to 100, tuned for dental industry signals)
- **Ranked output** sorted by opportunity, ready for outreach

## Who This Is For

**Dental marketing agencies** looking for practices that need better online presence, SEO, or patient acquisition campaigns.

**Dental supply companies** building territory lists of practices to visit or call.

**Practice management consultants** identifying practices with signs of operational gaps (outdated websites, low review counts, missing online booking).

**Dental software companies** finding practices that still use paper scheduling or lack modern patient management tools.

## Example Searches

| Search Query | What You Find |
|-------------|---------------|
| dentists in Miami FL | General practices in Miami metro |
| orthodontists in Los Angeles | Ortho specialists across LA |
| cosmetic dentistry Chicago | Cosmetic-focused practices in Chicago |
| pediatric dentist Austin TX | Kids dental practices in Austin |
| dental implants Houston | Implant specialists in Houston |
| emergency dentist Phoenix AZ | After-hours and emergency dental providers |

## How It Works

```
Search query  -->  Google Maps scrape  -->  Website enrichment  -->  Email validation  -->  Scored lead list
                   (20+ practices)         (emails, socials)       (deliverability)      (ranked 0 to 100)
```

1. Scrapes Google Maps for dental practices matching your query using a real browser
2. Visits each practice website to extract emails, social profiles, and tech stack
3. Validates every email address for deliverability
4. Scores and ranks each practice using dental-specific criteria

## Dental-Specific Lead Scoring

Every practice gets a score from 0 to 100. The scoring is calibrated for dental: lower review thresholds (dental practices get fewer reviews than restaurants), bonus points for online booking signals.

| Signal | Points |
|--------|--------|
| Has phone number | +15 |
| Has website | +15 |
| Has email address | +20 |
| Email validated as deliverable | +10 |
| Rating 4.0 or higher | +15 |
| Rating 4.5 or higher | +5 bonus |
| More than 30 reviews | +10 |
| More than 75 reviews | +5 bonus |
| Has social profiles | +5 |
| Website mentions appointment/booking | +10 |

A score of 75+ means the practice has solid contact data, good reputation, and active patient acquisition. These are your best outreach targets.

Practices scoring 40 to 60 with missing emails or no social profiles often have the biggest gap between their clinical quality and their marketing. These are the practices most likely to say yes to marketing services.

## Input

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| searchQuery | string | required | Dental search query with location. Example: "dentists in Miami FL" |
| maxResults | integer | 20 | Maximum practices to scrape (1 to 100) |
| enrichWebsites | boolean | true | Enrich each practice with website contact data |
| validateEmails | boolean | true | Validate all discovered emails |
| minRating | number | 0 | Only include practices with this rating or higher |

### Example Input

```json
{
    "searchQuery": "dentists in Miami FL",
    "maxResults": 20,
    "enrichWebsites": true,
    "validateEmails": true,
    "minRating": 3.5
}
```

## Output

Each practice in the output contains:

```json
{
    "rank": 1,
    "leadScore": 92,
    "practiceName": "Coral Gables Smiles Dentistry",
    "vertical": "dental",
    "category": "Dentist",
    "address": "2801 Coral Way, Miami, FL 33145",
    "phone": "+1-305-444-0192",
    "website": "https://coralgablessmiles.com",
    "rating": 4.9,
    "reviewCount": 187,
    "hours": "Mon to Fri 8AM to 6PM, Sat 9AM to 2PM",
    "googleMapsUrl": "https://maps.google.com/...",
    "emails": [
        {
            "email": "front@coralgablessmiles.com",
            "valid": true,
            "score": 0.92
        }
    ],
    "socialProfiles": {
        "facebook": "https://facebook.com/coralgablessmiles",
        "instagram": "https://instagram.com/coralgablessmiles"
    },
    "enrichment": {
        "industry": "Healthcare",
        "technologies": ["WordPress", "Mailchimp", "Dentrix"],
        "description": "Full service dental practice offering cosmetic dentistry, implants, and Invisalign. Book appointment online."
    },
    "enrichedAt": "2026-04-14T10:30:00.000Z"
}
```

## Pricing

**$39 per search** - less than the cost of acquiring one new dental patient.

The average dental patient is worth $1,000 to $1,500 per year to a practice. If your outreach from one search converts even a single practice into a client, the return pays for hundreds of searches.

| Method | Cost per search | Time |
|--------|----------------|------|
| Manual research | $200 (4 hours at $50/hr) | 4 hours |
| Buying dental lead lists | $0.50 to $2.00 per lead (stale data) | No enrichment |
| Hiring a VA | $500/month minimum | Training required |
| **This actor** | **$39 per search** | **Fully automatic, validated data** |

## Use Cases

### Dental Marketing Agency Prospecting

Search "dentists in [city]" for every city in your target market. Filter by practices scoring 40 to 60 that have websites but no social profiles or online booking. These practices need your services the most and are easier to close than practices already investing in marketing.

### Dental Supply Territory Building

Run searches across your territory to build a complete list of practices with phone numbers and office emails. Sort by review count to prioritize established practices with higher purchasing power.

### Practice Management Consulting

Find practices with high ratings but low review counts. These are clinically strong practices that underinvest in their online presence. They are ideal consulting clients because they have revenue but lack marketing systems.

### Dental Software Sales

Search for practices and check the enrichment tech stack. Practices running outdated WordPress sites without modern scheduling tools are prime targets for practice management software demos.

## Tips for Best Results

1. **Include the state abbreviation**: "dentists in Miami FL" works better than "dentists in Miami"
2. **Search by specialty**: "orthodontists in Dallas TX" or "cosmetic dentistry Seattle" for targeted lists
3. **Use minRating of 3.5**: Filters out closed or abandoned listings
4. **Run 20 results first**: Verify the data quality before scaling to 50 or 100
5. **Export as CSV**: Download from the Dataset tab for direct CRM import

## Integrations

Export your dental leads directly to:

- Google Sheets (via Apify integration)
- Zapier (trigger on new dataset)
- Make/Integromat
- HubSpot, Salesforce, or any CRM via webhook
- CSV/JSON/Excel download

## Support

Questions or custom requirements? Reach out through the Apify Store or open an issue on GitHub.
