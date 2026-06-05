# Agent instructions

This repository is a **trade journal** for logging equity trades made by a Cursor cloud agent. There is no application server, package manager, or build step.

## Cursor Cloud specific instructions

### What runs here

| Component | Required? | Notes |
|-----------|-----------|--------|
| Git + filesystem | Yes | All work is plain-text files under `Trades/` |
| Robinhood MCP | Optional | Use for live quotes, positions, and orders; journal files are the source of truth for P/L |
| Dev servers / Docker | No | Not part of this repo |

### Daily workflow

1. Create or edit `Trades/<M-D-YY>.txt` (see `Trades/example.txt` for column layout).
2. Sum profit/loss at the bottom (`TOTAL PROFIT: $X.XX`).
3. Commit the trade file when the session is complete.

### Lint / test / build

There is no configured linter, test runner, or build. Validate manually:

```bash
# Header must match example
head -1 Trades/<file>.txt

# Optional: confirm TOTAL line exists
grep -i '^TOTAL PROFIT:' Trades/<file>.txt
```

### Robinhood MCP (optional)

- **Read-only checks**: `get_equity_quotes`, `get_accounts`, `get_equity_positions`, `get_portfolio`
- **Trading**: Requires an account with `agentic_allowed=true` (nickname "Agentic" in this environment). Use `review_equity_order` before `place_equity_order`.
- Never place real orders during environment setup unless the user explicitly requests it.

### Directory name

README refers to `trades/`; the actual folder is `Trades/` (capital T). Use `Trades/` to match the repository.
