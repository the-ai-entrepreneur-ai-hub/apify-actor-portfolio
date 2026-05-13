
# Seven new Apify actors in two days

Two day sprint. Codex did the per-actor source code, I orchestrated and verified each one against real data. All seven live on Apify Store. Pay per event pricing activates 2026-05-26.

Each one targets a specific buyer category with a real budget. Not generic scrapers, not toy demos. Numbers on what each one does and which buyers should care.

## 1. Hospital Price Transparency MRF Normalizer

[Store link](https://apify.com/george-the-developer/hospital-mrf-normalizer)

CMS enforcement of the hospital price transparency rule tightened in April 2026. Every US hospital publishes a machine readable file of negotiated rates by payer and procedure, but the files are gigantic and inconsistent. CMS v2 JSON, CMS v3 JSON, CSV with column drift between hospitals.

This actor wraps the parsing into one Standby API. Detects format automatically (gzip, JSON, CSV), streams the file, normalizes each row to one schema with payer, plan, billing code, code type, negotiated rate, methodology, expiration date.

Pricing: $0.50 per start, $0.002 per rate row, $0.02 per provider procedure payer bundle.

Verified live test: Cooper University Hospital CSV returned 13 normalized rows including Aetna Better Health at code 0042T (HCPCS) for $272.44 negotiated.

Buyers: health cost transparency platforms (Amino, Cedar, Healthcare Bluebook), employer benefits tools (Castlight, Garner, Transcarent), TPA and PPO operators (Zelis, MultiPlan).

## 2. MCP Server Registry and Security Scorer

[Store link](https://apify.com/george-the-developer/mcp-server-registry-scorer)

Anthropic Model Context Protocol exploded past 22,000 servers indexed on Glama. Agent platforms admitting MCP servers do it by README and stars and hope.

This actor joins the official Anthropic registry with npm package metadata (downloads, first published date, maintainer count), GitHub repo data (stars, archived, last commit, open issues), and produces a deterministic risk score per server. Signals: missing repo, archived, stale 90 days, unknown publisher, no license, weird tool count, registered but never built, single maintainer npm, advisory match.

Score lands 0 to 100 in bands low, medium, high, critical. Same input always returns same score, no LLM in the loop.

Pricing: $0.50 per start, $0.025 per server profile, $0.15 per full security scan.

Verified live test: `ac.inference.sh/mcp` server flagged risk 70 (high) because no repo link, no license, unknown publisher, remote only transport.

Buyers: agent platform admission control (Docker MCP Toolkit, Cursor, Continue, Windsurf), enterprise AI governance teams, MCP marketplace ranking signals, dev tool risk dashboards.

## 3. FDA Warning Letter and Enforcement Monitor

[Store link](https://apify.com/george-the-developer/fda-warning-letter-monitor)

FDA published warning letters on a static index page that everyone in regulated industries needs to read but nobody wants to scrape. The April 2026 GLP-1 and telehealth enforcement push made this even more urgent.

This actor pulls the full letter feed, classifies each letter by topic (GLP-1, telehealth, compounding, manufacturing, biologics, food, advertising, dietary supplement), extracts the recipient company and product line, and rolls everything up into a company level risk brief with letter count, topic mix, time since last letter, and severity signals.

Pricing: $1 per start, $0.30 per letter, $1.50 per company risk brief.

Verified live test: CareFusion 213 LLC returned risk band "high" with 4 open enforcement actions tied to manufacturing.

Buyers: FDA consultants (Redica, Greenleaf Health, ProPharma, RQM Plus, The FDA Group), pharma QA SaaS (AssurX, Sparta, Kneat), med-device legal, telehealth ops.

## 4. Clinical Trial Investigator and Site Intelligence

[Store link](https://apify.com/george-the-developer/clinical-trial-investigator-intel)

CROs and sponsors at any scale rebuild the same data join for every new study. ClinicalTrials.gov plus NPI Registry plus OpenPayments plus PubMed publication count plus geo cluster of sites. The data is public, the join is mechanical, but everyone rebuilds it in a half maintained Python script.

This actor wraps the join into one Standby API. Query by condition or NCT id, get investigator profiles with NPI, OpenPayments dollar totals by company, publication counts, trial history broken down by phase, and a deterministic site fit score for each location.

Pricing: $1 per start, $0.10 per investigator profile, $0.50 per site fit row.

Verified live test: glioblastoma phase 2 query returned Thomas J Kaley MD at Memorial Sloan Kettering with NPI 1578721858, full therapeutic area list, and complete trial history.

Buyers: top 5 CROs (IQVIA, ICON, Parexel, Medidata, Veeva), clinical site networks (Advarra, Clinitiative), patient recruitment platforms (LINEA), sponsor BD teams.

## 5. Federal Contract Opportunity Monitor

[Store link](https://apify.com/george-the-developer/federal-contract-opportunity-monitor)

SAM.gov publishes federal contract opportunities hourly. USAspending publishes awarded contracts with recipient data. Joining them and tagging by topic is the daily grind for federal sales teams and GovCon advisors. Bloomberg Government and Govini do this at enterprise pricing.

This actor pulls SAM.gov internal search (no API key required) plus USAspending POST endpoint, normalizes both into one schema, tags opportunities by topic keyword (configurable per user), and produces partnership leads: which prime contractors won similar work recently and at what value.

Pricing: $1 per start, $0.10 per opportunity, $0.50 per partnership lead.

Verified live test: `/leads?keyword=consulting&awarded_amount_min=100000` returned General Dynamics IT with 2 recent awards totaling $1.7 billion, lead band "priority", top buying agency Department of State.

Buyers: GovCon advisors (Govini, Deltek, EZGovOpps), federal sales teams at MSPs and consulting firms, subcontract introduction services, state and local procurement intel.

## 6. LLM Provider Price and Latency Monitor

[Store link](https://apify.com/george-the-developer/llm-provider-price-latency-monitor)

LLM gateways and agent platforms route across 5 to 10 providers. Pricing changes weekly. OpenRouter aggregates in a UI but does not publish it as a clean JSON ingestion feed. Most teams maintain their own scraper.

This actor wraps OpenRouter as canonical (200+ models, no auth), falls back to scraping OpenAI, Anthropic, Together, and Groq pricing pages when a model is missing, and returns a normalized snapshot per model with prompt and completion price per 1M tokens, context length, capability flags (vision, tools, JSON mode), and provider routing list.

A second endpoint produces cross provider benchmark rows: same model family, multiple providers, cost per 1k chat pair, multiplier from cheapest to most expensive.

Pricing: $0.50 per start, $0.025 per model snapshot, $0.15 per benchmark row.

Verified live test: `/models?provider=anthropic&limit=3` returned 3 Anthropic models with full pricing populated. Benchmark endpoint returned 2 cross provider rows with cheapest_provider field.

Buyers: LLM gateway operators (Portkey, Helicone, LiteLLM), agent platform model admission, FinOps cost per task budgeting, AI engineering team weekly digests.

## 7. Multi City Building Permit Aggregator

[Store link](https://apify.com/george-the-developer/multi-city-building-permit-aggregator)

Each US city publishes building permit data in its own JSON shape. NYC moved their authoritative feed from the old DOB Issuance dataset to DOB NOW in 2024 and broke every scraper that hardcoded the old IDs.

This actor wraps NYC and Chicago open data portals into one schema. Per permit you get permit type, status, work type, estimated cost, address with GPS, ZIP, block lot, builder business name, builder license, property business name. A second endpoint produces a builder activity roundup for any business name.

Pricing: $1 per start, $0.05 per permit row, $0.30 per builder activity roundup.

Verified live test: COSTELLO CONSTRUCTION roundup returned 88 permits over 3 years for $3 million total value, top property businesses served (Flushing Hospital Medical Center, Jerome Avenue SM Realty LLC), top permit types, top ZIP codes, activity tier "high volume".

Buyers: construction supply distributors planning territories, contractor SaaS lead enrichment (ServiceTitan, Jobber, Buildertrend), real estate investor research, market research firms.

## What activation looks like

Pricing activates 2026-05-26 for the first 5 actors and 2026-05-27 for the last 2. Until then runs are free for testers who want to validate the schema.

If any of the buyer categories above describes your work, drop a free trial test at the contact info in each Store listing. Sample data on one company or condition of your choice gets returned within the day.

If you want to follow what each actor earns at first activation, the monthly digest goes out via [@ai_in_it on X](https://x.com/ai_in_it) and the [apify-actor-portfolio repo](https://github.com/the-ai-entrepreneur-ai-hub/apify-actor-portfolio).

George
[george.the.developer on Apify](https://apify.com/george-the-developer)
