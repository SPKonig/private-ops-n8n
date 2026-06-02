```markdown
# Daily German News Report

Automated AI-powered news aggregation workflow that collects, processes, and summarizes German news from multiple sources (FAZ, Tagesschau, ZDF) into structured morning briefings, delivered via Telegram twice daily.

## Overview

- **Workflow ID:** `5ILVTTV5hXbftLcX`
- **Status:** Active
- **Created:** 22.05.2026
- **Last Modified:** 24.05.2026
- **Project:** `vIaIDcGye5gviyqQ`
- **URL:** [https://private-ops.app.n8n.cloud/workflow/5ILVTTV5hXbftLcX](https://private-ops.app.n8n.cloud/workflow/5ILVTTV5hXbftLcX)

## Trigger

The workflow executes automatically twice daily at **08:00** and **19:00** via a schedule trigger, initiating parallel news collection from all configured RSS feeds.

## Workflow Steps

**1. Schedule Trigger**
- **Type:** `n8n-nodes-base.scheduleTrigger`
- **Function:** Triggers the workflow at 08:00 and 19:00 daily

**2. RSS FAZ.NET USA**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest political news from FAZ.NET USA section via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**3. RSS FAZ.NET Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest domestic political news from FAZ.NET via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**4. RSS FAZ.NET Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches latest international news from FAZ.NET via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**5. RSS Tagesschau Inland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches domestic news from Tagesschau via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**6. RSS Tagesschau Wirtschaft**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches economic news from Tagesschau via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**7. RSS Tagesschau Ausland**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches international news from Tagesschau via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**8. RSS ZDF Politik**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches political news from ZDF via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**9. RSS ZDF Nachrichten**
- **Type:** `n8n-nodes-base.rssFeedRead`
- **Function:** Fetches general news from ZDF via RSS
- **Notes:** Error handling and cleaning of wrong data happens in the merge node

**10. Merge FAZ.NET**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and cleans FAZ.NET news items using SQL query to filter valid entries

**11. Merge Tagesschau**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and cleans Tagesschau news items using SQL query to filter valid entries

**12. Merge ZDF**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines and cleans ZDF news items using SQL query to filter valid entries

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
- **Function:** Uses AI (Mistral/Anthropic) to summarize FAZ.NET news into structured briefing format with strict 12-hour recency rules

**17. Summarize Tagesschau**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI (Mistral/Anthropic) to summarize Tagesschau news into structured briefing format with strict 12-hour recency rules

**18. Summarize ZDF**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI (Mistral/Anthropic) to summarize ZDF news into structured briefing format with strict 12-hour recency rules

**19. Merge**
- **Type:** `n8n-nodes-base.merge`
- **Function:** Combines summaries from FAZ, Tagesschau, and ZDF into single data stream

**20. Aggregate**
- **Type:** `n8n-nodes-base.aggregate`
- **Function:** Consolidates all source summaries into unified data structure

**21. Write Report**
- **Type:** `@n8n/n8n-nodes-langchain.chainLlm`
- **Function:** Uses AI (Mistral/Anthropic) to generate final 8-item morning briefing from consolidated news, prioritizing global impact events

**22. Send Summary Sören**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers final news briefing to Sören via Telegram

**23. Send Summary Susanne**
- **Type:** `n8n-nodes-base.telegram`
- **Function:** Delivers final news briefing to Susanne via Telegram

## Connected Systems

- `n8n-nodes-base.rssFeedRead` to **FAZ.NET RSS Feeds**
- `n8n-nodes-base.rssFeedRead` to **Tagesschau RSS Feeds**
- `n8n-nodes-base.rssFeedRead` to **ZDF RSS Feeds**
- `@n8n/n8n-nodes-langchain.lmChatMistralCloud` to **Mistral AI**
- `@n8n/n8n-nodes-langchain.lmChatAnthropic` to **Anthropic Claude**
- `n8n-nodes-base.telegram` to **Telegram Messenger**

## Metadata

*Auto-generated by n8n workflow documentation system. Last updated: 24.05.2026*
```