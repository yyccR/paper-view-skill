# PaperView Skill for Claude Code

A Claude Code skill that provides AI-powered visualization APIs for research and data analysis.

## Features

- **ECharts Visualization** — Generate interactive charts (bar, line, scatter, pie, heatmap, scientific plots, etc.) from CSV/JSON/text data. AI auto-selects the best chart type.
- **AI Scientific Diagram** — Generate publication-quality figures, flowcharts, and architecture diagrams from text descriptions or arxiv papers.
- **Word Cloud** — Extract keyword frequencies from PDF documents with CJK support.

## Installation

```bash
claude /install-skill https://github.com/yyccR/paper-view-skill
```

Or manually copy the skill:

```bash
cp -r skills/paperview ~/.claude/skills/
```

## Quick Start

1. Get your API token from [www.ipaperview.com](https://www.ipaperview.com) (Profile → API Token)
2. Set your token:
   ```bash
   export PAPERVIEW_API_TOKEN=pv_live_your_token_here
   ```
3. Use the skill in Claude Code:
   ```
   /paperview
   ```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/v1/viz/generate/` | POST | Generate ECharts visualization from data |
| `/api/v1/viz/toolsets/` | GET | List available chart types |
| `/api/v1/viz/toolsets/{name}/templates/` | GET | List templates for a chart type |
| `/api/diagram/ai-generate/` | POST | Generate AI scientific diagram (SSE) |
| `/api/diagram/ai-modify/` | POST | Modify existing diagram (SSE) |
| `/api/diagram/templates/` | GET | List diagram templates |
| `/api/wordcloud/extract/` | POST | Extract word cloud data from PDF |

## API Quota

| Plan | Daily Limit | Price |
|------|-------------|-------|
| Free | 3 calls/day | $0 |
| Monthly | 30 calls/day | $4.99/mo |
| Yearly | 100 calls/day | $29.99/yr |

## Examples

### Generate a chart from CSV data

```bash
curl -X POST \
  -H "Authorization: Bearer $PAPERVIEW_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"data": "Year,Revenue\n2020,100\n2021,150\n2022,200", "context": "Show revenue growth"}' \
  https://api.ipaperview.com/api/v1/viz/generate/
```

### Generate a diagram from an arxiv paper

```bash
curl -N -X POST \
  -H "Authorization: Bearer $PAPERVIEW_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"template_type": "custom_text_only", "pdf_url": "http://arxiv.org/abs/2510.13809v1", "custom_prompt": "Create an architecture diagram"}' \
  https://api.ipaperview.com/api/diagram/ai-generate/
```

### Extract word cloud from PDF

```bash
curl -X POST \
  -H "Authorization: Bearer $PAPERVIEW_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pdf_url": "https://arxiv.org/pdf/2301.00001.pdf", "max_words": 50}' \
  https://api.ipaperview.com/api/wordcloud/extract/
```

See [SKILL.md](skills/paperview/SKILL.md) for full API documentation.

## License

MIT
