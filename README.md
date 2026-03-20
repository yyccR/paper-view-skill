# PaperView Skill

AI-powered visualization APIs for research and data analysis. Compatible with **Claude Code** and **OpenClaw**.

## Features

- **ECharts Visualization** — Generate interactive charts (98 templates across 25 chart types: bar, line, scatter, pie, heatmap, scientific plots, etc.) from CSV/JSON/text data. AI auto-selects the best chart type.
- **AI Scientific Diagram** — Generate publication-quality figures, flowcharts, and architecture diagrams from text descriptions or arxiv papers.
- **Word Cloud** — Extract keyword frequencies from PDF documents with CJK support.

## Installation

### Claude Code

```bash
claude /install-skill https://github.com/yyccR/paper-view-skill
```

Or manually:

```bash
git clone https://github.com/yyccR/paper-view-skill.git
cp -r paper-view-skill/skills/paperview ~/.claude/skills/
```

### OpenClaw

```bash
clawhub install paperview
```

Or manually:

```bash
git clone https://github.com/yyccR/paper-view-skill.git
# Machine-wide
cp -r paper-view-skill/skills/paperview ~/.openclaw/skills/
# Or workspace-specific
cp -r paper-view-skill/skills/paperview <your-workspace>/skills/
```

After installation, restart your OpenClaw session or ask the agent to "refresh skills".

## Quick Start

1. Get your API token from [www.ipaperview.com](https://www.ipaperview.com) (Profile → API Token)
2. Set your token:
   ```bash
   export PAPERVIEW_API_TOKEN=pv_live_your_token_here
   ```
3. Use the skill:
   - Claude Code: `/paperview`
   - OpenClaw: The agent auto-discovers the skill and uses it when you ask for visualizations

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/v1/viz/generate/` | POST | Generate ECharts visualization from data |
| `/api/diagram/ai-generate/` | POST | Generate AI scientific diagram (SSE) |
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

### Specify chart type (AI picks best sub-template)

```bash
curl -X POST \
  -H "Authorization: Bearer $PAPERVIEW_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"data": "Country,GDP,LifeExpectancy\nChina,17963,78\nUSA,25463,77\nJapan,4231,84", "toolset": "scatter", "context": "Show GDP vs life expectancy"}' \
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

See [SKILL.md](skills/paperview/SKILL.md) for full API documentation including response formats and rendering guides.

## License

MIT
