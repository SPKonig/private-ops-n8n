# Daily German News Report

Automated AI-powered morning briefing system that aggregates, analyzes, and distributes curated news summaries from major German media sources via Telegram.

## Overview

- **Workflow ID:** `5ILVTTV5hXbftLcX`
- **Status:** Active
- **Created:** 22.05.2026
- **Last Modified:** 24.05.2026
- **Project:** `vIaIDcGye5gviyqQ`
- **URL:** [https://private-ops.app.n8n.cloud/workflow/5ILVTTV5hXbftLcX](https://private-ops.app.n8n.cloud/workflow/5ILVTTV5hXbftLcX)

## Trigger

The workflow executes twice daily at **08:00** and **19:00** via a scheduled trigger, initiating parallel news aggregation from all configured RSS feeds.

## Workflow Steps

**1. Schedule Trigger**
- **Type:** `n8n-nodes-base.scheduleTrigger`
- **Function:** Initiates workflow execution at 08:00 and 19:00 daily

**2. RSS FAZ.NET USA**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches political news from FAZ.NET's USA section RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**3. RSS FAZ.NET Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches domestic political news from FAZ.NET's Inland section RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**4. RSS FAZ.NET Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches international political news from FAZ.NET's Ausland section RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**5. RSS Tagesschau Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches international news from Tagesschau's Ausland RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**6. RSS Tagesschau Wirtschaft**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches economic news from Tagesschau's Wirtschaft RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**7. RSS Tagesschau Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches domestic news from Tagesschau's Inland RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**8. RSS ZDF Politik**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches political news from ZDF's Politik RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**9. RSS ZDF Nachrichten**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches general news from ZDF's Nachrichten RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**10. Merge FAZ.NET**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and filters valid FAZ.NET articles using SQL query to remove null titles

**11. Merge Tagesschau**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and filters valid Tagesschau articles using SQL query to remove null titles

**12. Merge ZDF**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and filters valid ZDF articles using SQL query to remove null titles

**13. Aggregate FAZ.NET**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all FAZ.NET news items into a single data structure

**14. Aggregate Tagesschau**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all Tagesschau news items into a single data structure

**15. Aggregate ZDF**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Aggregates all ZDF news items into a single data structure

**16. Summarize FAZ**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to create structured news briefing from FAZ.NET articles with strict formatting rules and 12-hour recency prioritization
- **Models:** Mistral Small, Claude Haiku 4.5 (fallback)

**17. Summarize Tagesschau**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to create structured news briefing from Tagesschau articles with strict formatting rules and 12-hour recency prioritization
- **Models:** Mistral Small, Claude Haiku 4.5 (fallback)

**18. Summarize ZDF**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI to create structured news briefing from ZDF articles with strict formatting rules and 12-hour recency prioritization
- **Models:** Mistral Small, Claude Haiku 4.5 (fallback)

**19. Merge**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines summaries from all three news sources (FAZ, Tagesschau, ZDF)

**20. Aggregate**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Consolidates all source summaries into a single data payload

**21. Write Report**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Generates final 8-item morning briefing with global focus, strict character limits, and source attribution
- **Models:** Mistral Small, Claude Haiku 4.5 (fallback)

**22. Send Summary Sören**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers final news briefing to Sören via Telegram

**23. Send Summary Susanne**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers final news briefing to Susanne via Telegram

## Connected Systems

- **Telegram** for message delivery
- **FAZ.NET** RSS feeds (USA, Inland, Ausland sections)
- **Tagesschau** RSS feeds (Ausland, Wirtschaft, Inland sections)
- **ZDF** RSS feeds (Politik, Nachrichten sections)
- **Mistral AI** for news summarization (mistral-small-latest)
- **Anthropic Claude** for news summarization (Claude Haiku 4.5)

## Metadata

*Auto-generated by n8n workflow documentation system. Last updated: 24.05.2026*