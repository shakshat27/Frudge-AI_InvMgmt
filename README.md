# Frudge AI: Smart Fruit Basket

A camera watches your fruit basket or fridge shelf; a multimodal AI tells you what's there, how fresh it is, how many days it has left, and what you can cook with it.

<!-- screenshot: docs/app.png -->

![Frudge AI](https://github.com/user-attachments/assets/7e9536f5-6879-4dd0-8bb3-a87b0cabfc35)

## Features

- **Webcam auto-capture**: the browser grabs a frame every 30 s and uploads it, or you upload up to 3 photos at once
- **Item recognition**: identifies each fruit or food item and its quantity
- **Freshness**: estimates the ripeness stage and how many days until it is no longer edible
- **Recipe ideas**: suggests recipes from a single item and from everything in view, with one described in full
- Custom prompt per request, so the same backend can answer other questions about the images

## How it works

```
Browser (webcam.js) ──multipart POST /upload (≤3 images + prompt)──► Flask (backend.py, AWS EC2)
                                                                     │ upload images + prompt
                                                                     ▼
                                                              Gemini 1.5 Pro
```

The backend saves the images, uploads them to the Gemini Files API, sends them with a nutritionist-style prompt and returns the answer to the page.

## Tech stack

Python · Flask · Google Gemini 1.5 Pro (multimodal) · JavaScript · MediaDevices API · AWS EC2

## Run locally

```bash
pip install flask flask-cors google-generativeai
export GOOGLE_API_KEY=<your Gemini key>
mkdir -p uploads && python backend.py      # :5000
```

Open `index.html` and point the upload URL in `webcam.js` at your backend.

## Roadmap

- Track inventory over time and alert on low stock or items about to spoil
- Suggest and place grocery orders for missing items
- On-device detection (YOLO) before the AI call, to cut cost and latency
- Mobile dashboard

## Team

Akshat Sharma, [akioin11](https://github.com/akioin11)
