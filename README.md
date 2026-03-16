# Audio Tools

Local speech-to-text and text-to-speech utilities using OpenAI Whisper and pyttsx3. No API keys required.

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

## Dependencies

- [openai-whisper](https://github.com/openai/whisper) - local speech recognition
- [pyttsx3](https://github.com/nateshmbhat/pyttsx3) - offline text-to-speech
- [torch](https://pytorch.org/) - ML runtime for Whisper
