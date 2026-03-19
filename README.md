# TOEFL 2026 Speaking Practice — AI-Powered, Free, Unlimited

**Practice the TOEFL speaking section with real speech analysis — not just transcription.**

Most AI tools (ChatGPT, Gemini, Claude) can transcribe your speech and maybe check pronunciation. This tool goes deeper: it analyzes your **pace, rhythm, intonation, and phoneme-level pronunciation** using open-source AI models — all running for free on Google Colab.


---

## Why This Exists

I was preparing for the TOEFL 2026 and couldn't find a single free tool that actually evaluates *how* you speak — not just *what* you say. So I built one.

---

## What It Does

### Listen & Repeat
Listen to a sentence, repeat it back, and get scored on a 0–5 TOEFL scale. The AI evaluates:
- **Word accuracy** — Did you say the right words?
- **Pronunciation** — Phoneme-level analysis flags exactly which sounds you mispronounced (e.g., "/θ/ was pronounced as /d/")
- **Pace** — Words per minute, speech-to-silence ratio
- **Rhythm** — Pause patterns, hesitation detection
- **Intonation** — Pitch range, variation, and natural speech melody

**50 built-in practice sets** covering real-world scenarios (hospitals, banks, hotels, airports, etc.) plus a **custom generator** — type any topic and get a new set instantly.

### Take an Interview
Answer open-ended TOEFL-style interview questions and receive detailed feedback on:
- Content relevance and elaboration
- Fluency and flow
- Pronunciation with specific phoneme feedback
- Grammar and vocabulary range
- Intonation and expressiveness

**50 built-in interview topics** with 4 progressively harder questions each, plus a **custom topic generator**.

### Progress Tracking
Your scores are automatically saved to Google Drive as a JSON file. Come back anytime and pick up where you left off — your progress persists across Colab sessions.

---

## AI Models Under the Hood

| Model | Purpose |
|-------|---------|
| **Whisper Medium** (faster-whisper) | Speech-to-text transcription with word-level timestamps and confidence scores |
| **Wav2Vec2 Large** (facebook/wav2vec2-large-960h) | Phoneme-level pronunciation analysis — compares what you said vs. what you should have said at the individual sound level |
| **Qwen2.5-3B-Instruct** (4-bit quantized) | AI evaluator that scores your response using official TOEFL speaking rubrics and all the audio analysis data |
| **g2p-en** | Grapheme-to-phoneme conversion for expected text → IPA phoneme mapping |

All models run locally on the Colab GPU. Nothing is sent to external APIs. **Total VRAM usage fits within a free T4 (16 GB).**

---

## How to Use

1. Open the Colab notebook (link above)
2. Set runtime to **GPU** → Runtime > Change runtime type > T4 GPU
3. Run all cells (Runtime > Run all)
4. Allow Google Drive access when prompted
5. Upload the `English_Speaking_Practice.zip` file when prompted
6. Click the public URL that appears to open the app
7. Allow microphone access and start practicing

> **First run** takes 5–10 minutes to download the AI models. After that, it's much faster.

> **Note:** Google Colab's free tier doesn't guarantee GPU access at all times, and sessions can disconnect due to inactivity. If that happens, just reconnect and rerun — your progress is saved to Google Drive.

---

## Project Structure

```
├── English_Speaking_Practice.ipynb   # Colab notebook (entry point)
├── English_Speaking_Practice.zip     # Upload this to Colab
│   ├── server.py                     # Flask backend — API routes, model orchestration, TOEFL rubrics
│   ├── phoneme_analyzer.py           # Wav2Vec2 pronunciation analysis engine
│   ├── questions.py                  # 100 practice sets (50 Listen & Repeat + 50 Interview)
│   ├── templates/index.html          # Frontend UI
│   ├── static/style.css              # Styling
│   ├── requirements.txt              # Python dependencies
│   └── progress.json                 # Local progress file (Google Drive version is primary)
```

---

## Requirements

- A Google account (for Colab and Drive)
- A browser with microphone access (Chrome recommended)
- That's it. No local setup, no API keys, no payment.

---

## How It Works (Technical)

1. You speak into your microphone → audio is recorded as WebM
2. **Whisper** transcribes your speech with word-level timestamps and confidence
3. **Wav2Vec2** analyzes your audio at the phoneme level — it compares what you actually said against the expected phonemes (converted via g2p-en) using edit-distance alignment
4. Audio metrics are extracted: pitch (Hz range, std dev, direction changes), rhythm (pause count, duration, speech ratio), energy (volume consistency)
5. All data is fed to **Qwen2.5-3B** with the official TOEFL speaking rubric as context
6. The LLM returns a structured evaluation with a score (0–5) and specific feedback on every dimension

---

## Roadmap

- [ ] Reading section practice
- [ ] Listening section practice
- [ ] Writing section practice
- [ ] Score history visualization and trends

---

## Feedback

Found a bug? Have a suggestion? Open an issue or reach out — feedback is welcome.

If you found this helpful and want to support the project:
**[Support on Gumroad](https://testexpert.gumroad.com/l/hlilv)**

---

## License

This project is free for personal and educational use.
