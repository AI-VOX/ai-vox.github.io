# Best Practices

Production-ready patterns for enterprise AI deployments.

## Security

### Authentication

!!! danger "Never Hardcode Credentials"
    Always use environment variables or secret managers.

```python
# Good
import os
api_key = os.environ.get("API_KEY")

# Bad
api_key = "sk-1234567890"  # Never do this!
```

### Input Validation

Always validate user inputs before processing:

```python
from pydantic import BaseModel, validator

class PurchaseOrderRequest(BaseModel):
    material: str
    quantity: int

    @validator('quantity')
    def quantity_must_be_positive(cls, v):
        if v <= 0:
            raise ValueError('Quantity must be positive')
        return v
```

### Guardrails

Implement safety guardrails for agent actions:

```python
from strands.guardrails import ContentFilter, ActionLimit

agent = Agent(
    guardrails=[
        ContentFilter(block_pii=True),
        ActionLimit(max_actions_per_turn=5)
    ]
)
```

## Performance

### Caching

Cache frequently accessed data:

```python
from functools import lru_cache

@lru_cache(maxsize=100)
def get_material_info(material_id: str) -> dict:
    # Expensive SAP call
    return sap_client.get_material(material_id)
```

### Async Operations

Use async for I/O-bound operations:

```python
import asyncio

async def process_documents(docs: list):
    tasks = [process_single(doc) for doc in docs]
    return await asyncio.gather(*tasks)
```

### Connection Pooling

Reuse database/API connections:

```python
from sqlalchemy import create_engine
from sqlalchemy.pool import QueuePool

engine = create_engine(
    "postgresql://...",
    poolclass=QueuePool,
    pool_size=5,
    max_overflow=10
)
```

## Error Handling

### Graceful Degradation

```python
async def get_data_with_fallback():
    try:
        return await primary_source.get()
    except PrimarySourceError:
        logger.warning("Primary source failed, using fallback")
        return await fallback_source.get()
```

### Retry Logic

```python
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential(multiplier=1, min=4, max=10)
)
def call_external_api():
    return api_client.request()
```

## Observability

### Logging

```python
import structlog

logger = structlog.get_logger()

logger.info(
    "agent_action",
    action="create_po",
    material="MAT001",
    quantity=100
)
```

### Metrics

Track key performance indicators:

```python
from prometheus_client import Counter, Histogram

agent_requests = Counter(
    'agent_requests_total',
    'Total agent requests',
    ['agent_name', 'status']
)

response_time = Histogram(
    'agent_response_seconds',
    'Agent response time'
)
```

### Tracing

Implement distributed tracing:

```python
from opentelemetry import trace

tracer = trace.get_tracer(__name__)

with tracer.start_as_current_span("process_request"):
    result = agent.run(user_input)
```

## Deployment Checklist

- [ ] Environment variables configured
- [ ] Secrets stored securely
- [ ] Logging enabled
- [ ] Metrics collection set up
- [ ] Error alerting configured
- [ ] Rate limiting implemented
- [ ] Health checks added
- [ ] Backup/recovery tested

## Next Steps

- [Building Agents](building-agents.md) - Agent fundamentals
- [Demos](../demos/index.md) - See examples in action
