---
trigger: glob
globs: *.py
---
# Python Coding Standards

## CRITICAL RULES (Agent MUST Follow)

### Comments Policy
- NO module-level docstrings or comments at file start
- NO inline comments for obvious code (e.g., "# Initialize list" before `items = []`)
- NO docstrings on simple functions - if it's clear from the signature, skip it
- ONLY comment when explaining non-obvious "why" (business logic, workarounds, edge cases)
- Keep docstrings minimal: 1-2 sentences max, no Args/Returns for obvious cases

### Import Policy
- ALL imports at TOP of file - NEVER inside functions/methods
- Order: stdlib -> third-party -> local absolute -> local relative
- Blank line between each group
- Use isort with Black profile

### Simplicity Policy
- Implement the SIMPLEST solution that works
- Use existing base classes/mixins before creating new abstractions
- One function = one clear responsibility
- If extensive documentation needed, the code is too complex - refactor it
- Avoid over-engineering: no premature abstractions, no "just in case" code

## Code Standards
- PEP 8, snake_case functions/vars, PascalCase classes
- Type hints required on all function signatures (params + return)
- Modern syntax: `str | None` not `Optional[str]`, `list[str]` not `List[str]`
- Specific error handling; no bare `except:`
- Use uv for dependency management
- Use pytest for testing

## Django/FastAPI Patterns
- Use select_related/prefetch_related for related objects
- ViewSet-based views with proper authentication
- Pydantic for request/response schemas (FastAPI)
- Factory methods (@classmethod from_json) for object creation
- @property for computed values

## What NOT To Do
```python
# BAD: Import inside function
def process():
    import json  # NEVER DO THIS
    return json.dumps(data)

# BAD: Module docstring
"""
This module handles user authentication.
"""

# BAD: Obvious comment
user_list = []  # Initialize empty list

# BAD: Over-documented simple function
def add(a: int, b: int) -> int:
    """Add two integers together.

    Args:
        a: First integer
        b: Second integer

    Returns:
        Sum of a and b
    """
    return a + b

# GOOD: Simple function, no docstring needed
def add(a: int, b: int) -> int:
    return a + b
```
