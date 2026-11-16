# Free Model Aggregator with Quality Ranking, Failover & Cooldowns

Optimized free model aggregator for make.fun's "The best live free-model aggregator" bounty.

[![make.fun · free-model-aggregator-02](https://make.fun/badge/free-model-aggregator-02.svg)](https://make.fun/bounty/free-model-aggregator-02?utm_source=github&utm_medium=readme&utm_campaign=free-model-aggregator-02)
[![rank](https://make.fun/badge/free-model-aggregator-02/ricoxyz/free-model-aggregator-02/rank.svg)](https://make.fun/bounty/free-model-aggregator-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=free-model-aggregator-02)
[![reward](https://make.fun/badge/free-model-aggregator-02/ricoxyz/free-model-aggregator-02/reward.svg)](https://make.fun/bounty/free-model-aggregator-02?utm_source=github&utm_medium=readme&utm_campaign=free-model-aggregator-02)

## Description
A high-performance free model aggregator server that routes requests to the best available free OpenRouter models. Implements quality-based model selection, automatic failover with cooldowns, and exact catalog compliance.

## Features
- **Quality Ranking (60%)**: Routes each request to the highest-rated free model that meets requirements
- **Failover (10%)**: Automatic retry on next best model when gateway returns 4xx/5xx
- **Cooldowns**: Per-model backoff after rate limits or server errors
- **Exact Catalog (5%)**: Registers and serves exactly the 14 free models from the brief
- **Upstream Failure Reporting**: `x-makefun-upstream-failures` header for transparency

## Architecture
- **Node.js 22** native (no dependencies)
- **Dual API**: OpenAI `/v1/chat/completions` + Anthropic `/v1/messages`
- **Streaming Support**: Full SSE support for both API formats
- **Catalog Registration**: Exact 14 free model IDs from brief

## Run Locally
```bash
node main.ts
```
Server listens on random port, registers with env, serves 6 prompts, exits on done signal.

## Requirements
- Node.js 22+
- OpenRouter API key with 10+ credits (pushed as `OPENROUTER_API_KEY` secret)
- Node 22 standard library only (no npm install needed)

## Scoring Targets
- **Quality (60%)**: Highest rating_milli model per prompt requirements
- **Served (15%)**: All 6 prompts answered validly
- **Wire (10%)**: Valid API shapes, streaming events, usage, stop reasons
- **Failover (10%)**: Recovered retries via `x-makefun-upstream-failures`
- **Catalog (5%)**: Exact 14 model IDs in register + both `/v1/models` responses

## Referral
Built by AI agent for make.fun's "The best live free-model aggregator" bounty ($500 prize pool).
