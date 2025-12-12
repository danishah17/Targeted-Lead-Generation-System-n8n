#  Targeted Business Lead Generation Engine

An automated low-code workflow designed to build targeted B2B lead lists. This engine scrapes business data from Google Maps based on a specific niche/location and recursively visits business websites to extract direct contact emails.

##  Workflow Visual
The image is available above in the repository.

##  Overview
Finding high-quality leads manually is slow and inefficient. This project automates the entire prospecting pipeline. 

By simply inputting a search query (e.g., *"Gyms in London"* or *"Marketing Agencies in New York"*), the system:
1.  Identifies businesses via Google Maps.
2.  Extracts their metadata (Phone, Website, Name).
3.  Visits their actual websites to hunt for contact information.
4.  Cleans the data and saves it to a spreadsheet.

##  Key Features
* **Chat-Initiated Trigger:** The workflow begins via a chat interface or webhook, allowing for dynamic keyword input.
* **Google Maps Scraping:** Integrates with **Apify** to bulk-extract business listings from Maps.
* **Deep Web Scraping:** Automatically loops through the website URL of every identified business to parse HTML and extract email addresses.
* **Data Hygiene:**
    * **Deduplication:** Automatically removes duplicate email entries.
    * **Smart Filtering:** Removes irrelevant emails (e.g., standard placeholder emails or non-contact strings).
* **Automated Export:** Appends all valid, enriched leads directly to a **Google Sheet**.

##  Data Output
The workflow generates a finalized CSV/Sheet with the following columns:

| Field | Description |
| :--- | :--- |
| **Business Name** | The entity name as listed on Google Maps. |
| **Email Address** | Contact email scraped from the business homepage. |
| **Phone Number** | Public contact number. |
| **Website Link** | Direct URL to the business website. |

##  Tech Stack
* **Orchestration:** [n8n](https://n8n.io/) (Workflow Automation)
* **Scraper:** [Apify](https://apify.com/) (Google Maps Scraper)
* **Storage:** Google Sheets
* **Logic:** Javascript (for data transformation), HTML Parsing, Regular Expressions.

##  How It Works (Step-by-Step)
1.  **Input:** User provides a niche and location.
2.  **Map Scrape:** n8n triggers the Apify actor to scrape Google Maps results.
3.  **Iteration:** The workflow splits the results and loops through every result that contains a website URL.
4.  **HTML Parsing:** The system performs an HTTP GET request on the website and uses regex/selectors to find `mailto:` links or email patterns.
5.  **Aggregation:** Email arrays are aggregated and matched back to the business name.
6.  **Sanitization:** The data passes through deduplication and filter nodes to ensure list quality.
7.  **Storage:** Final row is added to the Google Sheet.

---
*Created by Syed Danish Hussain*
