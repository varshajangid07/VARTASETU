# VARTA-SETU 🌐🎙️

[![Hackathon](https://img.shields.io/badge/AI--FOR--BHARAT-Hackathon-orange.svg)](https://aiforbharat.iitm.ac.in/)
[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Framework-Django-092e20.svg)](https://www.djangoproject.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![AWS](https://img.shields.io/badge/AWS-Polly%20%26%20Bedrock-232F3E?logo=amazon-aws)](https://aws.amazon.com/)

**VARTA-SETU** (meaning *Communication Bridge*) is an advanced AI-powered pipeline designed for the **AI-FOR-BHARAT Hackathon**. The project breaks the language barrier by providing real-time translation and voice synthesis of live global news channels (like CNN, BBC, etc.) into local Indian languages. 

By leveraging cutting-edge STT (Speech-to-Text), LLM-based refinement, and a hybrid TTS (Text-to-Speech) approach using **Indic TTS** and **Amazon Polly**, VARTA-SETU makes global information accessible to every Indian in their mother tongue.

---

## 🚀 Key Features

- **Live Stream Integration**: Directly fetches audio from YouTube Live news channels using `yt-dlp`.
- **High-Accuracy Transcription**: Utilizes `faster-whisper` for near-instant and accurate English speech-to-text conversion.
- **LLM Refinement**: Uses **Amazon Bedrock (Claude 3.5 Sonnet)** to ensure translations are contextually accurate and culturally relevant for Indian audiences.
- **Hybrid TTS Engine**: 
    - **Amazon Polly**: For high-quality, neural cloud-based synthesis.
    - **Indic TTS / Parler-TTS**: For localized, high-fidelity Indian language nuances.
- **Asynchronous Processing**: Built with **Django Channels** and **Daphne** to handle real-time audio streams efficiently.
- **Multi-Language Support**: Targeted at major Indian languages including Hindi, Marathi, Bengali, Tamil, Telugu, and more.

---

## 🛠️ Tech Stack

### Backend & Infrastructure
- **Language:** Python 3.9+
- **Framework:** Django, Django Channels (WebSockets)
- **Server:** Daphne (ASGI)
- **Audio Processing:** Pydub, Soundfile, FFMPEG

### AI/ML Models
- **Speech-to-Text:** `faster-whisper`
- **Translation:** `deep-translator` & Amazon Bedrock (Claude 3.5 Sonnet)
- **Text-to-Speech:** 
    - **Cloud:** Amazon Polly (Boto3)
    - **Local/Open Source:** Indic TTS, Parler-TTS, Transformers (HuggingFace)
- **Compute:** PyTorch

---

## 📁 Repository Structure

```text
├── core/                   # Project settings and routing
├── config/                 # Configuration files for models
├── refined_indic_tts.py    # Logic for specialized Indian language synthesis
├── manage.py               # Django management script
├── requirements.txt        # Project dependencies
├── test_*.py               # Comprehensive test suite for various components
├── verify_pipeline.py      # End-to-end integration verification
└── .env.example            # Template for environment variables
```

---

## ⚙️ Installation Guide

### Prerequisites
- Python 3.9 or higher
- **FFMPEG** installed on your system
- AWS Account (for Polly and Bedrock access)
- NVIDIA GPU (optional but recommended for local inference)

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/varta-setu.git
cd varta-setu
```

### 2. Set Up Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
# Note: Parler-TTS is installed directly from GitHub as specified in requirements.txt
```

### 4. Configuration
Create a `.env` file based on `.env.example`:
```bash
cp .env.example .env
```
Fill in your credentials:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `DATABASE_URL` (if using external DB)

### 5. Run Migrations
```bash
python manage.py migrate
```

---

## 📋 Usage

### Verifying Components
Before running the full pipeline, verify that individual services are working:
```bash
# Test Amazon Polly
python test_polly.py

# Test YouTube Stream Downloader
python test_ytdlp.py

# Test Local Indic TTS
python test_indic_tts.py
```

### Running the Application
To start the development server with WebSocket support:
```bash
daphne -p 8000 core.asgi:application
```

### Running the Integrated Pipeline
To verify the full integration from stream to translated audio:
```bash
python verify_pipeline.py
```

---

## 🛠️ Development & Debugging

The repository includes several scripts to help debug specific parts of the AI pipeline:
- `debug_model_load.py`: Check if Torch and HuggingFace models load correctly in your environment.
- `check_indictts_config.py`: Validates the configuration for the local TTS engine.
- `test_audio_debug.py`: Utility to verify audio sample rates and formats.

---

## 🤝 Contributing

We welcome contributions to VARTA-SETU! 
1. **Fork** the repository.
2. **Create a Feature Branch** (`git checkout -b feature/AmazingFeature`).
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`).
4. **Push** to the branch (`git push origin feature/AmazingFeature`).
5. **Open a Pull Request**.

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🌟 Acknowledgments

- **AI-FOR-BHARAT** for the inspiration and platform.
- **AWS** for providing the Bedrock and Polly infrastructure.
- **HuggingFace** for the `faster-whisper` and `parler-tts` models.

---
*Built with ❤️ for a more connected India.*
