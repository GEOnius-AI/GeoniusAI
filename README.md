# Geonius AI 

Geonius AI is a comprehensive AI Search Optimization (GEO) platform that helps brands monitor, analyze, and optimize their visibility across AI-powered search engines like ChatGPT, Google Gemini, Perplexity, Claude, and Microsoft Copilot.

## Product Demo

Watch our product demo to see Geonius AI in action:

<div align="center">
  <a href="https://youtu.be/JGHli3sMqYw" target="_blank">
    <img src="https://img.youtube.com/vi/JGHli3sMqYw/maxresdefault.jpg" alt="Geonius AI - Product Demo" style="max-width: 100%; border-radius: 8px; cursor: pointer;">
  </a>
  <p><a href="https://youtu.be/JGHli3sMqYw" target="_blank">Watch on YouTube</a></p>
</div>

## Table of Contents

- [Project Overview](#project-overview)
- [Architecture & Components](#architecture--components)
- [Brand Visibility Score Calculation](#brand-visibility-score-calculation)
- [Search Volume Calculation](#search-volume-calculation)
- [Vista AI Assistant](#vista-ai-assistant---your-seo-expert-co-pilot)
- [Features](#features)
- [Future Integrations](#future-integrations)
- [Technology Stack](#technology-stack)
- [Setup & Installation](#setup--installation)

---

## Project Overview

Geonius AI provides businesses with actionable insights into how AI search engines discover, evaluate, and present their brand in response to user queries. The platform tracks brand mentions, citations, sentiment, and visibility across multiple AI engines, enabling data-driven optimization strategies.

### Key Capabilities

- **Multi-Engine Monitoring**: Track brand presence across ChatGPT, Gemini, Perplexity, Claude, and Copilot
- **Automated Prompt Execution**: Schedule and execute queries across AI engines
- **Competitive Intelligence**: Monitor competitor visibility and share of voice
- **Analytics Integration**: Connect Google Analytics 4, Google Search Console, and Shopify
- **AI-Powered Insights**: Get recommendations through Vista AI Assistant
- **Comprehensive Audits**: Perform complete SEO and GEO audits with 30+ tools

---

## Architecture & Components

### Backend (`/backend`)

The backend is built with **FastAPI** and provides RESTful APIs for all platform functionality.

#### Core Services

1. **AI Engine Service** 
   - Executes prompts across multiple AI engines (ChatGPT, Gemini, Perplexity)
   - Extracts URLs and citations from responses
   - Tracks execution metadata (tokens, cost, response time)

2. **Analytics Service** 
   - Extracts brand mentions from AI responses
   - Categorizes citations (owned, media, social)
   - Performs sentiment analysis
   - Processes execution analytics

3. **Prompt Generator Service** 
   - Generates prompts from keywords, topics, or competitors
   - Enforces subscription tier limits (Free, Pro, Enterprise)
   - Creates prompt generation jobs

4. **Integration Services**
   - **GA4 Service** : Google Analytics 4 integration
   - **GSC Service** : Google Search Console integration
   - **Shopify Service** : Shopify store integration

5. **DNS Verification Service** 
   - Domain ownership verification via DNS TXT records
   - Token generation and validation

6. **Scheduler Service** 
   - Manages scheduled jobs using APScheduler
   - Coordinates automated prompt execution and data sync

#### Scheduled Jobs

1. **Prompt Execution Job** 
   - Runs daily at midnight
   - Executes prompts based on subscription tiers
   - Processes analytics for each execution

2. **Integration Sync Job** 
   - Runs daily at 2 AM
   - Syncs data from GA4, GSC, and Shopify
   - Updates traffic and search performance metrics

3. **Analytics Processing Job** 
   - Runs hourly
   - Processes brand mentions and citations
   - Analyzes sentiment from recent executions

#### API Endpoints

- **Verification** : DNS verification endpoints
- **Integrations** : GA4, GSC, Shopify connection endpoints
- **Prompts** : Prompt generation and execution endpoints
- **Analytics** : Brand mentions, citations, sentiment endpoints
- **Health** : System health checks

### Frontend 

The frontend is built with **Next.js 14** and **TypeScript**, providing a modern, responsive dashboard interface.

#### Dashboard Components

1. **Overview Page** 
   - High-level visibility metrics and trends
   - Topic performance breakdown
   - Platform comparison charts
   - Recent signals and opportunities

2. **Prompt Analysis Page** 
   - Individual prompt performance metrics
   - Visibility scores and citation shares
   - Historical trends and rankings
   - Platform-specific breakdowns

3. **Prompt Insights Page** 
   - Top-performing prompts spotlight
   - Citation logs and mention tracking
   - Win rate analysis

4. **Competitor Analytics Page** 
   - Competitor visibility comparison
   - Share of voice analysis
   - Citation score tracking
   - Platform-specific competitor metrics

5. **Platform Insights Page** 
   - Per-platform visibility scores (ChatGPT, Perplexity, Gemini, etc.)
   - Platform-specific share of voice
   - Average position by platform
   - Citation score breakdown

6. **Region Insights Page** 
   - Geographic visibility mapping
   - Country-specific metrics
   - Regional share of voice trends

7. **GEO Audit Page** 
   - Site health checks
   - Structured data coverage
   - SEO audit recommendations
   - Actionable improvement opportunities

8. **SEOTools Page** 
   - SEO audit tools
   - Keyword research utilities
   - Content optimization tools
   - Visibility analysis tools

9. **Vista Page** 
   - AI-powered assistant interface
   - SEO tool integrations
   - Conversational analytics queries

10. **API Hub Page** 
    - API documentation and access
    - Query visibility scores programmatically
    - Integration endpoints

11. **Agent Analytics Page** 
    - AI crawler discovery monitoring
    - Web property evaluation tracking

12. **Answer Engine Monitor Page** 
    - Real-time answer engine monitoring
    - Response tracking and analysis

13. **Settings Page** 
    - User and organization settings
    - Integration management
    - Subscription management

### Database 

The platform uses **Supabase (PostgreSQL)** with a comprehensive schema including:

#### Core Tables

- **Users & Organizations**: Multi-tenant user management
- **Brands**: Tracked brands and domains
- **Brand Competitors**: Competitor tracking
- **Prompts**: Tracked prompts and queries
- **Prompt Executions**: Individual AI engine runs
- **Prompt Metrics**: Daily aggregated metrics (visibility scores, citation shares)

#### Analytics Tables

- **Citations**: Brand citations in AI responses
- **Brand Mentions**: Brand name mentions with sentiment
- **Competitor Metrics**: Daily competitor performance
- **Topic Metrics**: Topic-level performance tracking
- **Platform Metrics**: Per-platform daily metrics
- **Region Metrics**: Per-country daily metrics

#### Integration Tables

- **GA4 Integrations**: Google Analytics 4 connections
- **GSC Integrations**: Google Search Console connections
- **Shopify Integrations**: Shopify store connections

#### Audit & Recommendations

- **Site Health Checks**: Health check results
- **Recommendations**: GEO audit recommendations
- **Structured Data Coverage**: Schema markup tracking

#### Vista AI Assistant Tables

- **Vista Conversations**: Chat conversation history
- **Vista Messages**: Individual messages in conversations
- **Vista Tool Executions**: Tool execution results
- **Vista Reports**: Generated reports and analysis

---

## Brand Visibility Score Calculation

The **Brand Visibility Score** is a composite metric that quantifies how prominently a brand appears across AI search engines. It's calculated in the backend and stored in the `prompt_metrics`, `competitor_metrics`, `topic_metrics`, `platform_metrics`, and `region_metrics` tables.

### Calculation Methodology

The visibility score is calculated using multiple weighted factors:

1. **Position Score** (Weight: 40%)
   - Based on average position across all AI engines
   - Formula: `position_score = (1 / avg_position) * 100`
   - Higher positions (1-3) receive maximum weight
   - Positions beyond 10 receive minimal weight

2. **Citation Share** (Weight: 30%)
   - Percentage of total citations that belong to the brand
   - Formula: `citation_share = (brand_citations / total_citations) * 100`
   - Accounts for both owned and third-party citations

3. **Mention Frequency** (Weight: 20%)
   - Frequency of brand mentions across all prompt executions
   - Formula: `mention_score = (mentions_count / total_executions) * 100`
   - Normalized by total execution volume

4. **Presence Type** (Weight: 10%)
   - Bonus for direct citations vs. mentions
   - Cited: +10 points
   - Mentioned: +5 points
   - Not mentioned: 0 points

### Final Visibility Score

Visibility Score = (Position Score × 0.4) +
(Citation Share × 0.3) +
(Mention Frequency × 0.2) +
(Presence Type Bonus × 0.1)


The score is normalized to a 0-100 scale, where:
- **80-100**: Excellent visibility (top 3 positions, high citation share)
- **60-79**: Good visibility (positions 4-6, moderate citation share)
- **40-59**: Moderate visibility (positions 7-10, low citation share)
- **0-39**: Low visibility (positions 10+, minimal citations)

### Aggregation Levels

Visibility scores are calculated and aggregated at multiple levels:

- **Prompt Level**: Per individual prompt query
- **Topic Level**: Aggregated across all prompts in a topic category
- **Platform Level**: Per AI engine (ChatGPT, Perplexity, etc.)
- **Region Level**: Per country/geographic region
- **Competitor Level**: Comparative visibility against competitors

---

## Search Volume Calculation

The platform calculates **AI Search Volume** by combining traditional web search volume data with AI-specific search behavior metrics.

### Step 1: Theme Keyword Volume Calculation

1. **Keyword Collection**
   - Gather all relevant keywords for a theme/topic
   - Includes primary keywords, long-tail variations, and semantic variations

2. **Volume Aggregation**
   - Fetch search volume for each keyword from data providers (e.g., Google Keyword Planner, SEMrush, Ahrefs)
   - Sum all keyword volumes: `total_theme_volume = Σ(keyword_volume)`

3. **Overlap Deduplication**
   - Account for keyword overlap to avoid double-counting
   - Apply overlap reduction factor: `deduplicated_volume = total_theme_volume × (1 - overlap_factor)`
   - Overlap factor calculated based on keyword similarity and search intent overlap

4. **Total Theme Keyword Volume**

Theme Keyword Volume = Σ(keyword_volumes) × (1 - overlap_factor)


### Step 2: AI Search Volume Ratio Calculation

The AI Search Volume Ratio adjusts traditional web search volume to reflect actual AI search behavior. It's calculated using multiple weighted factors:

1. **Overall AI Search Traffic Ratio** (Weight: 25%)
   - Ratio of AI search traffic vs. traditional web search traffic
   - Based on industry data and platform analytics
   - Formula: `ai_traffic_ratio = ai_searches / total_searches`

2. **Thematic Bias** (Weight: 20%)
   - Certain topics are more likely to be searched in AI engines
   - Research-oriented queries have higher AI search propensity
   - Educational and comparison queries favor AI search
   - Formula: `thematic_bias = topic_ai_propensity_score`

3. **Trend Factor** (Weight: 15%)
   - Recent trends in AI search adoption
   - Growing queries have higher AI search volume
   - Formula: `trend_factor = (recent_ai_growth_rate / baseline_growth_rate)`

4. **Mobile vs. Desktop** (Weight: 15%)
   - Mobile users are more likely to use AI search (voice assistants, mobile apps)
   - Formula: `mobile_factor = (mobile_ai_ratio × mobile_traffic_share) + (desktop_ai_ratio × desktop_traffic_share)`

5. **Platform-Specific Traffic** (Weight: 15%)
   - Different AI platforms have different usage patterns
   - ChatGPT vs. Perplexity vs. Gemini have varying search volumes
   - Formula: `platform_factor = Σ(platform_usage_share × platform_ai_ratio)`

6. **Query Type Distribution** (Weight: 10%)
   - Percentage of queries in AI search that are actual search queries vs. conversational
   - Research queries: higher AI search volume
   - Transactional queries: lower AI search volume
   - Formula: `query_type_factor = (research_query_ratio × research_ai_ratio) + (transactional_query_ratio × transactional_ai_ratio)`

7. **Language Factor** (Weight: 5%)
   - Language-specific AI search adoption rates
   - English: higher AI search adoption
   - Other languages: varying adoption rates
   - Formula: `language_factor = language_specific_ai_adoption_rate`

### AI Search Volume Ratio Formula

```
AI Search Volume Ratio = (Overall AI Traffic Ratio × 0.25) +
                        (Thematic Bias × 0.20) +
                        (Trend Factor × 0.15) +
                        (Mobile vs. Desktop × 0.15) +
                        (Platform-Specific Traffic × 0.15) +
                        (Query Type Distribution × 0.10) +
                        (Language Factor × 0.05)
```

### Final AI Search Volume

```
AI Search Volume = Theme Keyword Volume × AI Search Volume Ratio
```

### Example Calculation

For a theme with:
- **Theme Keyword Volume**: 100,000 monthly searches
- **AI Traffic Ratio**: 0.15 (15% of searches are AI searches)
- **Thematic Bias**: 1.2 (research topic, 20% higher AI propensity)
- **Trend Factor**: 1.1 (10% growth in AI search)
- **Mobile Factor**: 1.15 (mobile users favor AI search)
- **Platform Factor**: 1.05 (ChatGPT-heavy usage)
- **Query Type**: 1.1 (research-heavy queries)
- **Language Factor**: 1.0 (English, baseline)

**AI Search Volume Ratio**:
```
= (0.15 × 0.25) + (1.2 × 0.20) + (1.1 × 0.15) + (1.15 × 0.15) + 
  (1.05 × 0.15) + (1.1 × 0.10) + (1.0 × 0.05)
= 0.0375 + 0.24 + 0.165 + 0.1725 + 0.1575 + 0.11 + 0.05
= 0.9325
```

**AI Search Volume**:
```
= 100,000 × 0.9325
= 93,250 monthly AI searches
```

---

## Features

### 1. Multi-Engine Monitoring

Track brand visibility across:
- **ChatGPT** (OpenAI)
- **Google Gemini** (formerly Bard)
- **Perplexity AI**
- **Claude** (Anthropic)
- **Microsoft Copilot**
- **Google AI** (various models)

### 2. Automated Prompt Execution

- Schedule prompt executions based on subscription tiers
- Free: 1 execution/day
- Pro: 4 executions/day
- Enterprise: Hourly executions
- Automatic analytics processing after each execution

### 3. Brand Mention & Citation Tracking

- **Mention Detection**: Automatically detect brand mentions in AI responses
- **Citation Extraction**: Extract and categorize URLs cited by AI engines
- **Citation Types**: Owned, media, social
- **Sentiment Analysis**: Positive, neutral, negative sentiment scoring

### 4. Visibility Score Analytics

- Real-time visibility scores across all prompts
- Historical trends and rankings
- Platform-specific visibility breakdowns
- Topic-level visibility aggregation
- Regional visibility mapping

### 5. Competitor Analytics

- Track competitor visibility scores
- Share of voice comparison
- Citation score tracking
- Platform-specific competitor metrics
- Competitive gap analysis

### 6. Topic Performance Tracking

- Organize prompts by topics/categories
- Topic-level visibility scores
- Citation share by topic
- Engine breakdown per topic
- Top pages per topic

### 7. Platform Insights

- Per-platform visibility scores
- Share of voice by platform
- Average position by platform
- Citation score breakdown
- Platform-specific trends

### 8. Regional Insights

- Geographic visibility mapping
- Country-specific metrics
- Regional share of voice
- Average position by region
- Citation scores by region

### 9. GEO Audit & Recommendations

- **Site Health Checks**: Core Web Vitals, structured data, mobile-friendliness
- **Structured Data Coverage**: Schema markup tracking
- **SEO Audit**: Comprehensive SEO analysis
- **Recommendations**: Actionable improvement opportunities
- **Priority Scoring**: High/medium/low impact recommendations

### 10. SEO Tools Suite

- **SEO Audit**: Comprehensive site health analysis
- **Keyword Research**: Discover high-value keywords
- **Content Optimization**: Optimize content for AI engines
- **Visibility Analysis**: Deep-dive visibility insights
- **Schema Generator**: Generate structured data markup

### 11. Vista AI Assistant

- Conversational interface for analytics queries
- SEO tool integrations
- Automated recommendations
- Quick wins identification
- Competitor intelligence queries

### 12. Integration Management

- **Google Analytics 4**: Traffic data integration
- **Google Search Console**: Search performance data
- **Shopify**: E-commerce data integration
- OAuth-based authentication
- Automated daily data sync

### 13. DNS Verification

- Domain ownership verification via DNS TXT records
- Token generation and validation
- Automated verification status updates

### 14. API Hub

- RESTful API access to all platform data
- Programmatic querying of visibility scores
- Integration endpoints for third-party tools
- Export capabilities (JSON, CSV, Markdown)

### 15. Prompt Generation

- AI-powered prompt generation from keywords
- Topic-based prompt generation
- Competitor-based prompt suggestions
- Subscription tier-based limits
- Automatic prompt deduplication

### 16. Analytics Dashboard

- Real-time visibility trends
- Share of voice charts
- Citation breakdowns
- Mention frequency analysis
- Sentiment distribution

---

## Future Integrations

### 1. ChatGPT Shopping Tracking

**Overview**: Track how products appear in ChatGPT's shopping-related responses and recommendations.

**Features**:
- Monitor product mentions in ChatGPT shopping queries
- Track product citation rates in shopping contexts
- Analyze product positioning in shopping recommendations
- Compare product visibility against competitors
- Track shopping query trends and seasonality

**Implementation**:
- Execute shopping-related prompts (e.g., "best [product category]", "where to buy [product]")
- Extract product citations and recommendations
- Categorize by product type, price range, and availability
- Track conversion signals (click-through rates, purchase intent)

### 2. LLM Ad Tracking

**Overview**: Monitor and analyze how brands appear in AI-generated advertising content and sponsored responses.

**Features**:
- Track ad placements in AI responses
- Monitor sponsored content mentions
- Analyze ad performance metrics (impressions, clicks, conversions)
- Compare organic vs. paid visibility
- Track ad spend efficiency across AI platforms

**Implementation**:
- Identify sponsored content markers in AI responses
- Track ad placement positions and frequency
- Integrate with advertising platforms (Google Ads, Microsoft Advertising)
- Calculate ROI for AI search advertising
- Provide recommendations for ad optimization

### 3. Additional Planned Integrations

- **Bing Chat Integration**: Monitor Microsoft Bing Chat responses
- **Siri/Apple Intelligence**: Track Apple's AI assistant responses
- **Amazon Alexa**: Monitor voice assistant product recommendations
- **Social Media AI**: Track brand mentions in AI-powered social media tools
- **E-commerce AI**: Monitor product visibility in AI shopping assistants
- **Content Management Systems**: Direct integration with CMS platforms for content optimization
- **Marketing Automation**: Integrate with HubSpot, Marketo, etc.
- **Customer Support AI**: Track brand visibility in AI-powered support tools





