---
name: speech-to-text
description: Transcribe audio WAV files to text using local Whisper model. Supports English (default) and Chinese. Outputs .txt files.
---

# Speech-to-Text Skill

Transcribe audio recordings to text using local OpenAI Whisper. No API key needed.

## Skill Metadata

```yaml
name: speech-to-text
version: 1.0.0
description: Transcribe audio files to text using local Whisper
triggers:
  - "transcribe"
  - "speech to text"
  - "audio to text"
  - "convert audio"
  - "extract text from audio"
```

## Instructions

When the user asks to transcribe audio, run the transcription script:

```bash
python3 /Users/song/bon-git/audio-tools/transcribe.py <input> [options]
```

### Input

- `<input>` can be a single WAV file or a directory of WAV files.
- Default audio source: `/Volumes/Untitled/RECORD/`
- Default output dir: `/Users/song/bon-git/audio-tools/output/`

### Options

| Flag | Description | Default |
|------|-------------|---------|
| `--lang en` | English | auto-detect |
| `--lang zh` | Chinese | - |
| `--model` | `tiny`, `base`, `small`, `medium`, `large` | `base` |
| `--output-dir` | Where to save .txt files | same as input |

### Examples

```bash
# Single file, English (auto)
python3 /Users/song/bon-git/audio-tools/transcribe.py /Volumes/Untitled/RECORD/V2026-03-16-10-27-43.WAV --output-dir /Users/song/bon-git/audio-tools/output

# All files in directory
python3 /Users/song/bon-git/audio-tools/transcribe.py /Volumes/Untitled/RECORD/ --output-dir /Users/song/bon-git/audio-tools/output

# Chinese audio
python3 /Users/song/bon-git/audio-tools/transcribe.py recording.wav --lang zh

# Higher accuracy
python3 /Users/song/bon-git/audio-tools/transcribe.py recording.wav --model medium
```

### After Transcription

- Read the output .txt file and show the user the content
- If the user wants TTS, use the `/text-to-speech` skill

## Dependencies

- `openai-whisper` + `torch` (installed in base conda env)
- Models download on first use (~140MB for base, ~1.5GB for medium)
