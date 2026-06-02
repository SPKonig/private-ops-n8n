```markdown
# Daily Geopolitics News Report

Automated workflow that aggregates geopolitical news from 16 RSS feeds, processes them with AI summarization, and delivers concise morning briefings via Telegram twice daily.

## Overview

- **Workflow ID:** `AKEWhsWFux9gSZBS`
- **Status:** Active
- **Created:** 15.05.2026
- **Last Modified:** 24.05.2026
- **Project:** `vIaIDcGye5gviyqQ`
- **URL:** [https://private-ops.app.n8n.cloud/workflow/AKEWhsWFux9gSZBS](https://private-ops.app.n8n.cloud/workflow/AKEWhsWFux9gSZBS)

## Trigger

The workflow executes **twice daily at 08:00 and 19:00 UTC** via a schedule trigger, initiating parallel RSS feed processing for all configured news sources.

## Workflow Steps

**1. Schedule Trigger**
- **Type:** `n8n-nodes-base.scheduleTrigger`
- **Function:** Initiates workflow execution at 08:00 and 19:00 UTC daily

**2. RSS NYT World**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *New York Times World* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**3. RSS NYT Americas**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *New York Times Americas* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**4. RSS NYT Africa**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *New York Times Africa* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**5. RSS NYT AsiaPacific**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *New York Times Asia Pacific* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**6. RSS NYT Europe**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *New York Times Europe* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**7. RSS NYT MiddleEast**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *New York Times Middle East* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**8. RSS WSJ World News**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *Wall Street Journal World News* RSS feed

**9. RSS WSJ Politics**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *Wall Street Journal Politics* RSS feed

**10. RSS WSJ US**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *Wall Street Journal US* RSS feed

**11. RSS BBC Asia**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *BBC Asia* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**12. RSS BBC Europe**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *BBC Europe* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**13. RSS BBC Latin America**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *BBC Latin America* RSS feed

**14. RSS BBC Middle East**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *BBC Middle East* RSS feed

**15. RSS BBC US & Canada**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *BBC US & Canada* RSS feed

**16. RSS BBC Politics**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *BBC Politics* RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**17. RSS FAZ.NET USA**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *Frankfurter Allgemeine Zeitung USA* RSS feed

**18. RSS FAZ.NET Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *Frankfurter Allgemeine Zeitung Inland* RSS feed

**19. RSS FAZ.NET Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest geopolitical news from *Frankfurter Allgemeine Zeitung Ausland* RSS feed

**20. Merge NYT**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all New York Times RSS feeds into a single dataset using SQL UNION queries

**21. Merge WSJ**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all Wall Street Journal RSS feeds into a single dataset using SQL UNION queries

**22. Merge BBC**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all BBC RSS feeds into a single dataset using SQL UNION queries

**23. Merge FAZ.NET**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all FAZ.NET RSS feeds into a single dataset using SQL UNION queries

**24. Aggregate NYT**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all New York Times articles into a single data object for AI processing

**25. Aggregate WSJ**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all Wall Street Journal articles into a single data object for AI processing

**26. Aggregate BBC**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all BBC articles into a single data object for AI processing

**27. Aggregate FAZ.NET**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all FAZ.NET articles into a single data object for AI processing

**28. Summarize NYT**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize New York Times articles into structured news blocks, prioritizing recent (<12h) content

**29. Summarize WSJ**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize Wall Street Journal articles into structured news blocks, prioritizing recent (<12h) content

**30. Summarize BBC**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize BBC articles into structured news blocks, prioritizing recent (<12h) content

**31. Summarize FAZ**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to summarize FAZ.NET articles into structured news blocks, prioritizing recent (<12h) content

**32. Merge**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all source-specific summaries into a single dataset

**33. Aggregate**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Prepares combined summaries for final report generation

**34. Write Report**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Generates the final structured morning briefing with 8 prioritized news blocks from all sources

**35. Send Summary Sören**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers the final report to Sören via Telegram

**36. Send Summary Susanne**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers the final report to Susanne via Telegram

## Connected Systems

- `n8n-nodes-base.rssFeedRead` to **RSS Feeds** (NYT, WSJ, BBC, FAZ.NET)
- `@n8n/n8n-nodes-langchain.chainLlm` to **AI Language Models** (Mistral, Anthropic Claude)
- `n8n-nodes-base.telegram` to **Telegram API**

## Metadata

*Auto-generated by n8n workflow documentation system. Last updated: 24.05.2026*
```