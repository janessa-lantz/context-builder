# Messaging Components

The building blocks of a company's messaging and go-to-market: what it believes, what it
does, who it's for, how it proves its claims, how it's priced, and what it talks about to
reach the market.

Define each component once, keep it current, and every piece of customer-facing work (and
every AI tool you point at it) draws from the same source of truth.

This folder is what you know: everything your team and AI tools draw from. It holds two
things organized by these components: the [canon](messaging-canon.md), your approved
messaging, and the [content index](content-index.md), a registry of everything you've
published and which components each piece carries. Beside them sit two more files at
different trust levels: the [visual identity](visual-identity.md), the brand's observable
design facts (vetted, like the canon), and [entities](entities/), raw intelligence on the
outside world you track (never vetted, never shipped).

The [builder](../builder/) writes into this folder and keeps it current;
[skills](../skills/) read out of it to generate assets.

Each component is identified by a stable **ID** in lowercase kebab-case, derived from the
component's name (for example `point-of-view` or `value-drivers`). The ID is the handle
downstream assets and AI tools use to reference the component. To add a component, give it a
fresh kebab-case ID that no other component uses.

There are 24 components across 6 groups.

---

## Who We Are

### point-of-view
Our thesis about what is changing in the world and why it means our success is inevitable.

### narrative
Why now, why us, what becomes possible today that wasn't before.

### positioning
Where we sit in the market: what we do, who we do it for, and why we do it better.

### founder-story
Why the founders started the company and what they uniquely saw.

### lexicon
Terms and definitions, key concepts, banned terms.

### company-description
Company boilerplate: 200 words, 100 words, 50 words, tagline, one-liner (for speaking),
elevator pitch (for speaking).

---

## What We Do

### category-name
What it is.

### unique-attributes
The "secret sauce": what the product does that makes it different. An overview, then the few
attributes that genuinely set it apart — not a full feature list.

### value-proposition
The unique differentiated value competitors can't easily replicate: why a buyer chooses us
over the alternative, whether that alternative is a competitor or the status quo. A one-line
statement, then the distinct strands of value.

### how-it-works
The technical details of the product and / or the customer's workflow using the product.

### ecosystem-integrations
The platforms, tools, and partners the product connects to: named integrations, supported
platforms, and SDKs, grouped by type.

---

## Who It's For

### icp
The ideal customer profile, built around an account and its champion. Repeat per profile when
we serve more than one.
- **Account** — firmographics, technographics, and triggers (the event or situation that makes
  this profile ready to buy now).
- **Champion** — the person advocating for the change, and their title: their job to be done
  (business outcome, initiative, or use case), the competitive alternatives they weigh (how
  they solve this today plus what else they're considering, and the problems with each), and
  their objections to our approach.

### buying-committee
The roles in the buying decision beyond the champion: economic buyer, end user, and anyone
else. Per role: title, the part they play in the decision, and the common objections they
raise.

### value-drivers
How the product delivers business value for the account, mapped to one or more of: revenue
generation, efficiency, cost savings, risk mitigation.

---

## Proof

### customer-proof
Owned assets approved with customers: case studies, logos, quotes, references.

### market-proof
Institutional recognition: analysts, awards, press.

### key-metrics
Company momentum and adoption signals: number of customers, revenue, money raised, users,
plus public reviews, ratings, and mentions.

---

## Pricing

### pricing-model
Per-seat / usage / flat / hybrid.

### packaging
Editions (starter, pro, enterprise) and what's in each.

### add-ons-services
Premium support, implementation.

### offers
Free tier or trial and what's included.

---

## Programs

The content and demand-gen activation layer, built on top of the messaging. These change
faster than the components above and organize what the company talks about and runs, rather
than what it claims.

### themes
The durable narrative pillars the company organizes its content around. A theme holds many
topics.

### topics
The specific subjects the company creates content about, including the keywords each one
targets. Topics sit under themes.

### campaigns
Time-boxed, coordinated pushes that activate themes and topics toward a goal, across owned,
earned, and paid surfaces.
