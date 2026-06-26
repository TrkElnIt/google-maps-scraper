# Google Maps Business Intelligence Scraper

## Overview

This project is a browser automation and data extraction system for building structured lead and market research datasets from Google Maps search results. It was designed for cases where a business needs repeatable local research across keywords, cities, and service categories instead of manually opening listings one by one.

The scraper collects visible business listing data, normalizes inconsistent listing text, and exports clean CSV or JSON records that can be reviewed, filtered, enriched, or imported into a CRM workflow.

## Problem

Google Maps listings are useful for local business research, but the data is presented as dynamic browser content. Search results load progressively, listing cards vary by business type, and details such as phone numbers, opening hours, review counts, websites, and addresses do not always appear in the same format.

The goal was to turn this dynamic page into a structured dataset with enough detail to support lead qualification and follow-up workflows.

## What The System Extracts

The project focuses on structured business fields:

- Business name
- Rating
- Review count
- Category
- Address or visible location
- Opening hours text
- Phone number
- Website URL
- Search keyword and region context
- CSV and JSON exports

It also supports a website enrichment step that can visit linked business websites and extract useful public information such as contact pages, emails, social links, service keywords, and team/about-page signals.

## Technical Work Built

The implementation uses Playwright to drive a real browser session, submit the Google Maps query, wait for the results feed, scroll the list until results are loaded, and capture the result HTML.

The parser uses BeautifulSoup and deterministic extraction rules to handle listing cards and detail pages. It includes fallback logic for common Google Maps patterns, including star-rating aria labels, review counts in parentheses, phone-number cleanup, address/hour splitting, and category/location detection.

For structuring messy listing text, the project includes a local LLM workflow using Ollama. The local model can convert raw snippets into a strict JSON schema while avoiding external API dependency for every batch. When the LLM call fails or returns invalid JSON, the scraper falls back to deterministic HTML parsing.

The pipeline is designed around batches, normalized records, and file outputs so it can be extended later into a database import, CRM enrichment job, or lead-scoring workflow.

## Engineering Decisions

- Use Playwright because Google Maps is dynamic and search results are loaded by browser interaction.
- Keep deterministic parser fallbacks so the scraper still produces useful records when the LLM step fails.
- Use a local Ollama model option to reduce API cost and keep the data-cleaning loop under local control.
- Export CSV and JSON so the data can be inspected manually before being imported into another system.
- Keep raw scraped output and credentials out of the public repository.

## Example Use Cases

- Local lead research for service businesses
- Market mapping by city and keyword
- Competitor list building
- CRM lead enrichment
- Website contact discovery
- Review and rating based prioritization

## Safety And Scope

This repository is a sanitized portfolio overview. It does not include credentials, raw scraped datasets, customer data, or private configuration. The system is intended for controlled research and internal data preparation, not spam or credential bypass.

