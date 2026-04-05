# 🎙️ Audio to Text Converter

Convert audio files to text using **OpenAI Whisper** via the **Hugging Face Transformers** pipeline — running on GPU in Google Colab.

---

## 📋 Overview

This project demonstrates automatic speech recognition (ASR) using OpenAI's Whisper model loaded through the Hugging Face `transformers` pipeline. It transcribes audio files (e.g., `.mp3`) into plain text with minimal setup.

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- CUDA-compatible GPU (recommended; Google Colab with GPU runtime works perfectly)
- Internet connection (to download the model and audio)

### Run on Google Colab

> ✅ Recommended: Open the notebook directly in [Google Colab](https://colab.research.google.com/) and enable a **GPU runtime** (`Runtime → Change runtime type → GPU`).

---

## 🛠️ Installation

Install the latest version of Hugging Face Transformers from GitHub:

```bash
pip install git+https://github.com/huggingface/transformers
```

---

## 📦 Dependencies

| Package        | Purpose                              |
|----------------|--------------------------------------|
| `transformers` | Hugging Face pipeline & Whisper model |
| `torch`        | Backend for model inference (GPU/CPU) |
| `IPython`      | Display audio in Colab notebooks     |

---

## 💻 Usage

### 1. Check GPU Availability

```python
!nvidia-smi
```

### 2. Download a Sample Audio File

```bash
wget -O audio.mp3 http://www.moviesoundclips.net/movies1/darkknight/criminal.mp3
```

### 3. Play the Audio (Colab)

```python
from IPython.display import Audio, display
display(Audio('audio.mp3', autoplay=True))
```

### 4. Load the Whisper Pipeline

```python
from transformers import pipeline

whisper = pipeline(
    "automatic-speech-recognition",
    "openai/whisper-medium",
    device=0  # Use GPU (device=0); set to -1 for CPU
)
```

### 5. Transcribe Audio

```python
text = whisper('audio.mp3')
print(text)
```

**Sample Output:**

```python
{'text': ' Some men aren\'t looking for anything logical, like money. They can\'t be bought, bullied, reasoned, or negotiated with.'}
```

---

## 🧠 Model Details

| Property       | Value                        |
|----------------|------------------------------|
| Model          | `openai/whisper-medium`      |
| Task           | Automatic Speech Recognition |
| Source         | Hugging Face Model Hub       |
| Languages      | Multilingual (99 languages)  |
| Parameters     | ~300M                        |


To switch models, simply replace `"openai/whisper-medium"` with your preferred size in the pipeline.

---

## 📁 Project Structure

```
audio-to-text/
│
├── audio_to_text.py     # Main transcription script
├── audio.mp3            # Sample audio file (downloaded at runtime)
└── README.md            # Project documentation
```

---

## ⚙️ Configuration

| Parameter  | Description                              | Default              |
|------------|------------------------------------------|----------------------|
| `model`    | Whisper model variant                    | `whisper-medium`     |
| `device`   | `0` for GPU, `-1` for CPU                | `0` (GPU)            |
| input file | Path to local audio file or URL          | `audio.mp3`          |

---

## 📝 Notes

- **GPU strongly recommended** — CPU inference is significantly slower for medium/large models.
- The pipeline supports local file paths, URLs, and NumPy audio arrays as input.
- For long audio files, Whisper automatically handles chunking.
- For non-English audio, you can force a language: `whisper('audio.mp3', generate_kwargs={"language": "french"})`.

---

## 📄 License

This project uses:
- [OpenAI Whisper](https://github.com/openai/whisper) — MIT License
- [Hugging Face Transformers](https://github.com/huggingface/transformers) — Apache 2.0 License

---

## 🔗 References

- [Whisper Paper (Radford et al., 2022)](https://arxiv.org/abs/2212.04356)
- [Hugging Face Whisper Docs](https://huggingface.co/openai/whisper-medium)
- [Transformers ASR Pipeline Docs](https://huggingface.co/docs/transformers/main_classes/pipelines#transformers.AutomaticSpeechRecognitionPipeline)
