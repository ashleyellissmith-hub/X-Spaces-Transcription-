# X Space Transcriber Website

A deployable MVP website for turning X Space recordings into transcripts, summaries, quotes, key points and post ideas.

It supports two workflows:

1. Paste an X Space / X audio link and attempt extraction with `yt-dlp`.
2. Upload an audio file directly if extraction fails.

X link extraction is best-effort because X changes access rules and some recordings are restricted, expired, private or too long for easy extraction.

## Features

- Web interface
- Link extraction with `yt-dlp`
- Upload fallback
- Audio conversion with `ffmpeg`
- OpenAI transcription
- Summary, key points, quotes and social post ideas
- Downloadable transcript `.txt`
- Simple `/health` endpoint for hosting platforms

## Requirements

- Python 3.11+
- `ffmpeg`
- OpenAI API key

## Local setup

```bash
cd x_space_transcriber_website
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
```

Add your OpenAI API key to `.env`.

Run:

```bash
uvicorn backend.main:app --reload --host 0.0.0.0 --port 8000
```

Open:

```text
http://localhost:8000
```

## Deploying

Use a host that supports long-running Python processes and system packages, such as Railway, Render, Fly.io, or a small VPS.

Vercel/Netlify are not ideal for this because `yt-dlp`, `ffmpeg`, long recordings and transcription jobs need a server-like environment.

### Railway / Render style deploy

Use the included `Dockerfile`.

Set environment variable:

```text
OPENAI_API_KEY=your_key_here
```

The app exposes port `8000` by default.

## Important notes

- Respect copyright, privacy, consent and platform terms.
- Only transcribe recordings you have permission to use.
- For large Spaces, transcription can take time and may need higher server limits.
- Speaker labelling is not included in this MVP. It can be added later using diarisation tools such as Pyannote, AssemblyAI, Deepgram or similar services.

## Suggested next upgrades

- Job queue for long recordings
- User accounts
- Speaker diarisation
- Stripe payments
- Supabase/S3 storage
- DOCX/PDF export
- Clip generation with timestamps
