# SupoClip

AI-powered video clipping tool that converts long-form content into TikTok / YouTube Shorts automatically. Free, open source, no watermarks.

> Hosted version: [supoclip.com](https://www.supoclip.com)

---

## What it does

- Converts landscape videos to 9:16 vertical (face-centered crop)
- AI selects the most engaging segments
- Word-synced captions with multiple styles
- No paid transcription API needed — runs fully local via Whisper

---

## Requirements

- Docker and Docker Compose
- A Google Gemini API key (free tier works) — or OpenAI / Anthropic / Ollama

---

## Installation

**1. Clone the repo**

```bash
git clone https://github.com/mattwyd/mattclip.git
cd mattclip
```

**2. Create a `.env` file** in the root directory:

```env
# AI provider for clip analysis — pick one:
GOOGLE_API_KEY=your_google_api_key
LLM=google-gla:gemini-3-flash-preview

# Or OpenAI:
# OPENAI_API_KEY=your_openai_api_key
# LLM=openai:gpt-4o

# Or Anthropic:
# ANTHROPIC_API_KEY=your_anthropic_api_key
# LLM=anthropic:claude-3-5-sonnet

# Or local Ollama:
# LLM=ollama:llama3.2
# OLLAMA_BASE_URL=http://localhost:11434/v1

# Whisper model for transcription (tiny/base/small/medium/large)
# Larger = more accurate but slower. "base" is a good default.
WHISPER_MODEL=base

# Auth secret (change this in production)
BETTER_AUTH_SECRET=change_this_in_production

# Database
POSTGRES_DB=supoclip
POSTGRES_USER=supoclip
POSTGRES_PASSWORD=supoclip_password
```

**3. Start everything**

```bash
docker-compose up -d
```

First run downloads Whisper model weights and builds containers (~5 min).

**4. Open the app**

Go to [http://localhost:3000](http://localhost:3000), create an account, and upload or paste a YouTube URL.

---

## Usage

1. Paste a YouTube URL or upload a video file
2. Choose processing mode (Fast / Balanced / Quality)
3. Hit **Generate** — clips appear as they're processed
4. Download or edit individual clips

---

## Troubleshooting

**Videos stuck in queue / not processing**
```bash
docker-compose logs -f worker
```

**Rebuild after changing `.env`**
```bash
docker-compose up -d --build
```

**Performance tuning**
```env
DEFAULT_PROCESSING_MODE=fast   # fast | balanced | quality
FAST_MODE_MAX_CLIPS=4          # max clips in fast mode
WHISPER_MODEL=small            # upgrade for better captions
```

---

## Local Development (without Docker)

See [CLAUDE.md](CLAUDE.md) for full local setup instructions.

---

## License

AGPL-3.0 — see [LICENSE](LICENSE).
