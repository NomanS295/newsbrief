# NewsBrief — NSAPP Daily Briefing

A standalone AI-powered daily news emailer that runs 24/7 on a Raspberry Pi.
Every morning at 8am, it scrapes Canadian news sources, summarizes them with a
local AI model, and emails you a clean daily briefing.

## What it looks like
A formatted HTML email with sections:
- CANADA — top Canadian stories of the day
- WORLD — major global events
- BIG PICTURE — AI analysis of the day's most important trend

## Tech Stack
- Python + Raspberry Pi 5 (runs 24/7, no cloud needed)
- Ollama + Llama 3.2 3B (local AI, no API costs)
- RSS feeds from CBC, Globe and Mail, National Post
- Gmail SMTP for delivery
- Docker (deployment, coming soon)

## News Sources
- CBC News Top Stories
- CBC Canada
- CBC World
- The Globe and Mail
- National Post

## Setup
1. Clone the repo
2. Install Ollama and pull the model:
   ollama pull llama3.2:3b
3. Copy config.example.py to config.py and fill in your details
4. Create a virtual environment:
   python3 -m venv venv
   source venv/bin/activate
5. Install dependencies:
   pip install requests schedule
6. Run:
   python3 src/news.py

## Requirements
- Raspberry Pi 4/5 with at least 4GB RAM
- Python 3.10+
- Ollama installed
- Gmail account with App Password enabled

## Known Issues / Work In Progress

### Model Quality
Llama 3.2 3B is the largest model that fits comfortably in 4GB RAM.
It does a decent job summarizing but lacks the depth of larger models.
Upgrading to an 8GB Pi 5 would allow running 7B models for better quality.

### Output Formatting
The model sometimes uses markdown asterisks instead of clean HTML despite
being instructed not to. This is a known limitation of smaller models
following complex formatting instructions reliably.

### More Sources Needed
Reuters and AP News RSS feeds failed to resolve — still investigating
alternative URLs or scraping methods to add international coverage.

### Docker Deployment
Container setup for auto-start on boot is planned but not yet implemented.
Currently requires manual start via SSH.

## Roadmap
- [ ] Docker container for auto-start on boot
- [ ] Add Reuters and AP News sources
- [ ] Add market/stocks section
- [ ] Add Toronto weather summary
- [ ] Better HTML email template
- [ ] Upgrade model quality with larger Pi RAM
