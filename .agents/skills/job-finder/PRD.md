# Job Finder - Product Requirements Document

## Overview

Job Finder is a personalized AI assistant that scrapes multiple job boards (LinkedIn, Indeed, Glassdoor, company career pages, Stack Overflow Jobs, etc.) for positions matching user preferences. It outputs results as plain text with clickable links. The assistant prompts users at the start of the first session for their role preferences, stores preferences in a local file, and asks in subsequent sessions whether to use the original description or update it. After generating results, it collects feedback on favorite and least favorite jobs to adjust future suggestions based on industry, salary range, location, and job title keywords.

---

## Tasks

### 1. User Preference Collection

- Prompt users at the beginning of the first session for a description of roles they are interested in
- In subsequent sessions, ask if the user wants to change the job description preferences or use the original
- Store preferences in a local file for persistence between sessions

### 2. Job Board Scraping

- Scrape multiple job boards: LinkedIn, Indeed, Glassdoor, company career pages, Stack Overflow Jobs, and other relevant job sites
- Implement rate limit handling: skip job boards that enforce rate limits
- Exclude any job boards requiring authentication
- Use Python with web scraping libraries (e.g., BeautifulSoup, Scrapy, Selenium)

### 3. Job Data Extraction

- Extract the following fields for each job listing:
  - Company name
  - Location (remote/on-site/hybrid)
  - Salary range
  - Job description
  - Date posted (if available)
  - Paid time off (if listed)
  - Benefits (if listed)
- For missing information, insert "not listed" as placeholder text

### 4. Deduplication System

- Detect and remove duplicate job postings across different job boards
- Ensure each unique job is displayed only once in results

### 5. Results Output

- Format results as plain text with clickable links to each job posting
- Present all scraped job information in a readable, structured format

### 6. Feedback Collection

- After displaying results, prompt user to identify their favorite and least favorite job from the suggestions
- Capture feedback signals: industry, salary range, location, job title keywords

### 7. Preference Learning

- Adjust future job suggestions based on collected feedback
- Update the local preference file with learned signals from favorite/least favorite selections
- Weight positive signals (from favorites) and negative signals (from least favorites) for improved matching

### 8. Edge Case Handling

- Handle missing salary or location data with "not listed" placeholder
- Gracefully skip job boards with rate limiting
- Bypass job boards requiring authentication
- Deduplicate cross-platform job postings
