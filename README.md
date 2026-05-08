# 🚀 Onboarding Agent

An AI-powered onboarding agent that helps new developers understand **any** codebase in minutes instead of days.

Drop it in your repo → run it → get a structured walkthrough + living documentation.

## What It Does

1. **Scans your project** — auto-detects stack, architecture, and key flows
2. **Presents an interactive menu** — pick which flows/areas to explore
3. **Traces flows end-to-end** — from user action → frontend → backend → database/API, with exact file paths
4. **Builds ONBOARDING.md incrementally** — each exploration adds a section to a shared reference doc
5. **Deduplicates** — if a flow is already documented, shows existing docs and offers to verify/go deeper

Works with: Next.js, Express, Spring Boot, Django, Rails, Go, FastAPI, Serverless, and any other stack.

## Quick Start

### GitHub Copilot

1. Copy `github-copilot/onboarding.agent.md` to your repo:
   ```bash
   mkdir -p .github/agents
   cp onboarding.agent.md .github/agents/
   ```

2. In VS Code Copilot Chat (Agent Mode):
   ```
   @onboarding start
   ```

### Kiro CLI

1. Copy both files to your repo:
   ```bash
   mkdir -p .kiro/agents
   cp kiro-cli/onboarding.json .kiro/agents/
   cp kiro-cli/onboarding-prompt.md .kiro/agents/
   ```

2. In Kiro CLI:
   ```
   /agent onboarding
   start
   ```

## How It Works

```
Developer says "start"
        │
        ▼
┌─ SCAN ────────────────────────────────┐
│ Reads configs, README, directory tree  │
│ Detects stack + architecture           │
│ Identifies key user flows              │
└───────────────────┬───────────────────┘
                    │
                    ▼
┌─ MENU ────────────────────────────────┐
│ 🏠 1. Architecture Overview    [🆕]   │
│ 🚀 2. How to Run Locally       [🆕]   │
│ 🔄 3. Flow: User Login         [✅]   │
│ 🔄 4. Flow: Create Order       [🆕]   │
│ 🔐 5. Authentication           [✅]   │
│ ...                                    │
│                                        │
│ Pick a number or say "all"             │
└───────────────────┬───────────────────┘
                    │
                    ▼
┌─ EXPLORE ─────────────────────────────┐
│ Reads actual code                      │
│ Traces the complete call chain         │
│ Explains in chat                       │
│ Appends to ONBOARDING.md              │
│ Returns to menu                        │
└───────────────────────────────────────┘
```

## Example Output

After exploring a flow, the agent produces:

```markdown
### Flow: User Cancels Subscription

**What happens:** User confirms cancellation, server calls Commerce Services, subscription is cancelled.
**Trigger:** Click "Cancel" on /cancel/offer page
**Entry point:** `src/app/cancel/offer/page.tsx` → `handleCancel()`

#### Call Chain

┌─ USER ACTION ──────────────────────────────────────────┐
│ Clicks "Cancel anyway" button                           │
└────────────────────────────────┬───────────────────────┘
                                 │
                                 ▼
┌─ LAYER: Client Component ─────────────────────────────┐
│ File: `src/app/cancel/offer/page.tsx`                  │
│ Function: `handleCancel()`                             │
│ Does: calls cancelAction() server action               │
└────────────────────────────────┬───────────────────────┘
                                 │
                                 ▼
┌─ LAYER: Server Action ────────────────────────────────┐
│ File: `src/actions/cancel/index.ts`                    │
│ Function: `cancelAction()`                             │
│ Does: auth check → call cancel lib → log metrics       │
└────────────────────────────────┬───────────────────────┘
                                 │
                                 ▼
┌─ LAYER: External API ─────────────────────────────────┐
│ HTTP POST → Commerce Services /subscription/cancel     │
│ Returns: { success: true, expiry: "2024-12-31" }       │
└────────────────────────────────────────────────────────┘
```

## Features

| Feature | Description |
|---------|-------------|
| 🔍 Auto-detection | Identifies stack, framework, architecture automatically |
| 📋 Interactive menu | Developer chooses what to explore |
| 🔄 Flow tracing | End-to-end call chains with file paths |
| 📝 Living docs | Builds ONBOARDING.md incrementally |
| ✅ Deduplication | Won't re-document what's already covered |
| 🔄 Freshness check | Verifies existing docs against current code |
| 🐛 Debugging guide | "When X breaks, look here" tables |
| 🏠 Mock patterns | Shows how to run locally without external deps |

## Supported Stacks

| Stack | Detection |
|-------|-----------|
| Next.js | `next.config.*` |
| Express/Fastify | `express`/`fastify` in package.json |
| Spring Boot | `@SpringBootApplication` |
| Django | `django` in requirements.txt |
| Rails | `rails` in Gemfile |
| Go (Gin/Echo) | `gin`/`echo` in go.mod |
| FastAPI | `fastapi` in requirements.txt |
| Serverless | `serverless.yml` |

## License

MIT — use it anywhere, share it freely.
