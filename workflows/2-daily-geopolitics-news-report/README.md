```markdown
# Daily Geopolitics News Report

Automated workflow that aggregates geopolitical news from 17 international RSS feeds, processes the content using AI summarization, and delivers structured morning briefings via Telegram.

## Overview

- **Workflow ID:** `AKEWhsWFux9gSZBS`
- **Status:** Active
- **Created:** 15.05.2026
- **Last Modified:** 24.05.2026
- **Project:** `vIaIDcGye5gviyqQ`
- **URL:** [https://private-ops.app.n8n.cloud/workflow/AKEWhsWFux9gSZBS](https://private-ops.app.n8n.cloud/workflow/AKEWhsWFux9gSZBS)

## Trigger

The workflow executes twice daily at **08:00** and **19:00** UTC via a schedule trigger, initiating parallel RSS feed processing from 17 international news sources.

## Workflow Steps

**1. Schedule Trigger**
- **Type:** `n8n-nodes-base.scheduleTrigger`
- **Function:** Triggers the workflow at 08:00 and 19:00 UTC daily.

**2. RSS NYT World**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The New York Times* World RSS feed.

**3. RSS NYT Americas**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The New York Times* Americas RSS feed.

**4. RSS NYT Africa**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The New York Times* Africa RSS feed.

**5. RSS NYT AsiaPacific**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The New York Times* Asia Pacific RSS feed.

**6. RSS NYT Europe**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The New York Times* Europe RSS feed.

**7. RSS NYT MiddleEast**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The New York Times* Middle East RSS feed.

**8. RSS WSJ World News**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The Wall Street Journal* World News RSS feed.

**9. RSS WSJ Politics**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The Wall Street Journal* Politics RSS feed.

**10. RSS WSJ US**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *The Wall Street Journal* US RSS feed.

**11. RSS BBC Asia**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *BBC* Asia RSS feed.

**12. RSS BBC Europe**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *BBC* Europe RSS feed.

**13. RSS BBC Latin America**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *BBC* Latin America RSS feed.

**14. RSS BBC Middle East**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *BBC* Middle East RSS feed.

**15. RSS BBC US & Canada**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *BBC* US & Canada RSS feed.

**16. RSS BBC Politics**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *BBC* Politics RSS feed.

**17. RSS FAZ.NET USA**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *Frankfurter Allgemeine Zeitung* USA RSS feed.

**18. RSS FAZ.NET Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *Frankfurter Allgemeine Zeitung* Inland RSS feed.

**19. RSS FAZ.NET Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest articles from *Frankfurter Allgemeine Zeitung* Ausland RSS feed.

**20. Merge NYT**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and filters *New York Times* RSS feeds using SQL to remove null titles.

**21. Merge WSJ**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and filters *Wall Street Journal* RSS feeds using SQL to remove null titles.

**22. Merge BBC**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and filters *BBC* RSS feeds using SQL to remove null titles.

**23. Merge FAZ.NET**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and filters *FAZ.NET* RSS feeds using SQL to remove null titles.

**24. Aggregate NYT**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all *New York Times* articles into a single data object.

**25. Aggregate WSJ**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all *Wall Street Journal* articles into a single data object.

**26. Aggregate BBC**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all *BBC* articles into a single data object.

**27. Aggregate FAZ.NET**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all *FAZ.NET* articles into a single data object.

**28. Summarize NYT**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize *New York Times* articles into a structured morning briefing format, prioritizing content from the last 12 hours.

**29. Summarize WSJ**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize *Wall Street Journal* articles into a structured morning briefing format, prioritizing content from the last 12 hours.

**30. Summarize BBC**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize *BBC* articles into a structured morning briefing format, prioritizing content from the last 12 hours.

**31. Summarize FAZ**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize *FAZ.NET* articles into a structured morning briefing format, prioritizing content from the last 12 hours.

**32. Merge**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines summaries from all four news sources into a single output.

**33. Aggregate**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all source summaries into a single data object for final processing.

**34. Write Report**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Generates a final consolidated morning briefing from all aggregated summaries, adhering to strict formatting and relevance rules.

**35. Send Summary Sören**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers the final report to Telegram user **Sören** (Chat ID: `8325665200`).

**36. Send Summary Susanne**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers the final report to Telegram user **Susanne** (Chat ID: `8887726838`).

## Connected Systems

- `n8n-nodes-base.rssFeedRead` to **RSS Feeds** (17 sources: NYT, WSJ, BBC, FAZ.NET)
- `@n8n/n8n-nodes-langchain.chainLlm` to **Mistral AI** (Model: `mistral-small-2603`)
- `@n8n/n8n-nodes-langchain.lmChatAnthropic` to **Anthropic Claude** (Model: `claude-haiku-4-5-20251001`)
- `n8n-nodes-base.telegram` to **Telegram API** (Bot: `kevin_geonews_bot`)

## Metadata

*Auto-generated by n8n workflow documentation system. Last updated: 24.05.2026*
```