# Demos

Explore our AI demonstrations for enterprise applications.

=== "SAP Agentic AI"

    Build autonomous AI agents that interact with SAP systems.

    **Capabilities:**

    - Query SAP data using natural language
    - Create and modify SAP documents (Purchase Orders, Sales Orders, etc.)
    - Automate complex multi-step workflows
    - Provide intelligent recommendations based on SAP data

    **Architecture:**

    ```
    ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
    │   User Input    │────▶│   AI Agent      │────▶│   SAP System    │
    │   (Natural      │     │   (Claude/      │     │   (S/4HANA,     │
    │    Language)    │◀────│    Bedrock)     │◀────│    BTP, etc.)   │
    └─────────────────┘     └─────────────────┘     └─────────────────┘
    ```

    **Quick Start:**

    ```python
    from sap_agent import SAPAgent

    agent = SAPAgent(
        sap_host="your-sap-host",
        sap_client="100",
        sap_user="your-user"
    )

    response = agent.run(
        "Show me all open purchase orders over $10,000"
    )
    ```

    **Available Tools:**

    | Tool | Description |
    |------|-------------|
    | `sap_query` | Execute read queries against SAP |
    | `sap_create` | Create new SAP documents |
    | `sap_update` | Modify existing documents |
    | `sap_workflow` | Trigger SAP workflows |

=== "ERP Automation"

    Streamline enterprise resource planning workflows with AI.

    **Use Cases:**

    - **Invoice Processing** - Automatic extraction and validation
    - **Inventory Management** - Predictive restocking and optimization
    - **Financial Reporting** - Automated report generation and analysis
    - **Workflow Automation** - Intelligent routing and approvals

    **Invoice Processing Example:**

    ```python
    from erp_agent import InvoiceAgent

    agent = InvoiceAgent()
    result = agent.process_invoice("invoice.pdf")

    print(f"Vendor: {result.vendor}")
    print(f"Amount: {result.amount}")
    print(f"Status: {result.validation_status}")
    ```

    **Inventory Optimization Example:**

    ```python
    from erp_agent import InventoryAgent

    agent = InventoryAgent()
    recommendations = agent.analyze_inventory(
        warehouse="WH001",
        forecast_days=30
    )

    for item in recommendations:
        print(f"{item.material}: Order {item.quantity} units")
    ```

=== "Video Showcases"

    Watch AI in action with our curated video demonstrations.

    !!! note "Coming Soon"
        Video content is being prepared. Check back for updates.

    **Video Library:**

    | Title | Duration | Level |
    |-------|----------|-------|
    | Introduction to AI-VOX | 5 min | Beginner |
    | SAP Agent Deep Dive | 20 min | Advanced |
    | ERP Automation Basics | 15 min | Intermediate |
    | Multi-Agent Systems | 25 min | Advanced |
