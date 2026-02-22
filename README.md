# HateShield AI

HateShield AI is a full-stack content safety and audience-insight toolkit.

It combines:
- **Text toxicity analysis** (hate speech / offensive / toxic / safe)
- **Emotion analysis** (anger, fear, joy, sadness, disgust)
- **Image moderation analysis**
- **Audience comment sentiment aggregation** from URL or manual comment lists
- **Pre-publication post review** with quality, risk, and engagement scoring

---

## Features

### 1) Text Analyzer
- Analyze single text input for toxicity class and confidence.
- Return emotion breakdown and processing time.

### 2) Image Detection
- Upload an image file for moderation analysis.
- Uses a multimodal model pipeline via the backend `ImagePredictor`.

### 3) Audience Analysis
- Accepts either:
  - a `post_url` / `url` (supports `http`, `https`, and local `file://` paths), or
  - manual comments (`comments[]` or newline text input).
- Extracts and de-duplicates comments from HTML.
- Produces sentiment percentages and dominant reaction trends.

### 4) Post Analysis (Pre-Publish Safety Check)
- Evaluates `caption`, `hashtags`, and `description`.
- Outputs:
  - toxicity risk level (`LOW`, `MEDIUM`, `HIGH`)
  - quality score
  - engagement score
  - actionable suggestions
  - publish recommendation (`APPROVED` / `NEEDS REVISION`)

---

## Project Structure

```
HateShield/
├─ backend/
│  ├─ app.py
│  ├─ requirements.txt
│  ├─ requirements-train.txt
│  └─ ml/
│     ├─ predictor.py
│     ├─ image_predictor.py
│     ├─ train_model.py
│     ├─ train_dataset.csv
│     ├─ hate_speech_model.pkl
│     └─ vectorizer.pkl
├─ frontend/
│  ├─ index.html
│  ├─ dashboard.html
│  ├─ text-analyzer.html
│  ├─ image-detection.html
│  ├─ audience-analysis.html
│  ├─ post-analysis.html
│  ├─ faceAI.html
│  ├─ settings.html
│  ├─ css/
│  ├─ js/
│  ├─ assets/
│  └─ models/
├─ test_positive.html
├─ test_negative.html
├─ test_neutral.html
├─ TESTING_GUIDE.md
└─ setup_and_run.bat
```

---

## Tech Stack

### Backend
- Python 3.8+
- Flask + Flask-CORS
- scikit-learn
- joblib
- Pillow
- transformers
- torch

### Frontend
- HTML, CSS, JavaScript
- Static pages served with `python -m http.server`

---

## Quick Start (Windows)

### Option A: One-click startup
From project root, run:

```bat
setup_and_run.bat
```

This script:
1. verifies Python,
2. installs backend dependencies,
3. trains model if missing,
4. starts backend on `http://127.0.0.1:5000`,
5. starts frontend on `http://localhost:8000`.

### Option B: Manual startup

#### 1) Backend
```powershell
cd backend
py -m pip install -r requirements.txt
py app.py
```

#### 2) Frontend (new terminal)
```powershell
cd frontend
py -m http.server 8000
```

Open: `http://localhost:8000`

---

## API Endpoints

Base URL: `http://127.0.0.1:5000`

### `GET /`
Health check.

### `POST /analyze`
Analyze one text string.

Request:
```json
{ "text": "sample text" }
```

### `POST /analyze_image`
Analyze uploaded image.

Request: `multipart/form-data` with field `image`.

### `POST /analyze_audience`
Analyze comments from URL or manual input.

Request examples:

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
Pre-publication post audit.

Request:
```json
{
  "caption": "Your caption",
  "hashtags": "#example #ai #safety",
  "description": "Longer post details",
  "target_audience": "Developers"
}
```

---

## Testing

Use local HTML fixtures for reliable audience-analysis validation:
- `test_positive.html`
- `test_negative.html`
- `test_neutral.html`

For complete testing instructions and expected sentiment distributions, see `TESTING_GUIDE.md`.

---

## Notes & Limitations

- Some social platforms block scraping or require authentication.
- Dynamic comments loaded only through heavy client-side JavaScript may not be extractable.
- URL extraction quality depends on target page HTML structure.

---

## Troubleshooting

- If dependencies fail to install, update `pip` first:
  ```powershell
  py -m pip install --upgrade pip
  ```
- If backend does not start, ensure port `5000` is free.
- If frontend does not load API data, confirm backend is running and CORS is enabled.

---

## License

No license file is currently included in this repository. Add a `LICENSE` file before public/commercial distribution.