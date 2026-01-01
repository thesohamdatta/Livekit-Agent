# LiveKit-Agent (AURAOS)
<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/9d76f086-be9d-4eca-9d4b-15eb22d47a4b" />


A small voice assistant example built with LiveKit Agents and LiveKit plugins (OpenAI, Silero). This project runs a voice-enabled assistant that connects to a LiveKit room, uses a speech-to-text (STT) engine, an LLM for responses, and a text-to-speech (TTS) engine for spoken replies.

## What this repo contains

- `main.py` — Entrypoint that starts the voice assistant worker.
- `api.py` — Example function context (temperature control) used by the assistant.
- `ai/` — Python virtual environment (included in this workspace).

## Prerequisites

- Windows (PowerShell recommended) — instructions below are PowerShell-focused.
- Python 3.11+ (the project already has a venv at `ai/`).
- Microphone and speakers for voice I/O.
- Required Python packages are installed in the `ai` virtual environment. If not, see "Install dependencies" below.
- A `.env` file with LiveKit and OpenAI credentials (see example below).

## Quick start (PowerShell)

Open PowerShell, change to the project directory and activate the virtual environment:

```powershell
cd C:\Users\Soham\Desktop\PROJECTS\AURA\AURAOS
.\ai\Scripts\Activate.ps1
```

If activation succeeds you should see `(ai)` in your prompt. Then run the app:

```powershell
python main.py
```

Alternatively, you can run the script directly with the virtualenv Python without activating:

```powershell
C:/Users/Soham/Desktop/PROJECTS/AURA/AURAOS/ai/Scripts/python.exe main.py
```

## Install dependencies (if needed)

If packages are missing or you created a fresh environment, install them using pip (while the venv is activated):

```powershell
pip install -r requirements.txt
```

Note: This repository already includes an `ai/` venv with many packages. Use the `get_python_environment_details` output or `pip list` to inspect installed packages.

## Environment variables (.env)

Create a `.env` file in the project root with the necessary credentials. Example (replace placeholders):

```
# LiveKit server (url) and API credentials
LIVEKIT_URL=https://your-livekit-server.example
LIVEKIT_API_KEY=lk_api_key_here
LIVEKIT_API_SECRET=lk_api_secret_here

# OpenAI API key (used by livekit-plugins-openai)
OPENAI_API_KEY=sk-...

# Optional: other provider-specific variables (follow plugin docs)
```

Do NOT commit secrets to source control. Use a `.env` or secure secret manager.

## Notes & troubleshooting

- Activation fails with an Exit Code 127 (or similar): make sure PowerShell's execution policy allows running scripts. You may need to run PowerShell as Administrator and run:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

- If `Activate.ps1` isn't present but you have `ai` venv, check `ai\Scripts\activate.bat` (for cmd) or recreate the venv.

- If `python main.py` produces no output: the assistant connects to LiveKit and waits for voice input — ensure the `.env` contains correct LiveKit and OpenAI values, and that your microphone is working.

- For permission issues with microphone/speakers, ensure Windows privacy settings allow apps to access microphone.

