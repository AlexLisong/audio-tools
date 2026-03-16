---
name: text-to-speech
description: Convert text to spoken English audio using local TTS. Accepts text directly or from a file. Outputs WAV audio files.
---

# Text-to-Speech Skill

Convert text content to spoken English audio files using the local `pyttsx3` engine (offline, no API needed).

## Skill Metadata

```yaml
name: text-to-speech
version: 1.0.0
description: Convert text to spoken English audio
triggers:
  - "speak this"
  - "text to speech"
  - "convert to audio"
  - "read aloud"
  - "generate speech"
```

## Usage

The TTS script is located at: `/Users/song/bon-git/audio-tools/speak.py`

### Commands

```bash
# Speak text directly (plays audio)
python3 /Users/song/bon-git/audio-tools/speak.py --text "Your text here"

# Speak from a text file (plays audio)
python3 /Users/song/bon-git/audio-tools/speak.py --file /path/to/transcript.txt

# Save to WAV file instead of playing
python3 /Users/song/bon-git/audio-tools/speak.py --text "Your text" --output /path/to/output.wav
python3 /Users/song/bon-git/audio-tools/speak.py --file /path/to/transcript.txt --output /path/to/output.wav

# Adjust speech rate (default: 160 wpm) and volume (default: 0.9)
python3 /Users/song/bon-git/audio-tools/speak.py --text "Slower speech" --rate 120 --volume 1.0
```

### Full Pipeline: Transcribe + Speak

```bash
# 1. Transcribe WAV recordings to text
python3 /Users/song/bon-git/audio-tools/transcribe.py /Volumes/Untitled/RECORD/ --output-dir /Users/song/bon-git/audio-tools/output

# 2. Convert transcript to speech audio
python3 /Users/song/bon-git/audio-tools/speak.py --file /Users/song/bon-git/audio-tools/output/V2026-03-16-10-27-43.txt --output /Users/song/bon-git/audio-tools/output/spoken.wav
```

## Parameters

| Param | Description | Default |
|-------|-------------|---------|
| `--text` | Direct text input | - |
| `--file` | Path to text file | - |
| `--output` | Save to audio file (WAV) | None (plays live) |
| `--rate` | Words per minute | 160 |
| `--volume` | Volume 0.0 - 1.0 | 0.9 |

## Dependencies

- `pyttsx3` - offline TTS engine (uses macOS NSSpeechSynthesizer)
- Install: `pip install pyttsx3`

## Related

- Transcription script: `/Users/song/bon-git/audio-tools/transcribe.py`
- Uses OpenAI Whisper locally for speech-to-text
- Supports `--lang en` (default) and `--lang zh` (Chinese)
