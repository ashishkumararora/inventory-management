# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

Factory Inventory Management System Demo - Full-stack application with Vue 3 frontend, Python FastAPI backend, and in-memory mock data (no database).

## Critical Tool Usage Rules

### Subagents
Use the Task tool with these specialized subagents for appropriate tasks:

- **vue-expert**: Use for Vue 3 frontend features, UI components, styling, and client-side functionality
  - Examples: Creating components, fixing reactivity issues, performance optimization, complex state management
  - **MANDATORY RULE: ANY time you need to create or significantly modify a .vue file, you MUST delegate to vue-expert**
- **code-reviewer**: Use after writing significant code to review quality and best practices
- **Explore**: Use for understanding codebase structure, searching for patterns, or answering questions about how components work
- **general-purpose**: Use for complex multi-step tasks or when other agents don't fit

### Skills
- **backend-api-test** skill: Use when writing or modifying tests in `tests/backend` directory with pytest and FastAPI TestClient

### MCP Tools
- **ALWAYS use GitHub MCP tools** (`mcp__github__*`) for ALL GitHub operations
  - Exception: Local branches only - use `git checkout -b` instead of `mcp__github__create_branch`
- **ALWAYS use Playwright MCP tools** (`mcp__playwright__*`) for browser testing
  - Test against: `http://localhost:3000` (frontend), `http://localhost:8001` (API)

## Stack
- **Frontend**: Vue 3 + Composition API + Vite (port 3000)
- **Backend**: Python FastAPI (port 8001)
- **Data**: JSON files in `server/data/` loaded via `server/mock_data.py`

## Commands

### Start Servers
```bash
# Backend (use uv if available, otherwise python3)
cd server
uv run python main.py        # preferred
python3 main.py              # fallback if uv not in PATH

# Frontend
cd client
npm install && npm run dev
```

### Tests
Tests live in `tests/backend/` and use FastAPI TestClient (no running server needed).
```bash
cd tests
uv run pytest -v                                     # all 51 tests
uv run pytest backend/test_inventory.py -v          # single file
uv run pytest -k "test_filter" -v                   # by name pattern
uv run pytest --cov=../server --cov-report=html     # with coverage

# fallback if uv not in PATH
cd tests && python3 -m pytest -v
```

### Build
```bash
cd client && npm run build      # outputs to client/dist/
cd client && npm run preview    # preview production build
```

## Architecture

### Data Flow
```
Vue filter state (useFilters composable)
  → client/src/api.js (axios, base URL http://localhost:8001/api)
  → FastAPI (filter_by_month / apply_filters helpers)
  → In-memory JSON data
  → Pydantic model validation
  → Vue computed properties (derived from raw refs)
```

### Composables (client/src/composables/)
- **useFilters.js** — Singleton global filter state. Exports: `selectedPeriod`, `selectedLocation`, `selectedCategory`, `selectedStatus`, `resetFilters()`, `getCurrentFilters()`, `hasActiveFilters`. All views import this to read and update the 4 shared filters.
- **useI18n.js** — EN/JA translations with USD/JPY currency switching (1 USD = 150 JPY). Locale persisted to localStorage. Exports: `t()`, `setLocale()`, `currentLocale`, `currentCurrency`. Translation files: `client/src/locales/en.js` and `ja.js`.
- **useAuth.js** — Mock user auth. Exports: `currentUser`, `isAuthenticated`, `logout()`, `getInitials()`.

### Vue Router (client/src/main.js)
`/` → Dashboard, `/inventory` → Inventory, `/orders` → Orders, `/demand` → Demand, `/spending` → Spending, `/reports` → Reports, `/backlog` → Backlog

### Filter System
4 global filters applied via query params to all data endpoints:
- `month` — `YYYY-MM` or quarter (`Q1-2025` through `Q4-2025`). Not supported by `/api/inventory`.
- `warehouse` — San Francisco, London, Tokyo
- `category` — Circuit Boards, Sensors, Actuators, Controllers, Power Supplies
- `status` — Delivered, Shipped, Processing, Backordered (orders only)

### API Endpoints
- `GET /api/inventory` — Filters: warehouse, category (no month)
- `GET /api/inventory/{item_id}`
- `GET /api/orders` — Filters: warehouse, category, status, month
- `GET /api/orders/{order_id}`
- `GET /api/dashboard/summary` — All filters; returns total_inventory_value, low_stock_items, pending_orders, total_backlog_items, total_orders_value
- `GET /api/demand`, `GET /api/backlog` — No filters
- `GET /api/spending/summary|monthly|categories|transactions`
- `GET /api/reports/quarterly`, `GET /api/reports/monthly-trends`
- `POST /api/purchase-orders`, `GET /api/purchase-orders/{backlog_item_id}`

## Key Patterns

**Reactivity**: Raw data in refs (`allOrders`, `inventoryItems`), derived/filtered data in computed properties — never mutate the raw refs directly for display purposes.

**Global styles**: Defined in `client/src/App.vue`, not in separate CSS files.

**Pydantic models** in `server/main.py`: `InventoryItem`, `Order`, `DemandForecast`, `BacklogItem`, `PurchaseOrder`, `CreatePurchaseOrderRequest`. Update these when changing JSON data structure in `server/data/`.

## Common Issues
1. Use unique keys in `v-for` (not `index`) — use `sku`, `month`, `id`, etc.
2. Validate dates before calling `.getMonth()` — raw JSON strings must be parsed first.
3. Inventory endpoints don't support `month` filter (inventory has no time dimension).
4. Revenue goals: $800K/month (single warehouse), $9.6M YTD (all months).
5. Quarter mapping lives in `QUARTER_MAP` dict in `server/main.py` — update there if adding new periods.

## File Locations
- Views: `client/src/views/*.vue`
- Reusable components: `client/src/components/*.vue`
- Composables: `client/src/composables/` (useFilters, useI18n, useAuth)
- API client: `client/src/api.js`
- Backend routes + models: `server/main.py`
- Data loader: `server/mock_data.py`
- Mock data: `server/data/*.json`
- Tests: `tests/backend/` (conftest.py + 4 test files)
- Global styles: `client/src/App.vue`

## Design System
- Colors: Slate/gray (`#0f172a`, `#64748b`, `#e2e8f0`)
- Status colors: green (Delivered), blue (Shipped), yellow (Processing), red (Backordered/low stock)
- Charts: Custom SVG — no chart library
- Layouts: CSS Grid
- No emojis in UI
