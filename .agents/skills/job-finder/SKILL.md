---
name: job-finder
description: A personalized AI assistant that scrapes multiple job boards for positions matching user preferences, collects feedback, and adjusts future suggestions.
---

Shared files: `user_preferences.txt` (role preferences + learned signals), `job_results.txt` (scraped listings), `feedback_log.txt` (favorite/least favorite + adjustments).

## Lead Agent (session controller)

1. Init (first run only): copy `./agents/skills/templates/job-finder/` files into working dir if not exist.
2. Load/Update Preferences: read `user_preferences.txt` if exists; prompt user to confirm or update role description. If new, prompt for role preferences. Write to `user_preferences.txt`.
3. Spawn Scraper Sub-Agent once. Wait.
4. Spawn Feedback Sub-Agent once. Wait.
5. Spawn Preference Learning Sub-Agent once. Wait.
6. Stop.

## Sub-Agents (all spawned via Task tool, `general` / `mode: subagent`)

**Scraper** (once per session):
1. Read `user_preferences.txt` for role keywords, location, salary range.
2. Scrape job boards in parallel: LinkedIn, Indeed, Glassdoor, Stack Overflow Jobs, company career pages. Skip boards with rate limits or authentication requirements.
3. For each job listing, extract: company name, location, salary range, job description, date posted, PTO, benefits. Use "not listed" for missing fields.
4. Deduplicate across boards by matching company + title + location.
5. Append results to `job_results.txt` in plain text format with clickable links. Do not read existing file.
6. Stop.

**Feedback Collector** (once per session):
1. Read `job_results.txt` to display results to user.
2. Prompt user to identify favorite and least favorite job from results.
3. Parse feedback signals: industry, salary range, location, job title keywords.
4. Append to `feedback_log.txt`: `--- Session <N> ---\nFavorite: <job_id> <signals>\nLeast Favorite: <job_id> <signals>`. Do not read existing file.
5. Stop.

**Preference Learner** (once per session):
1. Read `user_preferences.txt` for current preferences.
2. Read `feedback_log.txt` for latest feedback signals.
3. Adjust preferences: weight positive signals from favorites, negative signals from least favorites.
4. Overwrite `user_preferences.txt` with updated preferences.
5. Stop.

## Writing style (all sub-agents):
- concise, avoid ambiguity
- plain text output with structured formatting
- clickable URLs for job links
- readable job listing format with clear field labels

## Stop Conditions
- All sub-agents complete + `job_results.txt` written
- Sub-agent fails repeatedly → escalate to user
- User cancels
