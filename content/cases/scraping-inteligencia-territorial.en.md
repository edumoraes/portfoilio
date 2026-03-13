---
title: Operational scraping with geocoding, deduplication, and territorial analysis
description: A tool to map physical presence and territorial coverage through scraping, radial ZIP generation, and geographic visualization in an interactive map.
slug: operational-scraping-territorial-analysis
weight: 4
case:
  index: Case 04
  eyebrow: Data acquisition
  summary: "This case study organizes a territorial collection problem that is often poorly solved by linear scraping. Instead of querying only a few fixed points and accepting gaps, the solution generates radius-based coverage, turns coordinates into useful ZIP codes, and delivers clean data for geographic analysis."
  stack: "Python • Playwright • Geopy • Streamlit • CSV • geocoding"
  scope:
    - structured scraping
    - radial ZIP generation
    - geocoding and cache
    - deduplication
    - geographic dashboard
  results:
    - expands collection coverage from a central ZIP code and configurable radius
    - removes duplicates before analysis
    - turns raw data into a map usable by operations
---
## Context

When information about physical presence is scattered across search pages, manual collection quickly becomes wasteful. The challenge here was not only extracting records. It was covering a geographic area more intelligently, consolidating results without duplication, and making the output useful for territorial analysis.

The work needed to serve both data collection and later exploration.

## The problem

Scraping based on fixed queries usually creates an incomplete view. If the search depends only on a few ZIP codes or manually chosen regions, part of the coverage stays invisible. On top of that, the raw output almost always comes with duplicates, inconsistent addresses, and little support for geographic exploration.

So the problem was less about "scraping a page" and more about building a territorial acquisition pipeline that covered the area better, tolerated imperfections in the source data, and returned a usable dataset.

## Architecture and decisions

The solution was organized in two fronts. The first is collection: a scraper automates the search flow and extracts the records found. The second is territorial expansion: from a central ZIP code, the system geocodes the origin, calculates compass points by radius, and attempts to convert those coordinates into new ZIP codes to expand search coverage.

That choice matters because it attacks the structural limitation of simple scraping. Instead of depending on a small set of manual inputs, collection starts exploring the surrounding area with a replicable pattern.

After collection, the pipeline still solves three typical operational-data problems: deduplication, geocoding, and visualization. The dataset is not delivered as a raw list for someone else to figure out. It already comes prepared for map reading and coverage analysis.

## How the technology solves it

Python was used as the base to unify browser automation, CSV processing, and geographic components. Playwright appears where the site interaction needs to be reproduced reliably. Geopy and Nominatim handle direct and reverse geocoding, while caching reduces cost and repeated calls.

Radial ZIP generation is the most pragmatic part of the design. It turns a central point into an explorable area, improving collection without requiring a large manual list of inputs. When geocoding does not find the exact ZIP code, the flow tries alternative paths to approximate the search instead of failing unnecessarily.

The Streamlit dashboard closes the loop. It is not a cosmetic extra, but an operational reading layer. After cleaning, deduplicating, and geocoding the data, map visualization helps reveal concentration, gaps, and territorial reach without depending on outside treatment.

## Result and impact

The result is a tool that goes beyond one-off scraping. It collects, expands coverage, cleans the data, and delivers a dataset ready for geographic analysis. That reduces manual work at both ends: less effort to query and less effort to interpret.

Technically, the value comes from treating collection as a pipeline rather than an isolated script. The solution combines automation, geography, and visualization to solve a concrete operational problem: turning scattered lookups into actionable territorial visibility.
---
