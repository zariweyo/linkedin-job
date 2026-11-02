# LinkedIn Job — Project Context and Development Rules

## Objective

Build a personal job discovery and analysis application that collects job postings from LinkedIn searches, stores them, and evaluates their fit against the user's professional profile using explainable AI-assisted analysis.

The purpose is to identify relevant opportunities efficiently, compare requirements, prioritize applications, and track their evolution over time. The project is intended for personal use, not redistribution of scraped datasets.

## Core capabilities

1. **Job discovery:** configurable searches by role, keywords, location, country, remote/hybrid/on-site modality, seniority and publication date. Initial focus: DevOps, AWS/Cloud Engineer, Platform Engineer and SRE roles across Spain and Europe.
2. **Collection and normalization:** capture job ID, URL, title, company, location, work modality, description, technologies, salary when explicitly advertised, dates and source. Handle missing fields and deduplicate using source identifiers.
3. **Persistence:** maintain a searchable local history, first-seen and last-seen dates, updates and application status.
4. **Filtering:** deterministic filtering for hard requirements before spending AI tokens.
5. **AI analysis:** compare offers with a user-maintained CV/profile; score fit with explicit rationale, matched/missing skills, seniority, language, relocation, work modality and compensation. Scores are heuristic, not probabilities of hiring.
6. **Personal dashboard:** browse, filter, rank, bookmark, discard and track opportunities, with links to original listings.
7. **Incremental operation:** avoid repeated processing of unchanged jobs; optionally support scheduled runs and alerts.

## Initial implementation direction

- Start with a small, modular Python application and SQLite for local storage; consider PostgreSQL only if needed.
- Use structured models, clear boundaries between ingestion, normalization, storage, scoring and presentation, and testable adapters.
- Start with a command-line workflow; introduce a web dashboard after extraction and analysis are validated.
- Keep provider-specific logic isolated so LinkedIn can be replaced or complemented with authorized job feeds, ATS APIs and company career pages.
- Prefer low-cost, deterministic analysis first; reserve LLM analysis for promising offers.
- Technology choices are initial proposals, not immutable requirements.

## LinkedIn access constraints

LinkedIn does not provide unrestricted public job-search API access. Unofficial guest endpoints and HTML pages can change, become unavailable or be subject to terms restricting automated collection. Do not assume access is authorized simply because a page is public. Respect applicable terms, privacy, robots directives and reasonable request limits. Do not implement CAPTCHA bypass, credential theft, access-control circumvention or proxy-based evasion of blocking. Provide alternative authorized sources and manual URL import when collection is unavailable.

## Quality and security

- Never commit passwords, cookies, access tokens, personal CV details or raw private account data.
- Use configuration/environment variables for secrets and local preferences; provide example configuration files with fictitious values.
- Add unit tests for parsing, deduplication, filtering and scoring.
- Preserve original offer URLs and distinguish published salary from estimates.
- Make AI assessments traceable to source requirements; do not invent missing details.

## Documentation rule — mandatory for every change

**Every project change must be reflected in this file (`codex.md`) in the same commit or pull request.** This includes additions, refactors, fixes, configuration, dependencies, data model changes, scraping behavior, AI prompts/scoring, tests, workflows and architectural decisions.

For each change:
1. Update the relevant section of this document to reflect the current implementation rather than merely describing an intention.
2. Add a concise entry to the change log below stating what changed, why, and any important compatibility or operational implications.
3. Update the roadmap and known limitations when affected.
4. Do not mark functionality as complete until it is implemented and verified.
5. If no substantive section changes, still add a change-log entry explaining the change.

These instructions apply to human contributors and AI coding agents, including Codex. Before making edits, read this file; before completing any edit, update it. Keep documentation and code consistent.

## Roadmap

- [ ] Set up Python project structure, configuration and automated tests.
- [ ] Implement a configurable source adapter and manual job-URL import.
- [ ] Parse and normalize job descriptions.
- [ ] Add SQLite persistence and deduplication.
- [ ] Implement deterministic filtering and candidate-profile configuration.
- [ ] Add explainable AI scoring with controlled costs.
- [ ] Build a dashboard and application tracking.
- [ ] Add incremental refresh and optional alerts.

## Current status

Project initialized. This document defines the intended scope and development conventions; no application functionality is implemented yet.

## Change log

### 2026-11-02 — Initial project definition
- Created `codex.md` to establish goals, architecture direction, constraints, roadmap and mandatory documentation-on-every-change policy.
