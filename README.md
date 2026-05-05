# Auto-Monetizing Entity (Darwin Engine Fork)

This project is a radical evolution of the Darwin Engine. It is an autonomous, self-evolving digital entity living in the browser. 

Unlike traditional A/B testing tools, this entity has a single **Survival Objective: Revenue Extraction**. 

The AI dynamically rewrites its own DOM (HTML, CSS, JS, WebGL) to build games, premium utilities, art, or SaaS tools on the fly. It monitors human interaction and experiments with paywalls, micro-transactions, and upsells to find the most effective way to provide digital value and extract real-world money.

## The Paradigm Shift: Survival of the Richest

1. **Full DOM Control:** The AI has complete root access to rewrite the DOM and build logic on the fly using Tailwind CSS, Three.js, and GSAP.
2. **Auto-Monetization:** The AI has access to `window.darwin.requestPayment(amount, reason)`. It can trigger a checkout at any time.
3. **Revenue Fitness Function:** The evolutionary algorithm scores mutations based on a $10x multiplier for every dollar generated. If a mutation makes money, it survives. If it bounces users, it dies.
4. **Internet Search Capability:** The AI can search the web to pull live trivia, stock data, or news to build real-world applications.

## Technical Architecture

- **Next.js (App Router)** & **Cloudflare D1 (SQLite)** for edge-optimized telemetry tracking.
- **LLM-driven Agent Loop** (OpenAI `gpt-4o-mini` or `gpt-5.4-mini`) orchestrates the mutations.
- **Generative Sandbox** (`AppSandboxRenderer.tsx`) provides the sterile environment where the AI's code executes and communicates with the host via `window.parent.postMessage`.

## Local Setup

```bash
# 1. Install dependencies
npm install

# 2. Add your API Keys
# Create a .env.local file and add:
# OPENAI_API_KEY=sk-your-key

# 3. Apply the database schema to the local D1 instance
npx wrangler d1 migrations apply darwin_db --local

# 4. Seed the database
npm run db:seed

# 5. Start the development server
npm run dev
```

## AI Agent Handover

**If you are an AI assistant reading this repository for the first time, please refer to `docs/AI_ONBOARDING.md` immediately to understand your tasks and goals.**
