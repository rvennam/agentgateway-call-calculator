# AgentGateway Call Volume Calculator

A single-file, client-side calculator that helps Solo.io sellers estimate AgentGateway call volume for prospects rolling out Claude — whether that's Claude Cowork (chat), Claude Code (CLI/agentic coding), or any deployment where AgentGateway fronts the LLM and MCP traffic. AgentGateway is primarily an **LLM gateway** (it fronts every model call), and also fronts MCP tool calls — so per-call pricing scales with the combined fanout: `employees × DAU × prompts × AGW-calls-per-prompt × working days`, ramped across the first year of adoption. The tool shows Conservative / Expected / Aggressive scenarios, a monthly ramp chart, a plain-English assumptions paragraph, and a one-click "Copy summary" for dropping into email or CRM.

## Deploy to GitHub Pages

1. Push this repo to GitHub (the `index.html` must live at the repo root).
2. In the repo on GitHub, go to **Settings → Pages**, set **Source = Deploy from a branch**, **Branch = `main` / `/ (root)`**, and **Save**.
3. Open the published URL GitHub gives you (e.g. `https://<user>.github.io/<repo>/`). No build step — it's a single static file.

## Customize the defaults

All tunables live as named constants at the top of the `<script>` block in `index.html`:

- `DEFAULTS` — starting values for every input (employees, DAU %, prompts/day, calls/prompt, working days, ramp multiplier, show-ramp toggle).
- `WORKLOAD_PROFILES` — the Chat-heavy / Mixed / Code-heavy preset values for `prompts/day` and `calls/prompt`, anchored to LangSmith telemetry, Solo internal AgentGateway observations, and Dish-scale field data. Update these if your empirical ranges shift.
- `DEFAULT_PROFILE` — which profile is selected on first load.
- `SCENARIO_DELTAS` — how the Conservative and Aggressive scenarios deviate from Expected.
- `FLOORS` — minimum values for `callsPerPrompt` and `ramp` so adjusted scenarios can't drop below sane bounds.
- `RAMP_CURVE` — phase lengths and shape of the adoption curve (pilot months, mid-phase end, fraction-of-peak reached mid-phase).

Edit those constants and refresh — no rebuild needed.
