# 🛡️ HateShield AI

> **Production-grade AI Moderation & Audience Intelligence Platform**

[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-REST%20API-000000?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com)

HateShield is a comprehensive AI-powered content moderation platform designed for creators and teams. Evaluate text, images, and audience reactions **before content goes live** with confidence scoring and actionable insights.

---

## 📋 Table of Contents

- [✨ Key Features](#key-features)
- [🎯 Why HateShield](#why-hateshield)
- [🔧 Core Modules](#core-modules)
- [🏗️ Tech Stack](#tech-stack)
- [📦 Prerequisites](#prerequisites)
- [🚀 Quick Start](#quick-start)
- [🔌 API Reference](#api-reference)
- [🧪 Testing](#testing)
- [📄 License](#license)

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🔤 **Text Analysis** | Classifies content into hate speech, offensive, toxic, or safe with confidence scoring |
| 🖼️ **Image Moderation** | Advanced visual content analysis for potentially harmful material |
| 👥 **Audience Sentiment** | Analyzes audience reactions from URLs or manual comment inputs |
| 📊 **Post Quality Scoring** | Pre-publication risk assessment with improvement recommendations |
| ⚡ **Real-time Processing** | Fast JSON APIs for production integration |
| 🧪 **Local Testing** | Offline fixtures for repeatable validation and demos |

---

## 🎯 Why HateShield

Online content moves fast—and moderation often happens too late. HateShield provides a practical, **pre-publication workflow** to:

- ✅ Detect toxic and hateful text with confidence metrics
- ✅ Flag potentially harmful visual content
- ✅ Analyze audience sentiment automatically
- ✅ Score post quality and publish risk with actionable feedback

---

## 🔧 Core Modules

### 1. 🔤 Text Analyzer
Classifies text content with detailed analysis:
- Categorization: Hate Speech, Offensive, Toxic, Safe
- Confidence scores for each category
- Emotional tone detection
- Processing metrics

### 2. 🖼️ Image Detection
Visual content moderation pipeline:
- Batch image uploads supported
- Deep learning-based classification
- Confidence-based flagging
- Instant results

### 3. 👥 Audience Analysis
Multi-source sentiment analysis:
- URL-based comment extraction
- Manual comment input
- Text block analysis
- Smart deduplication and cleaning
- Local `file://` fixtures for offline testing

### 4. 📊 Post Analysis
Comprehensive pre-publication review:
- Caption, hashtags, description analysis
- Target audience consideration
- Quality, engagement, and risk scores
- AI-powered improvement suggestions
- Publish/hold recommendations

---

## 🏗️ Tech Stack

<div>

**Backend**
- Python 3.8+
- Flask + Flask-CORS
- scikit-learn, joblib
- Pillow
- transformers, torch

**Frontend**
- HTML5 / CSS3 / JavaScript
- Responsive multi-page interface
- Built-in HTTP server

</div>

---

## 📦 Prerequisites

- **Python** 3.8 or newer
- **pip** (latest recommended)
- **Windows PowerShell** or Command Prompt
- **Internet connection** (for first-time dependency installation)

---

## 🚀 Quick Start

### ⚡ Option A: Automated Setup (Windows)

One command to get everything running:

```bash
setup_and_run.bat
```

This script automatically:
1. ✅ Verifies Python installation
2. ✅ Installs all dependencies
3. ✅ Trains ML models (if needed)
4. ✅ Launches backend at `http://127.0.0.1:5000`
5. ✅ Serves frontend at `http://localhost:8000`

### 📝 Option B: Manual Setup

**Terminal 1 - Backend:**

```powershell
cd backend
py -m pip install -r requirements.txt
py app.py
```

**Terminal 2 - Frontend:**

```powershell
cd frontend
py -m http.server 8000
```

Then open **`http://localhost:8000`** in your browser.

---

## 📁 Project Structure

```
HateShield/
├── backend/
│   ├── app.py                 # Flask API server
│   ├── requirements.txt        # Runtime dependencies
│   ├── requirements-train.txt  # ML training dependencies
│   └── ml/
│       ├── predictor.py        # Text classification
│       ├── image_predictor.py  # Image moderation
│       ├── train_model.py      # Model training script
│       └── train_dataset.csv   # Training data
├── frontend/
│   ├── index.html             # Dashboard home
│   ├── text-analyzer.html     # Text moderation UI
│   ├── image-detection.html   # Image upload interface
│   ├── audience-analysis.html # Sentiment analysis
│   ├── post-analysis.html     # Full post review
│   ├── faceAI.html           # Face expression detection
│   ├── css/                   # Stylesheets
│   ├── js/                    # Client-side logic
│   └── models/               # ML model weights
├── test_positive.html         # Sample test fixture
├── test_negative.html         # Sample test fixture
├── test_neutral.html          # Sample test fixture
└── TESTING_GUIDE.md          # Detailed testing docs
```

---

## 🔌 API Reference

**Base URL:** `http://127.0.0.1:5000`

### Health Check
```http
GET /
```

### Text Analysis
```http
POST /analyze
Content-Type: application/json

{
  "text": "Your text to analyze"
}
```

### Image Moderation
```http
POST /analyze_image
Content-Type: multipart/form-data

[image field]
```

### Audience Sentiment
```http
POST /analyze_audience
Content-Type: application/json

# Option 1: From URL
{
  "post_url": "https://example.com/post"
}

# Option 2: From comments
{
  "comments": ["comment one", "comment two"]
}

# Option 3: From text block
{
  "text": "line 1\nline 2"
}
```

### Post Quality Review
```http
POST /analyze_post
Content-Type: application/json

{
  "caption": "Your caption",
  "hashtags": "#example #ai #safety",
  "description": "Extended post details",
  "target_audience": "Developers"
}
```

---

## 🧪 Testing

Local test fixtures are included for validation:

| File | Purpose |
|------|---------|
| `test_positive.html` | Positive sentiment example |
| `test_negative.html` | Negative sentiment example |
| `test_neutral.html` | Neutral sentiment example |

📚 **See `TESTING_GUIDE.md` for complete testing instructions.**

### Common Test Scenarios
- ✅ Testing text moderation with various input types
- ✅ Batch image analysis
- ✅ URL-based audience extraction
- ✅ Model accuracy validation

---

## ⚙️ Training Notes

- **Default behavior:** Models train automatically only if required artifacts are missing
- **Manual training:** Use scripts in `backend/ml/` with dependencies from `requirements-train.txt`
- **Custom datasets:** Place training data in `backend/ml/train_dataset.csv`

---

## ⚠️ Known Limitations

| Limitation | Details |
|-----------|---------|
| **Web Scraping** | Some platforms restrict scraping or require authentication |
| **JavaScript Content** | Heavily rendered comments may be partially unavailable |
| **Page Structure** | Extraction quality depends on target site structure |

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| Installation fails | `py -m pip install --upgrade pip` |
| Port 5000 unavailable | Ensure backend isn't already running on that port |
| Frontend API errors | Verify backend is running: `http://127.0.0.1:5000` |
| Dependency issues | Delete virtual environment and reinstall |

---

## 👤 Author

Created and maintained by **syedashraf49**

---

## 📄 License

This project is licensed under the **MIT License**. See the `LICENSE` file for complete terms.

