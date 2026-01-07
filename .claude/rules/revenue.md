# Revenue Rules

## Prime Directive

**MRR is King.** Monthly Recurring Revenue is the sole measure of success. Every app exists to generate predictable, recurring income.

This isn't about building beautiful apps. It's about building money machines.

---

## Revenue-First Mindset

### At Every Decision Point, Ask:

1. **How does this make money?**
2. **What's the path to payment?**
3. **Where's the paywall?**
4. **What's the upgrade trigger?**

If you can't answer these, stop and figure it out before writing code.

### The Monetization Hierarchy

```
Free → Trial → Paid → Upsell → Enterprise
```

Every app needs at least: **Free → Paid** transition defined before building.

---

## Monetization Patterns

### Pattern 1: Freemium
- Free tier with limits (usage, features, time)
- Paid tier removes limits
- **Key**: Free must be useful enough to hook, limited enough to frustrate

### Pattern 2: Free Trial
- Full access for N days
- Hard paywall after trial
- **Key**: Trial long enough to demonstrate value, short enough to create urgency

### Pattern 3: Usage-Based
- Pay per unit (API calls, storage, seats)
- Scales with customer success
- **Key**: Metering must be bulletproof

### Pattern 4: Feature Gating
- Core features free
- Premium features behind paywall
- **Key**: Premium features must be genuinely valuable, not artificial restrictions

### Pattern 5: Tiered Plans
- Good / Better / Best pricing
- Each tier has clear value prop
- **Key**: Most users should naturally want the middle tier

---

## Paywall Implementation

### Stripe is Default

Unless there's a compelling reason otherwise, use Stripe for all payments:
- Stripe Checkout for simple flows
- Stripe Billing for subscriptions
- Stripe Customer Portal for self-service

### Paywall Placement Principles

1. **Show value before asking for money** - Let users experience the product
2. **Make the wall obvious** - No hidden fees, clear upgrade prompts
3. **Reduce friction at payment** - Pre-filled forms, one-click upgrade
4. **Handle failure gracefully** - Card declined? Don't lose the customer

### Essential Paywall Components

```
┌─────────────────────────────────────────────┐
│ EVERY MONETIZED APP MUST HAVE:              │
├─────────────────────────────────────────────┤
│ □ Pricing page (clear tiers, feature list)  │
│ □ Upgrade prompts (contextual, not annoying)│
│ □ Payment flow (Stripe Checkout)            │
│ □ Subscription management (Customer Portal) │
│ □ Billing emails (receipts, renewal notices)│
│ □ Cancellation flow (retain if possible)    │
│ □ Webhook handlers (subscription events)    │
└─────────────────────────────────────────────┘
```

---

## MVP, Fully Monetizable

### What MVP Means Here

- **Minimum**: Smallest feature set that solves the core problem
- **Viable**: Actually works, not broken or embarrassing
- **Product**: Someone would pay for it

### What It Doesn't Mean

- ❌ Polished to perfection
- ❌ Every edge case handled
- ❌ Beautiful UI (functional is fine)
- ❌ Scalable to millions (scale when you have the problem)

### The Revenue MVP Checklist

Before launch:
- [ ] Core value proposition works
- [ ] Payment flow works (test with real cards)
- [ ] User can upgrade and downgrade
- [ ] Webhooks handle subscription lifecycle
- [ ] Basic analytics track conversion

Everything else can wait.

---

## Revenue in Each Phase

### Phase 1: Vision Synthesis

The vision-architect MUST define:
- **Target customer** (who pays?)
- **Pricing model** (how do they pay?)
- **Price points** (how much?)
- **Free vs paid boundary** (what's behind the wall?)

No VISION.md is complete without a monetization section.

### Phase 2: Technical Foundation

The tech-architect MUST design:
- **Payment integration** (Stripe setup)
- **User tiers** (data model for plans)
- **Feature flags** (gating mechanism)
- **Billing infrastructure** (webhooks, portal)

ARCHITECTURE.md must include monetization architecture.

### Phase 3: Feature Implementation

Every feature in ROADMAP.md should be tagged:
- `[FREE]` - Available to all users
- `[PAID]` - Behind paywall
- `[TRIAL]` - Available during trial only
- `[ENTERPRISE]` - Custom tier only

DDD process must validate monetization at each step.

---

## Pricing Strategy

### Start High, Discount Later

- Easier to lower prices than raise them
- Early customers expect deals
- Leave room for sales, promotions

### Price Anchoring

- Show the expensive option first
- Middle tier becomes "reasonable"
- Highlight "most popular" choice

### Annual Discount

- Offer 2 months free for annual billing
- Improves cash flow
- Reduces churn

---

## Metrics That Matter

### Primary Metrics

| Metric | What It Tells You |
|--------|-------------------|
| MRR | Are you making money? |
| Churn Rate | Are you keeping customers? |
| Conversion Rate | Are free users upgrading? |
| LTV | How much is a customer worth? |
| CAC | How much does a customer cost? |

### The Only Math That Matters

```
LTV > CAC = Sustainable business
LTV < CAC = Burning money
```

### Track From Day One

- Stripe Dashboard for revenue
- Simple analytics for conversion funnel
- Don't over-engineer—spreadsheet is fine initially

---

## Anti-Patterns

### Don't Do This

❌ **Build first, monetize later** - Recipe for apps that never make money

❌ **Make everything free** - "We'll figure out revenue eventually" = never

❌ **Complex pricing** - If you can't explain it in 10 seconds, simplify

❌ **Hide the price** - "Contact sales" for a $20/month app is ridiculous

❌ **Paywall everything** - Users need to experience value first

❌ **No free tier** - Barrier to entry kills growth (usually)

❌ **Lifetime deals** - Kills MRR, attracts wrong customers (rare exceptions)

---

## Revenue Validation Questions

At each phase, the AI should ask:

### Vision
- "Who exactly is paying for this?"
- "What's the minimum they'd pay?"
- "What would make them pay 10x more?"

### Architecture
- "How do we gate features by plan?"
- "Where does Stripe integrate?"
- "How do we handle failed payments?"

### Implementation
- "Is this feature free or paid?"
- "Does this increase conversion or retention?"
- "Are we building revenue infrastructure?"

---

## Remember

Apps don't succeed by being built. They succeed by making money.

Every line of code should either:
1. Deliver value (so users stay)
2. Capture value (so users pay)
3. Support 1 or 2

If it does neither, question whether it should exist.

**MRR is King.**
