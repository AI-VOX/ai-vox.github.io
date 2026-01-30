# SAP Agentic AI

Build autonomous AI agents that interact with SAP systems.

## Overview

The SAP Agentic AI Accelerator demonstrates how to build intelligent agents that can:

- Query SAP data using natural language
- Create and modify SAP documents (Purchase Orders, Sales Orders, etc.)
- Automate complex multi-step workflows
- Provide intelligent recommendations based on SAP data

## Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   User Input    │────▶│   AI Agent      │────▶│   SAP System    │
│   (Natural      │     │   (Claude/      │     │   (S/4HANA,     │
│    Language)    │◀────│    Bedrock)     │◀────│    BTP, etc.)   │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

## Quick Start

### 1. Configure SAP Connection

```python
from sap_agent import SAPAgent

agent = SAPAgent(
    sap_host="your-sap-host",
    sap_client="100",
    sap_user="your-user"
)
```

### 2. Run a Query

```python
response = agent.run(
    "Show me all open purchase orders over $10,000"
)
print(response)
```

### 3. Execute Actions

```python
response = agent.run(
    "Create a purchase order for 100 units of material MAT001 from vendor VEND001"
)
```

## Available Tools

The SAP agent comes with pre-built tools:

| Tool | Description |
|------|-------------|
| `sap_query` | Execute read queries against SAP |
| `sap_create` | Create new SAP documents |
| `sap_update` | Modify existing documents |
| `sap_workflow` | Trigger SAP workflows |

## Video Demo

<video controls width="100%">
  <source src="../assets/sap-agent-demo.mp4" type="video/mp4">
  Your browser does not support video playback.
</video>

!!! tip "Try It Yourself"
    Clone the repo and run `python demos/sap_agent_demo.py` to see it in action.

## Related Resources

- [Building Agents Guide](../guides/building-agents.md)
- [SAP ABAP Accelerator for Amazon Q](https://github.com/aws-samples/guidance-for-deploying-sap-abap-accelerator-for-amazon-q-developer)
