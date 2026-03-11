---
name: competitive-analysis
description: |
  Game industry competitive analysis framework for product managers.
  Provides structured methodologies for analyzing competing games, studios, and market positioning.
  Use when: (1) mapping the competitive landscape for a game genre or product,
  (2) building feature comparison matrices across competing titles,
  (3) analyzing positioning, monetization, or UA strategy differences,
  (4) conducting win/loss analysis on player acquisition and churn,
  (5) identifying market trends, genre shifts, and platform changes,
  (6) creating competitive intelligence briefs with web research.
  Triggers: "competitive analysis", "competitor research", "竞品分析", "竞争对手",
  "竞品调研", "市场分析", "competitor comparison", "market positioning",
  "feature matrix", "win loss analysis", "genre analysis", "品类分析",
  "竞品报告", "市场调研", "对标分析"
---

# Competitive Analysis - Game Industry Framework

A structured competitive analysis system designed for game product managers (游戏产品负责人). Provides frameworks for landscape mapping, feature comparison, positioning analysis, win/loss methodology, and market trend identification — all adapted for the game industry context.

## Table of Contents

1. [Competitive Landscape Mapping](#1-competitive-landscape-mapping-竞争格局)
2. [Feature Comparison Matrix](#2-feature-comparison-matrix-竞品特征矩阵)
3. [Positioning Analysis](#3-positioning-analysis-市场定位分析)
4. [Win/Loss Analysis](#4-winloss-analysis-竞争得失分析)
5. [Market Trend Identification](#5-market-trend-identification-市场趋势识别)
6. [/competitive-brief Command Workflow](#6-competitive-brief-command-workflow)
7. [Web Research Guide](#7-web-research-guide-情报收集)
8. [Templates & Quick Reference](#8-templates--quick-reference)
9. [LiveOps Comparison Framework](#9-liveops-comparison-framework-运营对比)
10. [Ad Creative Teardown Template](#10-ad-creative-teardown-template-素材拆解)
11. [Retention vs Monetization Trade-off](#11-retention-vs-monetization-trade-off-留存-变现权衡)
12. [Data Source Guide](#12-data-source-guide-数据源指南)
13. [China Market Analysis](#13-china-market-analysis-中国市场分析)
14. [Competitor Response Modeling](#14-competitor-response-modeling-竞争应对建模)

---

## 1. Competitive Landscape Mapping (竞争格局)

Map the full competitive environment by categorizing competitors into four tiers. This prevents tunnel vision on direct competitors while revealing threats from adjacent categories.

### Competitor Categories

| Category | Definition | Game Industry Examples |
|----------|-----------|----------------------|
| **Direct Competitors** (直接竞品) | Same genre, same target audience, same platform | Two open-world RPGs on mobile targeting mid-core players |
| **Indirect Competitors** (间接竞品) | Different genre, competes for same player time/spend | A gacha RPG vs a gacha card game — different gameplay, same spending audience |
| **Adjacent Competitors** (相邻竞品) | Same platform, different genre, shares some mechanics | Battle royale vs extraction shooter — both competitive multiplayer |
| **Substitute Competitors** (替代竞品) | Different platform, same genre, targets similar audience | Mobile RPG vs PC MMORPG targeting fantasy RPG fans |

### Mapping Framework

```
[Your Game] ← Center
├── Direct: Same genre + same platform + same audience
├── Indirect: Different genre + same spend/time
├── Adjacent: Same platform + overlapping mechanics
└── Substitute: Same genre + different platform
```

### Analysis Questions

1. **Direct Competition Analysis**
   - What are their core mechanics and unique selling propositions?
   - How do their monetization and live ops compare?
   - What is their market share and growth trajectory?

2. **Indirect Competition Analysis**
   - What player needs do they satisfy that overlaps with yours?
   - How do their engagement patterns compare?
   - What can you learn from their retention strategies?

3. **Adjacent Competition Analysis**
   - What mechanics can you borrow or improve upon?
   - How do they handle similar systems (e.g., progression, social)?
   - What are their technical and design innovations?

4. **Substitute Competition Analysis**
   - Why do players choose their platform over yours?
   - What platform-specific advantages do they leverage?
   - How can you differentiate your platform experience?

---

## 2. Feature Comparison Matrix (竞品特征矩阵)

Create comprehensive feature matrices to systematically compare competing games across multiple dimensions.

### Matrix Structure

| Feature Category | Your Game | Competitor A | Competitor B | Competitor C | Market Standard |
|------------------|-----------|--------------|--------------|--------------|-----------------|
| **Core Gameplay** | | | | | |
| Combat System | ✓ | ✓ | ✓ | ✗ | ✓ |
| Progression | ✓ | ✓ | ✗ | ✓ | ✓ |
| **Monetization** | | | | | |
| Gacha | ✓ | ✓ | ✗ | ✓ | ✓ |
| Battle Pass | ✓ | ✗ | ✓ | ✓ | ✓ |
| **Live Ops** | | | | | |
| Daily Events | ✓ | ✓ | ✓ | ✗ | ✓ |
| Seasonal Events | ✓ | ✗ | ✓ | ✓ | ✓ |

### Feature Analysis Framework

#### 1. Feature Presence Analysis
- **Must-Have Features**: Features present in >75% of successful competitors
- **Differentiating Features**: Unique features that set you apart
- **Missing Features**: Important features you lack but competitors have
- **Innovative Features**: Features not present in any competitor

#### 2. Feature Quality Assessment
- **Implementation Quality**: How well is the feature executed?
- **Player Reception**: How do players rate this feature?
- **Revenue Impact**: How does this feature drive monetization?
- **Retention Impact**: How does this feature affect player retention?

#### 3. Feature Opportunity Scoring
```
Opportunity Score = (Market Gap × Player Demand × Implementation Feasibility)
- Market Gap: How many competitors lack this feature?
- Player Demand: How much do players want this feature?
- Implementation Feasibility: How difficult is it to implement?
```

---

## 3. Positioning Analysis (市场定位分析)

Analyze how competitors position themselves in the market and identify positioning opportunities.

### Positioning Dimensions

#### 1. Price/Quality Matrix
```
High Quality ┌──────────────┐
            │ Premium      │
            │ Positioning  │
Low Quality ├──────────────┤
            │ Budget       │
            │ Positioning  │
            └──────────────┘
            Low Price    High Price
```

#### 2. Target Audience Positioning
- **Casual**: Low commitment, broad appeal
- **Mid-Core**: Moderate commitment, genre enthusiasts
- **Hardcore**: High commitment, dedicated players
- **Niche**: Specialized interests, specific communities

#### 3. Platform Positioning
- **Mobile First**: Optimized for mobile experience
- **Cross-Platform**: Unified experience across platforms
- **PC/Console Focused**: High-end gaming experience

### Positioning Analysis Framework

#### 1. Competitor Positioning Map
```
[Visual Map]
Y-Axis: Price Point (Low to High)
X-Axis: Complexity (Simple to Complex)
Plot each competitor and identify gaps
```

#### 2. Messaging Analysis
- **Value Proposition**: What is their core promise to players?
- **Brand Voice**: How do they communicate with players?
- **Marketing Channels**: Where do they acquire players?
- **Community Engagement**: How do they build player communities?

#### 3. Success Factor Analysis
- **Key Success Factors**: What makes them successful?
- **Differentiation Strategy**: How do they stand out?
- **Market Niche**: What specific segment do they target?
- **Growth Strategy**: How are they expanding their market?

---

## 4. Win/Loss Analysis (竞争得失分析)

Systematically analyze why players choose your game over competitors (wins) and vice versa (losses).

### Win/Loss Data Collection

#### 1. Player Acquisition Sources
- **Marketing Channels**: Where do players come from?
- **Conversion Rates**: How effective is each channel?
- **Cost Per Acquisition (CPA)**: What does each player cost?
- **Player Lifetime Value (LTV)**: What is each player worth?

#### 2. Churn Analysis
- **Churn Reasons**: Why do players leave?
- **Churn Timing**: When do players churn?
- **Competitor Migration**: Where do churned players go?
- **Win-Back Strategies**: How can you win back players?

### Win/Loss Framework

#### 1. Win Analysis
```
Win Factors:
├── Product Superiority
│   ├── Better Features
│   ├── Better Performance
│   └── Better UX/UI
├── Market Positioning
│   ├── Better Pricing
│   ├── Better Targeting
│   └── Better Messaging
└── Operational Excellence
    ├── Better Marketing
    ├── Better Support
    └── Better Community
```

#### 2. Loss Analysis
```
Loss Factors:
├── Product Deficiencies
│   ├── Missing Features
│   ├── Performance Issues
│   └── UX/UI Problems
├── Market Misalignment
│   ├── Wrong Pricing
│   ├── Wrong Targeting
│   └── Poor Messaging
└── Operational Issues
    ├── Weak Marketing
    ├── Poor Support
    └── Toxic Community
```

#### 3. Competitive Response Analysis
- **Feature Gap Analysis**: What features are you missing?
- **Pacing Analysis**: How does your content release pace compare?
- **Quality Analysis**: How does your game quality compare?
- **Innovation Analysis**: How innovative is your game compared to competitors?

---

## 5. Market Trend Identification (市场趋势识别)

Identify and analyze market trends that could impact your competitive position.

### Trend Categories

#### 1. Genre Trends
- **Rising Genres**: Genres gaining popularity
- **Declining Genres**: Genres losing market share
- **Genre Evolution**: How genres are changing over time
- **Cross-Genre Innovation**: New genre combinations

#### 2. Platform Trends
- **Platform Shifts**: Movement between platforms
- **Technology Adoption**: New technology adoption rates
- **Platform Evolution**: How platforms are evolving
- **Cross-Platform Trends**: Multi-platform game trends

#### 3. Monetization Trends
- **Revenue Models**: Shift in monetization strategies
- **Player Spending**: Changes in player spending patterns
- **Ad Integration**: Mobile advertising trends
- **Subscription Models**: Subscription service trends

#### 4. Player Behavior Trends
- **Engagement Patterns**: How player engagement is changing
- **Session Length**: Changes in player session duration
- **Social Features**: Social gaming trend evolution
- **Content Consumption**: How players consume content

### Trend Analysis Framework

#### 1. Trend Identification
- **Data Sources**: Where do you get trend data?
- **Time Horizons**: Short-term vs long-term trends
- **Geographic Scope**: Global vs regional trends
- **Platform Scope**: Cross-platform vs platform-specific

#### 2. Trend Validation
- **Multiple Sources**: Cross-reference trend data
- **Expert Opinions**: Industry expert perspectives
- **Player Feedback**: Direct player input
- **Market Data**: Quantitative market analysis

#### 3. Trend Impact Assessment
- **Direct Impact**: How trends directly affect your game
- **Indirect Impact**: How trends indirectly affect your game
- **Opportunity Analysis**: What opportunities do trends create?
- **Risk Assessment**: What risks do trends present?

---

## 6. /competitive-brief Command Workflow

Generate comprehensive competitive intelligence briefs using structured web research.

### Command Structure
```
/competitive-brief [competitor_name] [analysis_type] [time_period]
```

### Analysis Types
- **landscape**: Competitive landscape overview
- **features**: Detailed feature comparison
- **positioning**: Market positioning analysis
- **trends**: Market trend analysis
- **financial**: Financial performance analysis

### Workflow Steps

#### 1. Research Planning
- Define research objectives
- Identify key research questions
- Determine data sources
- Set time boundaries

#### 2. Data Collection
- Web search for competitor information
- App store analysis and reviews
- Social media sentiment analysis
- Industry reports and news

#### 3. Analysis Synthesis
- Organize collected data
- Identify key insights
- Draw conclusions
- Formulate recommendations

#### 4. Brief Generation
- Executive summary
- Detailed analysis
- Recommendations
- Action items

---

## 7. Web Research Guide (情报收集)

Systematic approach to gathering competitive intelligence through web research.

### Research Sources

#### 1. Primary Sources
- **Company Websites**: Official information and announcements
- **App Stores**: Download numbers, reviews, rankings
- **Social Media**: Official accounts and community sentiment
- **Press Releases**: Company announcements and milestones

#### 2. Secondary Sources
- **Industry Reports**: Market research and analysis
- **News Articles**: Media coverage and industry analysis
- **Review Sites**: Player reviews and ratings
- **Forums/Communities**: Player discussions and feedback

#### 3. Tertiary Sources
- **Financial Reports**: Public company financial data
- **Job Postings**: Company growth and strategy indicators
- **Patent Filings**: Technology development and innovation
- **Conference Presentations**: Industry insights and trends

### Research Methodology

#### 1. Search Strategy
- **Keyword Planning**: Systematic keyword approach
- **Boolean Operators**: Advanced search techniques
- **Source Evaluation**: Assess source credibility
- **Information Validation**: Cross-reference information

#### 2. Data Collection
- **Structured Collection**: Organized data gathering
- **Quality Control**: Data validation and verification
- **Documentation**: Source tracking and citation
- **Update Schedule**: Regular data refresh

#### 3. Analysis Framework
- **SWOT Analysis**: Strengths, Weaknesses, Opportunities, Threats
- **PEST Analysis**: Political, Economic, Social, Technological factors
- **Competitive Matrix**: Structured comparison framework
- **Trend Analysis**: Pattern identification and extrapolation

---

## 8. Templates & Quick Reference

### Competitive Analysis Template

#### Executive Summary
- **Market Overview**: Key market insights
- **Competitive Position**: Your current position
- **Key Findings**: Most important discoveries
- **Recommendations**: Actionable recommendations

#### Competitor Profiles
- **Company Overview**: Basic company information
- **Game Analysis**: Detailed game analysis
- **Market Position**: Current market standing
- **Strategic Moves**: Recent strategic actions

#### Feature Comparison
- **Core Features**: Essential game features
- **Unique Features**: Differentiating features
- **Missing Features**: Opportunities for improvement
- **Quality Assessment**: Feature quality comparison

#### Market Analysis
- **Market Size**: Total addressable market
- **Growth Rate**: Market growth projections
- **Trend Analysis**: Key market trends
- **Opportunity Assessment**: Market opportunities

### Quick Reference Checklist

#### Landscape Mapping
- [ ] Identify direct competitors
- [ ] Identify indirect competitors
- [ ] Identify adjacent competitors
- [ ] Identify substitute competitors
- [ ] Create visual landscape map

#### Feature Analysis
- [ ] List all competitor features
- [ ] Create feature comparison matrix
- [ ] Identify missing features
- [ ] Assess feature quality
- [ ] Score feature opportunities

#### Positioning Analysis
- [ ] Map competitor positioning
- [ ] Analyze messaging strategies
- [ ] Identify positioning gaps
- [ ] Assess positioning effectiveness

#### Win/Loss Analysis
- [ ] Collect acquisition data
- [ ] Analyze churn reasons
- [ ] Identify win factors
- [ ] Identify loss factors
- [ ] Develop win-back strategies

---

## 9. LiveOps Comparison Framework (运营对比)

Analyze competitor LiveOps strategies and identify best practices.

### LiveOps Categories

#### 1. Event Systems
- **Daily Events**: Regular daily activities
- **Weekly Events**: Themed weekly content
- **Seasonal Events**: Holiday and seasonal celebrations
- **Limited Events**: Special time-limited content

#### 2. Content Updates
- **Update Frequency**: How often new content is released
- **Content Types**: Types of content updates
- **Update Quality**: Quality of new content
- **Player Engagement**: How updates engage players

#### 3. Community Management
- **Communication**: How they communicate with players
- **Feedback Integration**: How they incorporate player feedback
- **Community Events**: Community-focused activities
- **Support Quality**: Player support quality

### LiveOps Analysis Framework

#### 1. Event Analysis
```
Event Effectiveness Metrics:
├── Participation Rate
├── Engagement Duration
├── Revenue Impact
├── Retention Impact
└── Social Sharing
```

#### 2. Content Update Analysis
```
Content Quality Metrics:
├── Bug Frequency
├── Player Satisfaction
├── Feature Completeness
├── Performance Impact
└── Innovation Level
```

#### 3. Community Health Analysis
```
Community Metrics:
├── Active User Rate
├── Sentiment Score
├── Support Response Time
├── Feedback Implementation
└── Social Engagement
```

---

## 10. Ad Creative Teardown Template (素材拆解)

Systematic analysis of competitor advertising creative strategies.

### Creative Analysis Framework

#### 1. Visual Elements
- **Art Style**: Consistency and appeal
- **Character Design**: Character appeal and relevance
- **Environment Design**: Background and setting quality
- **Animation Quality**: Motion and fluidity

#### 2. Messaging Strategy
- **Value Proposition**: Core message clarity
- **Call-to-Action**: Effectiveness of CTAs
- **Emotional Appeal**: Emotional connection with audience
- **Brand Consistency**: Alignment with brand identity

#### 3. Performance Metrics
- **Click-Through Rate**: Ad effectiveness
- **Conversion Rate**: Ad to install conversion
- **Cost Per Install**: Acquisition efficiency
- **Return on Ad Spend**: Revenue efficiency

### Creative Analysis Template

#### Ad Creative Breakdown
```
Creative Elements:
├── Visual Analysis
│   ├── Art Style Assessment
│   ├── Character Appeal
│   ├── Environment Quality
│   └── Animation Review
├── Message Analysis
│   ├── Value Proposition
│   ├── Call-to-Action
│   ├── Emotional Appeal
│   └── Brand Consistency
└── Performance Analysis
    ├── CTR Analysis
    ├── Conversion Analysis
    ├── CPA Analysis
    └── ROAS Analysis
```

---

## 11. Retention vs Monetization Trade-off (留存-变现权衡)

Analyze how competitors balance player retention with monetization strategies.

### Balance Framework

#### 1. Retention Strategies
- **Core Loop**: Engaging core gameplay
- **Progression Systems**: Meaningful advancement
- **Social Features**: Community engagement
- **Content Updates**: Fresh content delivery

#### 2. Monetization Strategies
- **Direct Purchases**: One-time transactions
- **Subscription Models**: Recurring revenue
- **Advertising**: Ad-based revenue
- **Gacha Systems**: Randomized rewards

#### 3. Balance Analysis
```
Retention vs Monetization Matrix:
High Retention/High Monetization: Ideal state
High Retention/Low Monetization: Monetization opportunity
Low Retention/High Monetization: Unsustainable
Low Retention/Low Monetization: Major issues
```

### Balance Metrics

#### 1. Retention Metrics
- **Day 1 Retention**: Initial engagement
- **Day 7 Retention**: Early retention
- **Day 30 Retention**: Long-term retention
- **Churn Rate**: Player loss rate

#### 2. Monetization Metrics
- **ARPU**: Average revenue per user
- **ARPPU**: Average revenue per paying user
- **Conversion Rate**: Free-to-paid conversion
- **LTV**: Lifetime value

#### 3. Balance Indicators
- **Paywall Density**: Frequency of monetization prompts
- **Value Perception**: Player perception of value
- **Satisfaction Score**: Overall player satisfaction
- **Revenue Stability**: Revenue consistency

---

## 12. Data Source Guide (数据源指南)

Comprehensive guide to competitive intelligence data sources.

### Primary Data Sources

#### 1. Market Intelligence Platforms
- **Sensor Tower**: Mobile app market data
- **App Annie**: App performance and analytics
- **Newzoo**: Global games market data
- **Statista**: Industry statistics and reports

#### 2. Financial Data Sources
- **SEC Filings**: Public company financial data
- **Annual Reports**: Company performance reports
- **Investor Presentations**: Strategic insights
- **Earnings Calls**: Executive commentary

#### 3. Industry Reports
- **Newzoo Global Games Market Report**: Market overview
- **Statista Gaming Reports**: Industry statistics
- **IDC Gaming Reports**: Technology trends
- **Gartner Reports**: Technology analysis

### Secondary Data Sources

#### 1. App Store Data
- **Google Play Store**: Android app data
- **Apple App Store**: iOS app data
- **Steam**: PC gaming data
- **Console Stores**: Console gaming data

#### 2. Social Media Analytics
- **Twitter Metrics**: Social engagement data
- **Facebook Insights**: Community data
- **Reddit Analysis**: Community discussions
- **Discord Analytics**: Community engagement

#### 3. Web Analytics
- **SimilarWeb**: Website traffic data
- **Alexa Rankings**: Website popularity
- **Google Trends**: Search interest data
- **Social Mention**: Brand mentions

### Data Quality Assessment

#### 1. Source Credibility
- **Authority**: Source reputation and expertise
- **Accuracy**: Historical accuracy of data
- **Timeliness**: Data recency and relevance
- **Objectivity**: Source bias and perspective

#### 2. Data Validation
- **Cross-Reference**: Multiple source confirmation
- **Expert Review**: Industry expert validation
- **Historical Comparison**: Trend consistency
- **Logical Consistency**: Data reasonableness

---

## 13. China Market Analysis (中国市场分析)

Specialized analysis framework for the Chinese gaming market.

### Market Characteristics

#### 1. Platform Distribution
- **Mobile**: Dominant platform with 70%+ market share
- **PC**: Strong presence in esports and MMO
- **Console**: Growing but regulated market
- **Web**: Declining but still relevant

#### 2. Player Behavior
- **Session Length**: Longer sessions than global average
- **Spending Patterns**: Higher average spending
- **Social Features**: Strong community engagement
- **Content Preferences**: Cultural content preferences

#### 3. Regulatory Environment
- **Approval Process**: Game approval requirements
- **Content Restrictions**: Content limitations
- **Monetization Rules**: Monetization regulations
- **Data Privacy**: Data protection requirements

### China-Specific Analysis

#### 1. Local Competitors
- **Tencent**: Market leader with diverse portfolio
- **NetEase**: Strong in PC and mobile gaming
- **miHoYo**: Rising star with global hits
- **Perfect World**: Established player with strong IP

#### 2. Market Trends
- **Esports Integration**: Growing esports market
- **Cross-Platform Play**: Increasing cross-platform support
- **Cultural Content**: Emphasis on cultural elements
- **Technology Innovation**: Advanced technology adoption

#### 3. Entry Strategies
- **Partnership**: Local partnership requirements
- **Localization**: Cultural adaptation needs
- **Regulatory Compliance**: Approval process navigation
- **Marketing**: Local marketing strategies

---

## 14. Competitor Response Modeling (竞争应对建模)

Model how competitors might respond to your strategic moves.

### Response Categories

#### 1. Direct Responses
- **Feature Matching**: Copying your features
- **Price Competition**: Undercutting your pricing
- **Marketing Counter**: Competing marketing campaigns
- **Legal Action**: IP or legal challenges

#### 2. Indirect Responses
- **Market Positioning**: Adjusting their positioning
- **Product Diversification**: Expanding their portfolio
- **Partnership Formation**: Strategic partnerships
- **Technology Investment**: R&D investments

#### 3. No Response
- **Strategic Ignoring**: Choosing not to respond
- **Resource Constraints**: Unable to respond effectively
- **Market Focus**: Focusing on different segments
- **Timing Delays**: Delayed response planning

### Response Modeling Framework

#### 1. Scenario Planning
```
Competitor Response Scenarios:
├── Aggressive Response
│   ├── Rapid Feature Matching
│   ├── Price War
│   └── Marketing Blitz
├── Strategic Response
│   ├── Selective Feature Adoption
│   ├── Positioning Adjustment
│   └── Partnership Formation
├── Limited Response
│   ├── Minor Feature Updates
│   ├── Marketing Adjustments
│   └── Community Engagement
└── No Response
    ├── Status Quo Maintenance
    ├── Focus on Other Areas
    └── Resource Constraints
```

#### 2. Response Probability
- **Market Share Impact**: How your move affects their market share
- **Resource Availability**: Their ability to respond
- **Strategic Priority**: How important this is to them
- **Historical Patterns**: Past response behaviors

#### 3. Response Preparation
- **Counter-Strategies**: Plans for competitor responses
- **Contingency Planning**: Alternative strategies
- **Resource Allocation**: Resource allocation flexibility
- **Timing Strategies**: Strategic timing considerations

---

## Usage Instructions

### Basic Usage
```
@competitive-analysis
```
Displays available analysis frameworks and templates.

### Specific Analysis
```
@competitive-analysis landscape
@competitive-analysis features
@competitive-analysis positioning
@competitive-analysis trends
```

### Competitor-Specific Analysis
```
@competitive-analysis competitor_name analysis_type
```

### Command-Based Briefing
```
/competitive-brief [competitor] [analysis_type] [time_period]
```

---

*Competitive Analysis Framework*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
