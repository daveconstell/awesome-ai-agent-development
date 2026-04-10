# Awesome AI Agent Development

A compact guide to core agent-building concepts.

## Core Components
- **Agent**: Orchestrates decisions and actions toward a goal.
- **Model**: Reasoning engine that generates plans/content.
- **Prompt**: Instructions that define behavior and constraints.
- **Memory**: Session context and long-term state.
- **Tools**: External capabilities (APIs, DB, filesystem, code execution).

## Execution Building Blocks
- **Trigger**: Event that starts execution (user action, schedule, webhook).
- **Task**: A single unit of work (e.g., summarize, classify, send email).
- **Workflow**: Ordered tasks + logic (branching, retries, handoffs).

## Relationship (Quick View)
- `Trigger -> Workflow -> Tasks`
- Agent runs the workflow.
- Model reasons.
- Prompt steers output.
- Memory preserves context.
- Tools perform real actions.

## Minimal Example: Re-engagement Email Agent
**Goal:** Send one email to customers inactive for 30+ days.

### Flow
1. Trigger daily at 09:00.
2. Query inactive customers.
3. Skip customers already contacted recently.
4. Generate personalized email content.
5. Send email.
6. Log result.

### Pseudocode
```python
def daily_trigger():
    for customer in db.inactive_customers(days=30):
        if memory.sent_recently(customer.id):
            continue
        body = model.generate(
            f"Write a short re-engagement email for {customer.name}."
        )
        email_api.send(to=customer.email, body=body)
        memory.log_sent(customer.id)
```

## Practical Rule of Thumb
In most projects, start with:
1. A strong prompt.
2. The right tools.
3. Basic memory and logging.

Only fine-tune/train later if prompt + tooling + workflow design cannot meet quality needs.


![Model Diagram](./model.png)
