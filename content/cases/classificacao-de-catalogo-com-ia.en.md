---
title: AI catalog classification with assisted search and operational fallback
description: A pipeline that turns a manual classification job into an auditable workflow with web search, LLM-assisted decisions, confidence scoring, and outputs ready for operations.
slug: ai-catalog-classification
weight: 2
case:
  index: Case 02
  eyebrow: Operational automation
  summary: "This case study starts from a classic operations problem: large spreadsheets, incomplete context, and a lot of manual work to place products into categories useful for the business. The solution was a pipeline combining search, LLM reasoning, validation, and resumable execution without hiding uncertainty."
  stack: "Python • LangGraph • OpenAI • DuckDuckGo Search • Excel • GUI/CLI"
  scope:
    - spreadsheet ingestion
    - search-based enrichment
    - LLM classification
    - confidence scoring
    - resume and reporting
  results:
    - reduced to hours a process that would take at least 3 weeks
    - automated catalog organization and operational consolidation
    - kept doubt and error as explicit states instead of masking uncertainty
---
## Context

The work started in one spreadsheet and ended in another, but the real cost was in the middle: understanding each item, gathering context, deciding the right category, and recording it consistently. As volume grows, the operation becomes dominated by repetitive tasks and manual review.

The goal was not simply to "classify with AI." It was to create a workflow reliable enough to become a real tool, with outputs useful to the team and predictable behavior when available information was insufficient.

## The problem

Spreadsheets like this often contain incomplete descriptions, ambiguous names, and little context about the real application of the product. If the system decides only from the raw row text, the error rate rises quickly. If it always answers confidently, even when uncertain, it becomes operational risk disguised as automation.

So the problem had two parts. First, enrich the item before deciding. Then represent uncertainty explicitly so operations know when to trust the output and when to review it.

## Architecture and decisions

The solution was structured as a state graph in LangGraph. Instead of a single function that receives a row and returns a category, the flow was broken into small observable stages: build the search query, retrieve context, classify with the LLM, interpret the answer, and decide whether the output is usable, doubtful, or an error.

That decomposition mattered for two reasons. The first is technical: each stage can be tested, adjusted, and instrumented separately. The second is operational: when something fails, it is clear where and why.

Another rigorous choice was maintaining a confidence threshold and explicit output states. The system was not designed to always look certain. It was designed to stay useful even when it could not decide alone. Instead of inventing a category, it marks doubt, records an observation, and enables manual review with context.

Beyond the main flow, the application gained two usage surfaces: CLI and GUI. That keeps the automation from being restricted to people who code and brings the tool closer to the actual operational routine.

## How the technology solves it

Python was used as the base because it fits the spreadsheet, automation, search, and LLM integration ecosystem well. Excel reading and writing preserve the original structure while adding classification, confidence, status, and notes columns, which makes adoption easier without restructuring the team's work.

LangGraph solves what matters here: a flow with explicit stages, controlled retries, and clearly defined state. DuckDuckGo Search provides external context to reduce dependence on poor or incomplete descriptions. The OpenAI model is responsible for synthesizing that context and returning structured classification rather than free text.

The application design is also pragmatic outside the AI core. It includes persisted progress for resumability, structured logs, TXT/CSV/JSON reports, and useful stats for execution monitoring. In a long-running automation, that matters as much as the classification itself.

## Result and impact

The main gain was turning a process that would take weeks into a workflow completed in hours, without trading speed for opacity. The automation does not hide what it knows and what it does not know. It makes confidence, error, and doubt explicit as part of the product.

That makes the solution more reliable for operational use. The team receives an enriched spreadsheet, a clear report of what happened, and a tool that can be used both from the terminal and from a graphical interface. The outcome is not only less manual work. It is more predictability across the entire process.
---
