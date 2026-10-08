# Voice AI

A real-time voice assistant powered by Groq AI. Speak into your microphone and get instant spoken responses using a large language model and text-to-speech.

## Features

- **Live Speech Recognition** — Captures microphone input using Google Speech Recognition
- **LLM Responses** — Sends your speech to Groq's `llama-3.3-70b-versatile` model for intelligent replies
- **Text-to-Speech** — Converts AI replies to audio using Groq's `playai-tts` voice model
- **Conversation Memory** — Maintains full message history for context-aware chat
- **REST API** — FastAPI backend with a `/process` endpoint and audio file serving
- **Docker Ready** — Includes a `Dockerfile` for containerized deployment
- **Vercel Config** — `vercel.json` included for quick cloud deployment

## Tech Stack

| Layer | Technology |
|---|---|
| Backend Framework | FastAPI |
| Speech Recognition | SpeechRecognition (Google) |
| LLM | Groq API — `llama-3.3-70b-versatile` |
| Text-to-Speech | Groq Audio — `playai-tts` |
| Server | Uvicorn + Gunicorn |
| Containerization | Docker |
| Deployment | Vercel |

## Setup & Installation

### Prerequisites

- Python 3.10+
- A [Groq API key](https://console.groq.com/)
- A working microphone

### 1. Clone the Repository

```bash
git clone https://github.com/mohsin-khann/Voice-Ai.git
cd Voice-Ai
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

### 4. Run the Server

```bash
uvicorn tests:app --host 0.0.0.0 --port 8001 --reload
```

### 5. Trigger Voice Input

Send a POST request to start listening:

```bash
curl -X POST http://localhost:8001/process
```

The API will listen through your microphone, process the speech, and return:

```json
{
  "user_text": "What is the capital of France?",
  "response_text": "The capital of France is Paris.",
  "audio_url": "/audio/response0.wav"
}
```

## Docker

```bash
docker build -t voice-ai .
docker run -p 8001:8001 --env-file .env voice-ai
```

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/process` | Listen via mic, get AI response + audio |
| `GET` | `/audio/{filename}` | Serve a generated audio file |

## Environment Variables

| Variable | Description |
|---|---|
| `GROQ_API_KEY` | Your Groq API key |

## License

MIT
