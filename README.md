# VARTA-SETU 🌐🎙️

[![Hackathon](https://img.shields.io/badge/Hackathon-AI--BHARAT-orange.svg)](https://ai4bharat.iitm.ac.in/)
[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Framework-Django-green.svg)](https://www.djangoproject.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![AWS](https://img.shields.io/badge/Cloud-AWS%20Polly-FF9900?logo=amazonservices)](https://aws.amazon.com/polly/)

**VARTA-SETU** (Varta = Conversation/News, Setu = Bridge) is an innovative AI-driven pipeline developed for the **AI-BHARAT Hackathon**. The project aims to democratize access to global information by translating live international news broadcasts (like CNN, BBC, etc.) into local Indian languages in real-time. 

By leveraging cutting-edge Speech-to-Text (STT), Machine Translation, and specialized Text-to-Speech (TTS) models like **Indic TTS** and **Amazon Polly**, VARTA-SETU breaks the language barrier for millions of Indian citizens.

---

## ✨ Key Features

- **Live Stream Integration**: Directly fetches audio from live YouTube news channels using `yt-dlp`.
- **High-Accuracy Transcription**: Utilizes `faster-whisper` for near real-time English speech-to-text conversion.
- **Multi-Model TTS**: 
    - **Indic TTS**: High-quality synthesis for regional Indian nuances.
    - **Amazon Polly**: Professional-grade neural voices for seamless listening.
- **Smart Translation**: Employs `deep-translator` and **Amazon Bedrock (Claude 3.5 Sonnet)** for context-aware translation into Indian languages.
- **Real-time Pipeline**: Designed for low-latency processing using Django Channels and asynchronous workers.
- **Audio Refinement**: Uses `pydub` and `soundfile` to ensure output audio is clear and synchronized.

---

## 🛠 Tech Stack

- **Backend**: Django, Daphne (Asynchronous Server Gateway Interface)
- **AI/ML Models**:
    - **Transcription**: Faster-Whisper (OpenAI)
    - **Translation**: Deep-translator, Amazon Bedrock (Claude 3.5 Sonnet)
    - **TTS**: AI4Bharat Indic-TTS, Amazon Polly, Parler-TTS
- **Cloud Services**: AWS Boto3 (Polly, Bedrock)
- **Audio Processing**: Pydub, Soundfile, FFmpeg, ImageIO
- **Core Libraries**: Torch (PyTorch), NumPy, Transformers, Protobuf

---

## 📂 Repository Structure

```text
.
├── core/                   # Django project configuration
├── config/                 # Environment and model configurations
├── refined_indic_tts.py    # Optimized logic for Indic TTS generation
├── manage.py               # Django management script
├── requirements.txt        # Project dependencies
├── test_*.py               # Comprehensive test suite for individual components
├── verify_pipeline.py      # Script to validate the end-to-end integration
└── .env.example            # Template for environment variables
```

---

## 🚀 Installation Guide

### Prerequisites
- Python 3.9 or higher
- FFmpeg installed on your system
- AWS Credentials (for Polly and Bedrock)

### Step 1: Clone the Repository
```bash
git clone https://github.com/your-username/varta-setu.git
cd varta-setu
```

### Step 2: Set Up Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
# Install Parler-TTS from source as required
pip install git+https://github.com/huggingface/parler-tts.git
```

### Step 4: Configure Environment Variables
Create a `.env` file based on `.env.example`:
```env
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
AWS_REGION=your_region
# Add other necessary keys
```

### Step 5: Database Migrations
```bash
python manage.py migrate
```

---

## 💻 Usage Examples

### 1. Running the Integration Verification
Before starting the server, verify that the AI models and AWS services are connected correctly:
```bash
python verify_pipeline.py
```

### 2. Testing YouTube Audio Extraction
To test if the system can fetch audio from a live link:
```bash
python test_ytdlp.py
```

### 3. Generating Indic TTS Output
To test the specific translation and voice generation for Indian languages:
```bash
python test_indic_tts.py
```

### 4. Start the Application
```bash
python manage.py runserver
```

---

## 🛠 Verification Tools
The repository includes several debug scripts to ensure smooth operation:
- `check_models.py`: Checks if local models (Whisper/Transformers) are loaded correctly.
- `test_polly.py`: Validates AWS Polly connectivity and voice generation.
- `debug_model_load.py`: Profiles memory and loading time for AI models.

---

## 🤝 Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. 

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

**VARTA-SETU** - *Connecting the world to India, one voice at a time.* 🇮🇳
