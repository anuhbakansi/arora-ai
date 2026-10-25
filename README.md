# arora-ai
# 🌌 NovaLearn: AI Study Studio

A black-and-blue Streamlit app powered by Google Gemini (`gemini-3.8-flash`).

## Features
- **Explain Anything**: upload PDF, Word, PowerPoint, images, text/code, audio and get an easy explanation.
- **Lectures & Audio**: record in the browser or upload several recordings, then get TL;DR, key points, terms and likely exam topics.
- **Smart Notes**: bullet, Cornell, mind-map or cheat-sheet notes from any text, file or lecture.
- **Roadmap**: enter field, level (Beginner / Intermediate / Advanced / PhD) and time, then get a phased plan.
- **Exam**: 100–200 MCQs generated in parallel for speed. After submitting you get fireworks, balloons and a reward token (Diamond / Gold / Silver / Brave Learner).
- Every output can be downloaded as Markdown.

## Run locally
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
streamlit run app.py
```
Get a **free** API key at https://aistudio.google.com/apikey and paste it in the sidebar. Or set it permanently:

```bash
export GEMINI_API_KEY="your_key"      # Windows PowerShell: $env:GEMINI_API_KEY="your_key"
```
or create `.streamlit/secrets.toml`:
```toml
GEMINI_API_KEY = "your_key"
# GEMINI_MODEL = "gemini-3.8-flash"   # optional override
```

### Optional: dark theme + bigger uploads
Create `.streamlit/config.toml`:
```toml
[theme]
base = "dark"
primaryColor = "#2f7bff"
backgroundColor = "#04060c"
secondaryBackgroundColor = "#0a1222"
textColor = "#e8eefc"

[server]
maxUploadSize = 1000
```

## Push to GitHub
```bash
git init
printf "venv/\n__pycache__/\n.streamlit/secrets.toml\n.env\n" > .gitignore
git add app.py requirements.txt README.md .gitignore
git commit -m "NovaLearn: first version"
git branch -M main
```
Create an empty repo on https://github.com/new (no README), then:
```bash
git remote add origin https://github.com/<your-username>/novalearn.git
git push -u origin main
```
**Never commit your API key.** `secrets.toml` is in `.gitignore`.

## Deploy on Streamlit Community Cloud (free)
1. Go to https://share.streamlit.io and sign in with GitHub.
2. Click **Create app** → choose your repo, branch `main`, main file `app.py`.
3. Open **Advanced settings → Secrets** and paste: `GEMINI_API_KEY = "your_key"`
4. Click **Deploy**. Every `git push` redeploys automatically.

## Honest notes about "no limits" and "free"
- The app puts **no limit** on text, files, audio length or number of lectures.
- Gemini's **free tier has its own rate limits** that no app can remove. If you hit one, wait a minute. Each user can paste their own free key in the sidebar so they use their own quota instead of yours.
- Files over ~15 MB are sent through the Gemini Files API automatically.
- Streamlit Community Cloud is free but has modest resources and sleeps when idle.
- Check the model name if you get a "not found" error: sidebar → Advanced.
