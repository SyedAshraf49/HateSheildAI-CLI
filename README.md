# HateShield AI

[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-API-000000?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)

Production-style AI moderation and audience intelligence platform for safer digital publishing.

HateShield helps creators and teams evaluate text, images, and audience reactions before content goes live.

## Quick Links

- [Project Preview](#project-preview)
- [Why HateShield](#why-hateshield)
- [Core Modules](#core-modules)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [API Endpoints](#api-endpoints)
- [Testing](#testing)
- [License](#license)

## Portfolio Summary

HateShield demonstrates end-to-end product thinking across machine learning, backend API design, and frontend user experience.

- Multi-module moderation workflow in a single web app.
- Practical JSON APIs for real integration scenarios.
- Local testing fixtures for reliable verification and demos.
- Clear deployment path for both quick run and manual setup.

## Project Preview

![HateShield dashboard preview](frontend/assets/readme-preview.svg)

## Why HateShield

Online content moves fast, and moderation often happens too late. HateShield provides a practical, pre-publication workflow to:

- Detect toxic and hateful text with confidence scoring.
- Flag potentially harmful visual content.
- Analyze audience sentiment from URLs or imported comments.
- Score post quality and publish risk with actionable recommendations.

## Core Modules

### 1. Text Analyzer
- Classifies text into hate speech, offensive, toxic, or safe categories.
- Returns confidence values, emotional cues, and processing time.

### 2. Image Detection
- Accepts uploaded images for moderation checks.
- Uses a dedicated backend image prediction pipeline.

### 3. Audience Analysis
- Supports `post_url` / `url`, manual comments, or text blocks.
- Handles local `file://` fixtures for offline and repeatable testing.
- Cleans and deduplicates extracted audience comments.

### 4. Post Analysis
- Reviews caption, hashtags, description, and target audience.
- Produces quality, engagement, and toxicity-risk signals.
- Provides improvement suggestions and a publish recommendation.

## Tech Stack

### Backend
- Python 3.8+
- Flask + Flask-CORS
- scikit-learn, joblib
- Pillow
- transformers, torch

### Frontend
- HTML, CSS, JavaScript
- Multi-page UI served with `python -m http.server`

## Architecture Snapshot

1. Frontend collects text/image/post/audience inputs.
2. Requests are sent to Flask API endpoints.
3. ML pipelines in `backend/ml` run classification and scoring.
4. Structured JSON responses drive dashboard-style results.

## Prerequisites

- Python 3.8 or newer
- pip (latest recommended)
- Windows PowerShell or Command Prompt
- Internet connection for first-time dependency installation

## Repository Structure

```text
HateShield/
|-- backend/
|   |-- app.py
|   |-- requirements.txt
|   |-- requirements-train.txt
|   `-- ml/
|       |-- predictor.py
|       |-- image_predictor.py
|       |-- train_model.py
|       `-- train_dataset.csv
|-- frontend/
|   |-- index.html
|   |-- dashboard.html
|   |-- text-analyzer.html
|   |-- image-detection.html
|   |-- audience-analysis.html
|   |-- post-analysis.html
|   |-- faceAI.html
|   |-- settings.html
|   |-- assets/
|   |-- css/
|   |-- js/
|   `-- models/
|-- test_positive.html
|-- test_negative.html
|-- test_neutral.html
|-- TESTING_GUIDE.md
`-- setup_and_run.bat
```

## Getting Started

### Option A: One-Step Launch (Windows)

From the project root, run:

```bat
setup_and_run.bat
```

The script checks Python, installs dependencies, trains the model (if needed), starts the backend at `http://127.0.0.1:5000`, and serves the frontend at `http://localhost:8000`.

### Option B: Manual Launch

Backend terminal:

```powershell
cd backend
py -m pip install -r requirements.txt
py app.py
```

Frontend terminal:

```powershell
cd frontend
py -m http.server 8000
```

Then open `http://localhost:8000`.

## Training Notes

- In normal use, the startup script trains only if required artifacts are missing.
- For explicit training workflows, use files in `backend/ml` and `backend/requirements-train.txt`.

## API Endpoints

Base URL: `http://127.0.0.1:5000`

### `GET /`
Service health endpoint.

### `POST /analyze`
Runs text toxicity and emotion analysis.

```json
{ "text": "sample text" }
```

### `POST /analyze_image`
Runs moderation analysis on an uploaded image.

Request type: `multipart/form-data` with `image` field.

### `POST /analyze_audience`
Runs audience sentiment analysis from URL or provided comments.

```json
{ "post_url": "https://example.com/post" }
```

```json
{ "comments": ["comment one", "comment two"] }
```

```json
{ "text": "line 1\nline 2\nline 3" }
```

### `POST /analyze_post`
Runs pre-publication content quality and risk analysis.

```json
{
  "caption": "Your caption",
  "hashtags": "#example #ai #safety",
  "description": "Longer post details",
  "target_audience": "Developers"
}
```

## Testing

Local fixtures included for audience-analysis validation:

- `test_positive.html`
- `test_negative.html`
- `test_neutral.html`

Detailed test instructions are in `TESTING_GUIDE.md`.

## Limitations

- Some platforms restrict scraping or require authentication.
- Heavily JavaScript-rendered comments may be partially unavailable.
- Extraction quality depends on the source page structure.

## Troubleshooting

- Upgrade pip if installs fail: `py -m pip install --upgrade pip`
- Ensure port `5000` is free for the backend.
- Confirm backend availability if frontend API calls fail.

## Author

Created and maintained by **syedashraf49**.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.