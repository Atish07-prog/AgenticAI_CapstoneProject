# Multi-Agent Travel Itinerary & Budget Compliance System

An automated, data-backed Travel Concierge and Financial Compliance pipeline built using **LangGraph**, **LangChain**, and **DuckDuckGo Search Tools**. 

This system leverages a multi-agent **Pipeline Pattern with a Validation-Retry Loop** to dynamically design, audit, and refine a realistic day-by-day travel itinerary based on live search statistics and strict financial constraints.

## System Architecture & Orchestration

A single-prompt LLM often struggles to simultaneously manage creative itinerary mapping and strict mathematical budgeting constraints, frequently resulting in fictional pricing or ungrounded activity planning. 

This repository solves that limitation by dividing responsibilities across two specialized, isolated agent states synchronized via a **Shared Global State**:

1. **The Travel Planner Agent (`planner_node`):** Acts as the creative concierge. It uses live web search tools to fetch up-to-date landmark tickets, accommodation averages, and transport fees for the target destination, constructing a comprehensive daily plan.
2. **The Compliance Auditor Agent (`compliance_node`):** Acts as the financial gatekeeper. It evaluates the draft itinerary's content, dynamically verifies that itemized financial breakdowns exist, and assesses whether the calculated spending falls within the user's hard cap.

### Failure Handling & The Validation-Retry Loop
To prevent silent failures or broken formatting, the system includes a strict programmatic quality check. If the Planner Agent omits cost metrics or proposes activities that breach the maximum budget, the Compliance Auditor flags the state as invalid, constructs contextual feedback detailing the exact adjustments required, and reroutes execution back to the Planner node for an explicit, self-correcting rewrite loop.

---

## Directory Structure

```text
├── main.py          # Main executable Python script containing the multi-agent execution graph
├── README.md        # Documentation and setup instructions
└── requirements.txt # Project package dependencies