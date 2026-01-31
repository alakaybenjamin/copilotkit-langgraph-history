# Examples

This directory contains example applications demonstrating how to use `copilotkit-langgraph-history` with FastAPI and Next.js.

## Available Examples

### fastapi-nextjs

A complete example showing:
- FastAPI server with LangGraph and PostgreSQL persistence
- Next.js UI with CopilotKit integration
- History hydration using `copilotkit-langgraph-history`
- Custom client for self-hosted FastAPI servers
- Thread ownership and management

**See:** [fastapi-nextjs/README.md](./fastapi-nextjs/README.md)

---

## Quick Start

Each example is self-contained with its own setup instructions. Navigate to the example directory and follow the README.

### General Requirements

- **Python**: 3.10+ (for FastAPI backend)
- **Node.js**: 18+ (for Next.js frontend)
- **PostgreSQL**: For persistent storage (or use MemorySaver for testing)

### Common Setup Pattern

1. **Backend (Python)**:
   ```bash
   cd examples/fastapi-nextjs/agent
   pip install -e .
   python main.py
   ```

2. **Frontend (Next.js)**:
   ```bash
   cd examples/fastapi-nextjs/ui
   npm install
   npm run dev
   ```

---

## Package Usage

All examples use the published packages:

- **Python**: `copilotkit-langgraph-history` from PyPI
  ```bash
  pip install copilotkit-langgraph-history
  ```

- **TypeScript**: `test-history-agui` from npm
  ```bash
  npm install test-history-agui
  ```

---

## Related Packages

- **PyPI Package**: https://pypi.org/project/copilotkit-langgraph-history/
- **npm Package**: https://www.npmjs.com/package/test-history-agui
- **Python Repository**: https://github.com/alakaybenjamin/copilotkit-langgraph-history
- **npm Repository**: https://github.com/alakaybenjamin/copilotkit-langgraph-history-extend
