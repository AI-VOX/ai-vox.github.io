# Building Agents

Learn how to create AI agents for enterprise applications.

## What is an Agent?

An AI agent is an autonomous system that can:

- **Perceive** - Understand user intent and context
- **Reason** - Plan and make decisions
- **Act** - Execute tasks using tools
- **Learn** - Improve from feedback

## Agent Architecture

```
┌────────────────────────────────────────────────────────────┐
│                        AI Agent                            │
├────────────────────────────────────────────────────────────┤
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │  Model   │  │  Tools   │  │  Memory  │  │ Guardrails│   │
│  │ (Claude) │  │ (Actions)│  │ (Context)│  │ (Safety) │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘   │
└────────────────────────────────────────────────────────────┘
```

## Creating Your First Agent

### Step 1: Define the Agent

```python
from strands import Agent

agent = Agent(
    name="my-assistant",
    description="A helpful AI assistant for enterprise tasks",
    model="anthropic.claude-sonnet"
)
```

### Step 2: Add Tools

```python
from strands.tools import tool

@tool
def get_customer_info(customer_id: str) -> dict:
    """Retrieve customer information from the database."""
    # Your implementation here
    return {"id": customer_id, "name": "Acme Corp"}

agent.add_tool(get_customer_info)
```

### Step 3: Run the Agent

```python
response = agent.run("Get information for customer C001")
print(response)
```

## Tool Types

### Built-in Tools

| Tool | Purpose |
|------|---------|
| `web_search` | Search the internet |
| `file_read` | Read local files |
| `http_request` | Make API calls |

### Custom Tools

Create tools specific to your enterprise:

```python
@tool
def create_purchase_order(
    material: str,
    quantity: int,
    vendor: str
) -> dict:
    """Create a purchase order in SAP."""
    # SAP RFC call or API request
    return {"po_number": "4500001234", "status": "created"}
```

## Adding Memory

Enable context retention across conversations:

```python
from strands.memory import ConversationMemory

agent = Agent(
    name="my-assistant",
    memory=ConversationMemory(max_messages=50)
)
```

## Multi-Agent Systems

Orchestrate multiple specialized agents:

```python
from strands import Agent, Orchestrator

sales_agent = Agent(name="sales", tools=[...])
support_agent = Agent(name="support", tools=[...])

orchestrator = Orchestrator(
    agents=[sales_agent, support_agent],
    routing="automatic"
)

response = orchestrator.run("I need help with my order")
```

## Next Steps

- [Best Practices](best-practices.md) - Production deployment tips
- [SAP Agentic AI](../demos/sap-agentic-ai.md) - SAP-specific implementation
