# Daily German News Report

Automated AI-powered morning briefing that collects, aggregates, and summarizes German news from multiple sources (FAZ, Tagesschau, ZDF) into structured Telegram messages sent twice daily.

## Overview

- **Workflow ID:** `5ILVTTV5hXbftLcX`
- **Status:** Active
- **Created:** 22.05.2026
- **Last Modified:** 24.05.2026
- **Project:** `vIaIDcGye5gviyqQ`
- **URL:** [https://private-ops.app.n8n.cloud/workflow/5ILVTTV5hXbftLcX](https://private-ops.app.n8n.cloud/workflow/5ILVTTV5hXbftLcX)

## Trigger

The workflow executes **twice daily at 08:00 and 19:00** via a schedule trigger, initiating parallel news collection from all configured RSS feeds.

## Workflow Steps

**1. Schedule Trigger**
- **Type:** `n8n-nodes-base.scheduleTrigger`
- **Function:** Starts the workflow at 8 AM and 7 PM daily

**2. RSS FAZ.NET USA**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches political news about the USA from FAZ.NET RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**3. RSS FAZ.NET Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches German domestic political news from FAZ.NET RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**4. RSS FAZ.NET Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches international political news from FAZ.NET RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**5. RSS Tagesschau Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches German domestic news from Tagesschau RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**6. RSS Tagesschau Wirtschaft**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches economic news from Tagesschau RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**7. RSS Tagesschau Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches international news from Tagesschau RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**8. RSS ZDF Politik**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches political news from ZDF RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**9. RSS ZDF Nachrichten**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches general news from ZDF RSS feed
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**10. Merge FAZ.NET**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all FAZ.NET RSS feeds into a single dataset using SQL query filtering for valid entries

**11. Merge Tagesschau**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all Tagesschau RSS feeds into a single dataset using SQL query filtering for valid entries

**12. Merge ZDF**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all ZDF RSS feeds into a single dataset using SQL query filtering for valid entries

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
- **Function:** Uses AI (Mistral/Anthropic) to summarize FAZ.NET news into 8 structured briefing blocks with strict time relevance rules

**17. Summarize Tagesschau**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI (Mistral/Anthropic) to summarize Tagesschau news into 8 structured briefing blocks with strict time relevance rules

**18. Summarize ZDF**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI (Mistral/Anthropic) to summarize ZDF news into 8 structured briefing blocks with strict time relevance rules

**19. Merge**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines all source summaries (FAZ, Tagesschau, ZDF) into a single dataset

**20. Aggregate**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Consolidates all merged summaries into one final data structure

**21. Write Report**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI (Mistral/Anthropic) to create the final morning briefing from all aggregated summaries

**22. Send Summary Sören**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Sends the final briefing via Telegram to recipient Sören

**23. Send Summary Susanne**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Sends the final briefing via Telegram to recipient Susanne

## Connected Systems

- `n8n-nodes-base.rssFeedRead` to **FAZ.NET RSS Feeds**
- `n8n-nodes-base.rssFeedRead` to **Tagesschau RSS Feeds**
- `n8n-nodes-base.rssFeedRead` to **ZDF RSS Feeds**
- `@n8n/n8n-nodes-langchain.lmChatMistralCloud` to **Mistral AI**
- `@n8n/n8n-nodes-langchain.lmChatAnthropic` to **Anthropic Claude**
- `n8n-nodes-base.telegram` to **Telegram API**

## Metadata

*Auto-generated by n8n workflow documentation system. Last updated: 24.05.2026*