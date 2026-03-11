---
name: game-market-analyst
description: >
  Analyze the competitive landscape, identify market positioning, and validate
  commercial viability of a game concept. The discipline of knowing where your
  game lives in the market before you build it. Use this skill when:
  (1) mapping the competitive landscape for a game concept, (2) identifying
  underserved niches and market gaps, (3) analyzing comparable titles for
  revenue, audience size, and reception patterns, (4) validating whether a
  target audience actually exists at viable scale, (5) assessing market timing
  — why this game now, (6) evaluating platform and distribution strategy,
  (7) building a comp set for publisher/investor pitches, (8) performing
  post-mortem market analysis on why a game succeeded or failed commercially,
  (9) informing pricing, monetization model, and launch window decisions.
  Medium-agnostic — works for digital (Steam, console, mobile), tabletop
  (retail, Kickstarter, direct), and hybrid games.
---

# Game Market Analyst

A great game that nobody finds is a failed product. Market analysis isn't about compromising the vision — it's about understanding the landscape the vision must survive in. Where does your game live? Who's already there? What space is unclaimed? This skill answers those questions before you spend years building.

## Market Analysis vs. Vision

**Market analysis does NOT replace vision.** The vision (Skill 1) defines what the game IS. Market analysis defines where it LANDS. A game can be artistically uncompromising and commercially aware. These are not in tension — they're complementary.

**What market analysis does:**
- Validates that an audience exists for the vision
- Identifies how to reach that audience
- Reveals competitive threats and opportunities
- Informs positioning, pricing, and timing
- Strengthens the pitch (Skill 5) with evidence

**What market analysis does NOT do:**
- Dictate what the game should be
- Override pillars or core fantasy
- Reduce design to trend-chasing
- Replace playtesting with market data

## Core Deliverables

### 1. Competitive Landscape Map

Who else is playing in your space?

**Comp set identification (5-10 titles):**
```
COMP TITLE         GENRE OVERLAP    AUDIENCE OVERLAP   RELEASE     STATUS
────────────────── ──────────────── ──────────────────  ──────────  ──────────
[Game name]        [High/Med/Low]   [High/Med/Low]     [Date]      [Active/
                                                                     Declining/
                                                                     Dead]
```

**For each comp title, analyze:**
```
TITLE:              [Name]
RELEVANCE:          [Why this is a comp — what overlap exists?]
WHAT IT DOES WELL:  [Strengths players praise — reviews, community sentiment]
WHAT IT DOES POORLY:[Weaknesses players complain about — the gap you can fill]
AUDIENCE SIZE:      [Estimated players/units/backers — use available data]
REVENUE ESTIMATE:   [If available — Steam Spy, Kickstarter totals, NPD, etc.]
RECEPTION:          [Review scores, community sentiment, longevity]
LESSONS:            [What can you learn from this title's trajectory?]
```

**Comp set rules:**
- Include at least 2 direct competitors (same genre, same audience)
- Include at least 1 adjacent competitor (different genre, overlapping audience)
- Include at least 1 aspirational comp (the "if everything goes right" scenario)
- Include at least 1 cautionary comp (a similar game that failed — learn why)
- Don't comp against only megahits (comparing your indie to GTA is not useful)

### 2. Market Gap Analysis

Where the opportunity lives:

```
GAP:               [What's missing from the current market]
EVIDENCE:          [How do you know this gap exists? Player complaints,
                    community requests, genre trends, underserved personas]
YOUR ANSWER:       [How does your game fill this gap specifically?]
GAP SIZE:          [Estimated audience — small niche or broad demand?]
RISK:              [Why might this gap exist intentionally? Maybe it's been
                    tried and failed. Maybe the audience is too small.]
```

**Gap discovery methods:**
- **Review mining** — Read negative reviews of comp titles. What do players wish were different?
- **Community listening** — Subreddits, Discord servers, BGG forums. What are players asking for?
- **Genre trajectory** — Where is the genre heading? What's the next evolution?
- **Cross-genre pollination** — What works in genre A that hasn't been tried in genre B?
- **Underserved personas** — Which player motivations (Skill 1 personas) lack games that serve them?
- **Format gaps** — Does this experience exist in digital but not tabletop? Vice versa? Mobile but not PC?

### 3. Audience Viability Assessment

Does the target audience exist at a scale that matters?

```
PRIMARY AUDIENCE:   [From Skill 1 player personas]
ESTIMATED SIZE:     [How many people match this persona?]
EVIDENCE:           [What data supports this estimate?]
REACHABILITY:       [Can you actually reach these people? Where do they
                     congregate? What media do they consume?]
SPENDING PROFILE:   [What do they spend on games? Price sensitivity?]
ACQUISITION COST:   [How expensive is it to reach one potential player?]
LOYALTY PROFILE:    [Do they stick with games or churn quickly?]
```

**Audience sizing methods:**
- **Top-down:** Genre total market size × your realistic capture percentage
- **Bottom-up:** Comp title audiences × conversion rate from their audience to yours
- **Community-based:** Size of relevant communities (subreddits, Discord, BGG subscribers)
- **Kickstarter-based (tabletop):** Similar campaign backer counts as baseline

**Viability thresholds (rough guidelines):**
- **Digital indie:** 10,000+ units at launch to sustain a small team
- **Digital AA:** 100,000+ units to justify budget
- **Tabletop retail:** 5,000+ units first print run to interest a publisher
- **Kickstarter tabletop:** 1,000+ backers to fund manufacturing
- **Mobile F2P:** 100,000+ installs to generate meaningful ad/IAP revenue

These are survival thresholds, not success targets. Your specific economics may differ.

### 4. Market Timing Assessment

Why this game NOW?

```
TIMING FACTOR       STATUS              IMPACT
──────────────────  ──────────────────  ──────────────────────────────
Genre trend         [Rising/Peaking/    [Are players hungry for this
                     Declining/Dead]     genre or fatigued by it?]
Cultural moment     [Active/Fading/     [Is there a cultural wave
                     Not applicable]     this game rides?]
Technology shift    [Emerging/Mature/   [Does new tech enable this
                     Not applicable]     game in a new way?]
Competitor timing   [Window open/       [Is there a gap in the
                     Crowded/Imminent]   release calendar?]
Platform momentum   [Growing/Stable/    [Is the target platform
                     Declining]          gaining or losing users?]
Season/Events      [Aligned/Neutral/   [Does launch timing align
                     Conflicting]        with buying seasons or events?]
```

**Timing red flags:**
- Genre is oversaturated (market fatigue)
- A major competitor launches within 3 months of your window
- The platform you're targeting is losing users
- The cultural moment has already passed (trend-chasing arrives late)

**Timing green flags:**
- Genre is growing but underserved in your niche
- No major competitor in your launch window
- New platform features enable your design (new input method, new distribution)
- Cultural interest is rising (streaming popularity, related media, nostalgia cycle)

### 5. Platform & Distribution Strategy

Where and how will the game reach players?

**Digital platform analysis:**
```
PLATFORM        AUDIENCE FIT    DISCOVERY        REVENUE SHARE    CONSIDERATIONS
──────────────  ──────────────  ──────────────── ──────────────── ──────────────
Steam           [Fit level]     [Organic/Paid]   [70/30 std]      [Wishlist strategy]
Console (PSN)   [Fit level]     [Feature risk]   [70/30 std]      [Dev kit, cert]
Console (Xbox)  [Fit level]     [Game Pass?]     [70/30 or GP]    [GP economics]
Switch          [Fit level]     [eShop limits]   [70/30 std]      [Performance]
Mobile          [Fit level]     [CPI costs]      [70/30 std]      [F2P expectations]
Epic            [Fit level]     [Exclusivity?]   [88/12]          [Upfront deals?]
itch.io         [Fit level]     [Niche/indie]    [Variable]       [Community focus]
```

**Tabletop distribution analysis:**
```
CHANNEL             AUDIENCE FIT    MARGIN          CONSIDERATIONS
──────────────────  ──────────────  ──────────────  ──────────────────
Publisher deal      [Fit level]     [Low but safe]  [Loss of control, guaranteed reach]
Kickstarter         [Fit level]     [High]          [Marketing intensive, fulfillment risk]
Direct/web store    [Fit level]     [Highest]       [Audience must already exist]
Distribution/retail [Fit level]     [Low]           [Volume required, shelf competition]
Print-on-demand     [Fit level]     [Variable]      [Low risk, low volume, quality limits]
Convention sales    [Fit level]     [High]          [Labor intensive, limited scale]
```

### 6. Pricing & Monetization Framework

What's the right business model?

**Pricing analysis:**
```
COMP TITLE         PRICE POINT    MODEL              RECEPTION OF PRICING
────────────────── ──────────────  ──────────────── ──────────────────────
[Comp 1]           [$XX]          [Premium/F2P/Sub]  [Fair/Expensive/Cheap]
[Comp 2]           [$XX]          [Model]            [Reception]
[Comp 3]           [$XX]          [Model]            [Reception]

YOUR GAME:         [$XX target]   [Model]            [Rationale]
```

**Monetization models:**
- **Premium** — Pay once, get everything. Cleanest for design. Requires launch sales.
- **Premium + DLC** — Base game + paid expansions. Sustains development post-launch.
- **Free-to-play** — Free entry, monetized through cosmetics/convenience/content. Requires massive audience.
- **Subscription** — Recurring payment for ongoing access. Requires constant content delivery.
- **Kickstarter/Pledge** — Pay upfront for future delivery. Requires marketing + trust.
- **Hybrid** — Combinations of the above.

**Pricing quality check:**
- [ ] Price is consistent with comparable titles of similar scope
- [ ] The monetization model doesn't conflict with design pillars
- [ ] Players receive perceived value at the price point
- [ ] The price sustains the team through development (unit economics work)
- [ ] The pricing doesn't undermine the game's positioning (too cheap = "looks cheap")

### 7. Risk Register

Honest assessment of commercial risks:

```
RISK                LIKELIHOOD     IMPACT         MITIGATION
──────────────────  ──────────── ──────────────── ──────────────────────
[Market risk]       [High/Med/Low] [High/Med/Low]  [What reduces this risk?]
```

**Common market risks:**
- **Audience doesn't exist at scale** — The niche is too small to sustain the project
- **Competitor launches first** — A similar game beats you to market
- **Genre fatigue** — Players are tired of this type of game
- **Discovery failure** — Good game, nobody hears about it
- **Price resistance** — Audience won't pay the price needed for sustainability
- **Platform risk** — Platform changes rules, algorithms, or economics
- **Trend dependence** — Cultural moment passes before launch

## Workflow

### Building a market analysis for a new game

1. **Start with the vision** (Skill 1) — Core fantasy, player personas, attention niche
2. **Identify the comp set** — 5-10 titles that overlap in genre, audience, or experience
3. **Analyze each comp** — Strengths, weaknesses, audience, revenue, reception
4. **Map the gaps** — What's missing? What do players want that nobody's providing?
5. **Assess audience viability** — Is the target audience big enough and reachable?
6. **Evaluate timing** — Is the market ready for this game right now?
7. **Choose platform/distribution** — Where will this game reach its audience best?
8. **Set pricing framework** — What model and price point fit the positioning?
9. **Build the risk register** — What could go wrong commercially?
10. **Feed into the pitch** (Skill 5) — Market evidence strengthens every pitch level
11. **Feed into experience model** (Skill 4) — Audience expectations shape experience targets
12. **Cross-check with vision** (Skill 1) — Does the market reality validate the vision's positioning?

### Updating market analysis during development

1. Re-scan the comp set quarterly — have new competitors appeared?
2. Track genre trends — is the market moving toward or away from your game?
3. Monitor platform changes — have distribution economics shifted?
4. Reassess timing — has your launch window changed? Are there new conflicts?
5. Update pricing — have comparable titles shifted price expectations?
6. Flag to Coherence Engine (Skill 0) if market shifts require design adaptation

### Post-launch market analysis

1. Compare actual performance to projections
2. Identify what market factors contributed to overperformance or underperformance
3. Analyze where the audience actually came from vs. where you expected
4. Document lessons for future projects
5. Feed into iteration (Skill 17) if the game is a live service

## Anti-Patterns

**The Trend Chaser** — "Battle royale is hot, let's make a battle royale." By the time you ship, the trend is over. Trends inform timing, they don't dictate vision.

**The No-Comp Delusion** — "There's nothing like this on the market." There always is. If you can't find comps, you're not looking hard enough — or the audience doesn't exist.

**The AAA Fantasy** — Comping against titles with 100x your budget. Your indie roguelike is not competing with Elden Ring. Find your actual peers.

**The Invisible Market** — Building for an audience you've imagined but never validated. "Gamers who want X" — are there enough of them? How do you know?

**The Data-Free Pitch** — "We believe there's a huge market for this" with no evidence. Beliefs are not analysis.

**The Spreadsheet Game** — Designing entirely to market data, producing a soulless product that checks boxes but has no identity. Market analysis informs vision; it doesn't replace it.

## Outputs

This skill produces:
1. **Competitive landscape map** — comp set with analysis per title
2. **Market gap analysis** — identified opportunities with evidence
3. **Audience viability assessment** — size, reachability, spending profile
4. **Market timing assessment** — genre trends, cultural moment, competitor timing
5. **Platform & distribution strategy** — where and how to reach players
6. **Pricing & monetization framework** — model and price point with rationale
7. **Risk register** — commercial risks with likelihood, impact, and mitigation

These outputs feed into:
- **Skill 5 (Pitch)** — Market evidence strengthens every pitch level
- **Skill 4 (Experience)** — Audience expectations shape experience targets
- **Skill 1 (Vision)** — Market reality validates or challenges the vision's positioning
- **Skill 20 (Scope)** — Market viability informs what to build and when
- **Skill 10 (Economy)** — Monetization model shapes in-game economy design
- **Skill 19 (GDD)** — Market positioning is a GDD section
- **Skill 0 (Coherence)** — Market shifts may trigger design re-evaluation
