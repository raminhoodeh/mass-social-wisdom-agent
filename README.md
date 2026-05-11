# Social Extractor

A multimodal AI web app that extracts, transcribes, and categorises content from Instagram Reels, Instagram Posts (including carousels), YouTube videos, and local image files — then exports everything as a clean, Notion-ready `.docx` file.

Built with **Flask**, **Google Gemini 2.5 Flash**, and the **SociaVault API**.

![UI Preview](https://img.shields.io/badge/Flask-3.0-black?style=flat-square&logo=flask) ![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat-square&logo=python) ![Gemini](https://img.shields.io/badge/Gemini-2.5_Flash-orange?style=flat-square&logo=google)

---

## The User Journey

Here is exactly how you will use this app from start to finish:

### 1. Get Your API Keys
To power the AI and social scraping, you need two APIs. You'll place these keys in a `.env` file in the root of the project:
- **Google Gemini API**: Get your free key at [Google AI Studio](https://aistudio.google.com/app/apikey). This acts as the brain for OCR, content composition, and categorisation.
- **SociaVault API**: Get your key at [SociaVault](https://sociavault.com). This handles the heavy lifting of extracting transcripts and captions from Instagram and YouTube URLs.

### 2. Prepare Your Content
- **URLs**: Copy a list of Instagram (Reels/Posts) or YouTube URLs. You can paste them messy, with text or tracking tags (like `?igsh=...`) attached. The app automatically cleans them and extracts just the links.
- **Local Images**: If you have screenshots or slide decks, just drop the image files directly into the `Scan/` folder on your computer.

### 3. Run the Extraction
- Open the web interface at `http://127.0.0.1:5001`.
- Paste your URLs into the left panel and click **Extract**.
- **Live UI**: Watch the right panel as the "Liquid Glass" UI updates in real-time. You'll see the AI transcribing videos, OCR-ing image slides, composing the text, and figuring out the correct category.

### 4. Import to Notion
- Once finished, click **Download Results**. 
- You'll receive a fully structured `.docx` file exported to your `Results/` folder.
- All extracted content is categorised (e.g., "Finance", "Health"), grouped by topic similarity, and formatted with clean H1 headers and source links. Simply drag and drop this file into Notion for a perfect import.
- Any URLs that failed to process are saved in a `failed_urls_*.txt` file so you can easily retry them later.

---

## Features

- **Multi-Platform Extraction**: Paste any mix of Instagram or YouTube URLs and the app figures out the rest.
- **Advanced OCR**: Instagram carousels and static image posts are OCR'd via Gemini Vision, turning slide decks into structured text.
- **Intelligent Composition**: Raw transcripts, OCR data, and captions are woven together by Gemini into polished, readable prose — not a summary, but a faithful reconstruction.
- **Auto-Categorisation**: Every item is automatically filed into one of 8 categories (Finance, AI, Health, Romance, Film, Conspiracy, Personal Branding, or Other) using keyword overrides and Gemini reasoning.
- **Similarity Sorting**: Within each category, items are reordered by topic proximity so related content sits together.
- **Notion-Ready Export**: Results are exported as a structured `.docx` (H1 headers + source links) that Notion imports perfectly.
- **Live UI**: A real-time dual-column "Liquid Glass" frontend lets you watch the LLM transcribe each item as it happens.
- **URL Sanitisation**: Auto-strips Instagram tracking parameters (`igsh`, `si`, `utm_*`) and unwraps login-redirect URLs before hitting the API.
- **Scan Folder**: Drop local image files (screenshots, slide decks) into `Scan/` and they'll be OCR'd and merged into the same session export.

---

## Quick Setup Guide

1. **Clone the repo**
   ```bash
   git clone https://github.com/your-username/social-extractor.git
   cd social-extractor
   ```

2. **Set up a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate   # Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure your API keys**
   Copy the example env file and fill in your keys:
   ```bash
   cp .env.example .env
   ```
   *Open `.env` and add your Gemini and SociaVault API keys.*

5. **Run the app**
   ```bash
   python app.py
   ```
   Open **http://127.0.0.1:5001** in your browser.

---

## Directory Structure

```
social-extractor/
├── app.py                  # Flask backend — routing, extraction, LLM, docx generation
├── requirements.txt        # Python dependencies
├── .env.example            # API key template (copy to .env)
├── templates/
│   └── index.html          # Real-time Liquid Glass UI
├── Scan/                   # Drop local images here for OCR
├── Processed/              # Images are moved here after OCR (auto-managed)
└── Results/                # .docx exports + failed URL logs (auto-managed)
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3.10+, Flask 3.0 |
| AI / LLM | Google Gemini 2.5 Flash (`google-genai`) |
| Image OCR | Gemini Vision API via Pillow |
| Social Scraping | SociaVault API |
| Export | `python-docx` |
| Frontend | Vanilla HTML/CSS/JS (no framework) |
