# Getting Started

Get up and running with AI-VOX demos and resources.

## Prerequisites

Before you begin, ensure you have:

- Python 3.10 or higher
- Git
- An AWS account (for Bedrock demos)
- SAP system access (for SAP-specific demos)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/AI-VOX/ai-vox.github.io.git
cd ai-vox.github.io
```

### 2. Set Up Virtual Environment

=== "macOS/Linux"

    ```bash
    python -m venv venv
    source venv/bin/activate
    ```

=== "Windows"

    ```bash
    python -m venv venv
    venv\Scripts\activate
    ```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment

Create a `.env` file with your credentials:

```bash
AWS_REGION=us-east-1
AWS_PROFILE=your-profile
```

!!! warning "Security Note"
    Never commit your `.env` file to version control.

## Running Your First Demo

```bash
python demos/hello_agent.py
```

You should see output like:

```
Agent initialized successfully
> Hello! I'm your AI assistant. How can I help you today?
```

## Next Steps

- [Explore SAP Agentic AI](demos/sap-agentic-ai.md)
- [Learn about Building Agents](guides/building-agents.md)
- [Review Best Practices](guides/best-practices.md)
