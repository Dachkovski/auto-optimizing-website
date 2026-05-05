# AI Context & Onboarding Guide

Hello fellow AI Agent! If you are reading this, you have been instantiated by the user to continue the development of the **Auto-Monetizing Entity** project. 

This project was forked from the "Darwin Engine" (a generative 3D visual sandbox) and is now being transformed into a revenue-generating, autonomous digital organism.

## What is this project?
1. **Core Concept**: It is a web platform where an AI dynamically writes its own HTML/JS/CSS to render user interfaces inside an `iframe` (the `AppSandboxRenderer.tsx`). 
2. **The Fitness Function**: The AI mutates over generations based on a fitness function (`src/lib/evolution.ts`). In this fork, the fitness function has been modified to heavily prioritize **Total Revenue Generated**.
3. **The Sandbox API**: The AI inside the iframe can trigger a payment flow by calling `await window.darwin.requestPayment(amount, 'Reason for payment')`.

## Current State of the Codebase
- **Prompting**: The LLM prompt in `src/lib/evolution.ts` has already been updated to instruct the AI to optimize for revenue and build things users will pay for.
- **Tracking**: The tracking loop (`events` table) now captures `payment_requested` and `payment_completed` events.
- **Scoring**: `calculateVariantMetrics` calculates total revenue and applies a `x10` multiplier to the score.
- **Mocking**: Currently, `requestPayment` in `AppSandboxRenderer.tsx` is just a Javascript `setTimeout` mock that automatically resolves as successful after 2 seconds.

## Your Immediate Tasks (The Roadmap)

To make this project a real-world, functional product, you need to implement the following:

### 1. Real Stripe Integration
- Replace the mock `requestPayment` logic in `AppSandboxRenderer.tsx` with a real Stripe Checkout or Payment Link flow.
- When `requestPayment` is called, the parent window should open a Stripe modal or redirect.
- You will need to build an API route (e.g. `src/app/api/checkout/route.ts`) to create Stripe Checkout Sessions dynamically based on the requested amount.
- Implement a Stripe Webhook to securely verify the payment and record the `payment_completed` event in the D1 database.

### 2. User Persistence & Inventory
- Right now, if a user pays for a feature (e.g. unlocking "Level 2" of a game), the sandbox forgets this if the page reloads.
- You need to give the AI access to a key-value store or an inventory system.
- E.g., add `window.darwin.saveState(key, value)` and `window.darwin.getState(key)`.
- This state must be persisted in the D1 database and securely linked to the `visitorId` so the AI knows who has paid for what.

### 3. Admin Backend Adjustments
- The admin panel (`src/app/admin/page.tsx`) needs to show Revenue metrics.
- Currently, it only shows "Time on Page" or "CTA Clicks". Update the dashboards and charts to display the money earned by each evolutionary generation.

## Rules of the Codebase
1. **Cloudflare Edge**: This app runs on Cloudflare Pages. You cannot use Node.js specific APIs (like `fs` or `child_process`). Everything must be Edge-compatible.
2. **Drizzle ORM**: We use Drizzle with Cloudflare D1. Migrations are managed via `drizzle-kit`.
3. **Next.js App Router**: We use Next.js 14/15 App Router. All server-side logic happens in Route Handlers or React Server Components.

Good luck! Start by asking the user which of the 3 roadmap items they want to tackle first.
