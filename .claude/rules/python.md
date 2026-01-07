---
paths: **/*.py
---

# Python: Deterministic Only

Claude Code provides all intelligence. Python handles only deterministic operations.

## Allowed

- File operations
- Web scraping
- Filtering/sorting
- JSON CRUD
- Regex/string manipulation
- Database queries

## Forbidden

```python
from anthropic import Anthropic
from openai import OpenAI
from langchain import *
from pydantic_ai import Agent
```

No semantic analysis, no NL ranking, no "intelligent" decisions in Python.

## Architecture

```
User → Claude Code (intelligence) → Python (deterministic data) → Claude Code (analysis) → User
```
