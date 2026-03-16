# Audio Tools

Local speech-to-text and text-to-speech utilities using OpenAI Whisper and pyttsx3. No API keys required — everything runs offline on your machine.

## What It Does

- **transcribe.py** — Converts WAV audio recordings into text files. Supports English (auto-detected) and Chinese. Useful for transcribing meetings, voice memos, or interviews.
- **speak.py** — Converts text into spoken English audio. Can play it live or save to a WAV file.

## Quick Start

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Transcribe a recording to text
python3 transcribe.py /path/to/recording.wav --output-dir ./output

# 3. Convert the transcript to speech
python3 speak.py --file ./output/recording.txt --output ./output/spoken.wav
```

## Setup

```bash
pip install -r requirements.txt
```

## Speech to Text

Transcribe WAV audio files using local Whisper.

```bash
# Single file (English auto-detected)
python3 transcribe.py recording.wav

# Chinese audio
python3 transcribe.py recording.wav --lang zh

# All WAV files in a directory
python3 transcribe.py /path/to/recordings/ --output-dir ./output

# Higher accuracy (downloads ~1.5GB model)
python3 transcribe.py recording.wav --model medium
```

### Options

| Flag | Description | Default |
|------|-------------|---------|
| `--lang` | `en` or `zh` | auto-detect |
| `--model` | `tiny`, `base`, `small`, `medium`, `large` | `base` |
| `--output-dir` | Output directory for .txt files | same as input |

## Text to Speech

Convert text to spoken English audio.

```bash
# Play text aloud
python3 speak.py --text "Hello world"

# Read from file
python3 speak.py --file transcript.txt

# Save to WAV
python3 speak.py --text "Hello" --output output.wav

# Adjust speed and volume
python3 speak.py --file transcript.txt --rate 120 --volume 1.0
```

### Options

| Flag | Description | Default |
|------|-------------|---------|
| `--text` | Direct text input | - |
| `--file` | Text file to read | - |
| `--output` | Save to WAV file | plays live |
| `--rate` | Words per minute | 160 |
| `--volume` | 0.0 - 1.0 | 0.9 |

## Claude Code Skills

This project includes two Claude Code skills for hands-free usage:

- **`/speech-to-text`** — Tell Claude to transcribe audio, e.g. "audio to text for /path/to/recording.wav"
- **`/text-to-speech`** — Tell Claude to speak text, e.g. "convert transcript.txt to speech"

Skill definitions are in the [`skills/`](skills/) directory. To install them locally:

```bash
cp skills/speech-to-text.md ~/.claude/skills/speech-to-text/SKILL.md
cp skills/text-to-speech.md ~/.claude/skills/text-to-speech/SKILL.md
```

## Dependencies

- [openai-whisper](https://github.com/openai/whisper) - local speech recognition
- [pyttsx3](https://github.com/nateshmbhat/pyttsx3) - offline text-to-speech
- [torch](https://pytorch.org/) - ML runtime for Whisper
