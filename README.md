# 🗺️ Scraping & Data Extraction — Google Maps Scraper

A browser-based Python scraper that extracts detailed business data from Google Maps listings, including contact information, website, reviews, and ratings.  
Enhanced with OpenAI GPT-4.0 for parsing unstructured listing content into clean, structured fields.

---

## 💡 Features

- Extracts structured business information:
  - Name, address, phone number
  - Website
  - Ratings and review count
  - Category and location
- Scrapes dynamically loaded listings using Playwright
- Uses **OpenAI GPT-4.0 for parsing** unstructured text such as business descriptions
- Generates structured tags, service types, and clean summaries
- Saves output as CSV or JSON
- Supports keyword + location search with pagination

---

## 🛠 Technologies

- Python 3
- Playwright (browser automation)
- OpenAI GPT-4.0 for parsing and data structuring
- CSV / JSON output

---

## ⚙️ Workflow

1. Performs Google Maps search for a given keyword and region
2. Scrolls to load all results
3. Extracts visible data from each listing
4. Sends raw content to GPT-4.0 to structure key fields
5. Outputs to CSV or JSON

---

## 🔐 Access

🔒 Source code is private.  
This repository provides a public overview of the scraper’s functionality and architecture.

---

## 🧑‍💻 Author

**TrkElnIt** – AI-enhanced automation & data extraction tools  


