---
title: Fullstack conversational commerce with AI, guided checkout, and real-time operations
description: A fullstack solution to sell through conversation, combining catalog search, automated service, controlled checkout, and real-time monitoring without losing operational control.
slug: conversational-commerce-fullstack
weight: 1
case:
  index: Case 01
  eyebrow: Fullstack solution
  summary: "A conversational sales operation only scales when AI, business rules, and human oversight can work together without friction. This case study combines a web interface, transactional backend, catalog search, conversational state, and payment flow into a single system built for real use."
  stack: "Next.js • FastAPI • PostgreSQL • Redis • Elasticsearch • LangGraph • WebSockets • WhatsApp"
  scope:
    - conversational service
    - catalog and product discovery
    - deterministic checkout
    - payments and order status
    - real-time operations dashboard
  results:
    - 90% reduction in AI-to-human support escalations
    - more than 300 managed conversations in the first 15 days
    - BRL 8k in orders in the first 15 days
---
## Context

The goal was to turn a conversation channel into a real commercial operation. That meant moving beyond the usual "chatbot that answers questions" pattern and building a system that could understand intent, query the catalog, preserve context, create a cart, persist the customer, generate the order, track payment, and still allow human intervention when needed.

In practice, the problem was not only answering well. It was keeping conversation, transactional state, and operational monitoring consistent.

## The problem

In conversational commerce, the most dangerous part is not the agent's first reply. The real risk appears when the conversation leaves the open-ended stage and enters decisions that require strict order: confirming items, collecting customer data, choosing delivery, persisting records, and closing payment.

A naive solution based only on prompting tends to fail exactly where the business cannot afford failure. It loses checkout state, mixes intent with execution, and makes both auditing and human handoff harder. The challenge here was separating what could stay probabilistic from what had to remain deterministic.

## Architecture and decisions

The solution was designed as a fullstack system, with a web surface in Next.js and an operational backend in FastAPI. In the backend, modeling was not organized only around messages, but around the real entities of the operation: conversations, customers, carts, orders, payments, and tracking events.

The conversational flow was split into two layers. The first remains flexible: intent triage, product discovery, loyalty program questions, store information, and general answers. The second is rigid: once the conversation enters checkout, the flow becomes controlled by an explicit graph, validating data and advancing only when prerequisites are satisfied.

That design is clear in the combination of LangGraph and the checkout orchestrator. The agent remains natural outside order closing, but the transactional moment gains order, traceability, and predictability. That reduces operational error without killing conversational fluency.

The catalog also had to be treated as a retrieval problem, not just a generation problem. Search uses Elasticsearch to handle free text, term variation, and intent-oriented discovery. Instead of asking the model to "remember" products, the architecture forces a catalog lookup before recommendation.

## How the technology solves it

FastAPI acts as the backbone of the operation. It exposes routes for assistants, conversations, products, payments, orders, customers, and status, while concentrating authentication, observability, persistence, and external integrations. PostgreSQL supports transactional data and execution history; Redis and real-time events help keep operations synchronized.

WebSockets with polling fallback were used to update the operations dashboard without manual refresh. That matters for handoff, human control, timeline reading, and conversation status changes. Operations do not need to look for what changed; they receive an event when something critical happens.

At the AI core, the work is divided by responsibility. There is intent triage to decide whether the user is asking for information, product, delivery, payment, status, or purchase. There are specialized agents for store information retrieval, catalog lookup, and data validation. And there is the checkout flow, where state stops being implicit and becomes governed by explicit stages such as data collection, delivery type, address, loyalty offer, customer persistence, and cart closing.

This separation is the most pragmatic point of the project. AI does not try to solve everything alone. It operates where flexibility is valuable and hands over to explicit rules when the cost of error rises.

## Result and impact

The result was a solution that works both as product and as operation. It reduces unnecessary handoff, preserves room for human intervention when the case demands it, and keeps the business auditable from start to finish.

The operational indicators show the effect of that design: a sharp reduction in escalation to human support, hundreds of AI-managed conversations in production, and revenue generation within the first weeks. More important than any isolated number is what it represents: the technology was used to sustain the entire commercial flow, not just automate the most visible conversational layer.
---
