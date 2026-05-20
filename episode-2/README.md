# Episode 2: Conversation Management & Skills

📺 [Watch on YouTube](https://www.youtube.com/watch?v=Dt7a7i726y0)

Building a production-style customer service agent with conversation memory, system prompts, steering, and skills.

## Setup

```bash
# From the repo root
source .venv/bin/activate

# Install dependencies
pip install strands-agents strands-agents-tools
```

## Files

| File | Description |
|------|-------------|
| `customer_service.py` | Full customer service agent with tools and skills |
| `customer_service_tools.py` | Extracted tools (lookup_customer, get_order_history, process_refund) |
| `customer_service_steering.py` | Agent with steering handlers for guardrails and tone enforcement |
| `steering_handlers.py` | Custom event handlers (refund workflow + tone checking) |
| `sliding_window_simple.py` | Conversation manager with sliding window strategy |
| `summarizing_simple.py` | Conversation manager with summarization strategy |
| `file_session_simple.py` | Session persistence using local file storage |
| `s3_session.py` | Session persistence using S3 |
| `skills/` | Skill definitions for guided workflows |

## Running the Examples

```bash
cd episode-2

# Basic customer service agent
python customer_service.py

# With steering handlers (guardrails + tone)
python customer_service_steering.py

# With sliding window memory management
python sliding_window_simple.py

# With summarization memory management
python summarizing_simple.py

# With file-based session persistence
python file_session_simple.py
```

## Topics Covered

- **System prompts** — Define agent personality and behavior guidelines
- **Custom tools** — `lookup_customer`, `get_order_history`, `process_refund`
- **Agent Skills** — On-demand workflow instructions loaded from markdown files (order tracking, refund processing, account troubleshooting)
- **Steering handlers** — Event-driven guardrails:
  - Deterministic handlers (enforce refund steps)
  - LLM-based handlers (enforce communication tone)
- **Conversation managers**:
  - Sliding window — Keep the last N messages, truncate older ones
  - Summarization — Compress older messages into a summary to preserve context
- **Session persistence**:
  - File-based — Save/restore conversations to local disk
  - S3-based — Save/restore conversations to an S3 bucket

## Skills

The `skills/` directory contains guided workflow instructions:

| Skill | Purpose |
|-------|---------|
| `order-tracking` | Step-by-step guide for helping customers track orders |
| `refund-processing` | Workflow for processing refunds with proper verification |
| `account-troubleshooting` | Guide for password resets, locked accounts, etc. |
| `pdf-processing` | Instructions for handling PDF document requests |
