# AI Content Assistant

A beginner-friendly Streamlit app that uses the official Groq Python SDK to create platform-ready social media posts from user-provided facts.

## Features

- Supports LinkedIn, Facebook, Instagram, and X/Twitter
- Uses a distinct writing blueprint for every platform instead of recycling one
  generic post structure
- Automatically converts only the LinkedIn hook to copyable Unicode bold text
- Seven content types, seven tones, and three length options
- Produces a hook, main post, call to action, caption, and 5-10 hashtags
- Uses short, mobile-readable paragraphs
- Keeps generated content in Streamlit session state
- Copy-friendly result and TXT download
- Reset button, input validation, spinner, and friendly error messages
- Prompt-injection resistance and explicit non-fabrication rules
- Secure API-key handling through Streamlit Secrets

## Technology stack

- Python
- Streamlit
- Official Groq Python SDK
- Groq production model: `openai/gpt-oss-120b`
- GitHub
- Streamlit Community Cloud

The model ID is stored once in the clearly labeled `GROQ_MODEL` variable in `app.py`, so it is easy to update later. Groq model availability and free-plan limits can change; check the official Groq Models and Rate Limits pages if deployment reports that the model is unavailable.

## Project structure

```text
ai-content-assistant/
├── .streamlit/
│   └── secrets.toml.example
├── .gitignore
├── app.py
├── README.md
└── requirements.txt
```

Your real `.streamlit/secrets.toml` is local-only and must never be uploaded.

## Local installation

### 1. Install Python

Install Python 3.10 or newer from https://www.python.org/downloads/. During Windows installation, enable **Add Python to PATH**.

### 2. Download this project

Put all files in one folder and keep the `.streamlit` subfolder.

### 3. Create a virtual environment (recommended)

Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

## Create a Groq API key

1. Open https://console.groq.com/ and sign in.
2. Open **API Keys**.
3. Select **Create API Key**, give it a recognizable name, and copy it once.
4. Never paste it into `app.py`, GitHub, screenshots, or public messages.

## Configure Streamlit Secrets locally

1. Inside the project folder, open the `.streamlit` folder.
2. Copy `secrets.toml.example` and rename the copy to `secrets.toml`.
3. Replace the placeholder in the new file:

```toml
GROQ_API_KEY = "paste_your_real_key_here"
```

The real `secrets.toml` is already blocked by `.gitignore`. Do not remove that rule.

## Run locally

From the project folder, run:

```bash
streamlit run app.py
```

The browser normally opens automatically. Otherwise, open the Local URL shown in the terminal.

## Upload through the GitHub website

1. Sign in at https://github.com/.
2. Select **New repository**.
3. Name it `ai-content-assistant`, choose **Public** or **Private**, and create it.
4. On the empty repository page, choose **uploading an existing file**.
5. Upload `app.py`, `requirements.txt`, `README.md`, `.gitignore`, and the `.streamlit` folder containing only `secrets.toml.example`.
6. Confirm that `.streamlit/secrets.toml` is **not** in the upload list.
7. Add a commit message such as `Add AI Content Assistant` and select **Commit changes**.

GitHub sometimes hides dotfiles in a file picker. If needed, enable hidden-file viewing in your operating system. Preserve the `.streamlit/secrets.toml.example` path; do not move it to the root.

## Deploy on Streamlit Community Cloud

1. Open https://share.streamlit.io/ and sign in with GitHub.
2. Select **Create app** (or **New app**).
3. Choose your GitHub repository and the correct branch, normally `main`.
4. Set the main file path to `app.py`.
5. Open **Advanced settings** and find **Secrets**.
6. Enter this, using your real key:

```toml
GROQ_API_KEY = "paste_your_real_key_here"
```

7. Select **Deploy** and wait for installation to finish.
8. Open the app URL and test generation.

## Testing checklist

- Leave Topic or Target audience empty: Generate must stay disabled.
- Test each platform and confirm the style changes appropriately.
- Test Short, Medium, and Long.
- Confirm all five headings appear in the result.
- Confirm 5-10 hashtags are returned.
- Use Reset and confirm inputs plus output are cleared.
- Generate content, interact with the page, and confirm the result remains.
- Download the TXT file and open it.
- Temporarily test without a secret and confirm a friendly message appears.
- Confirm no real key exists in GitHub.
- Review every factual claim before publishing.
- Compare one topic across all four platforms and confirm that LinkedIn uses
  professional white space, Instagram uses caption-style rhythm, Facebook feels
  community-oriented, and X is a concise post or numbered thread.
- Confirm that only the LinkedIn hook—not the complete post—is Unicode bold.
- Change the platform and confirm the previous result clears before generating
  the new platform-specific version.

## Common errors and solutions

### `GROQ_API_KEY is missing`

Add the exact key name `GROQ_API_KEY` to local `.streamlit/secrets.toml` or the deployed app's **Settings → Secrets**, then restart/reboot the app.

### Invalid API key / status 401

Remove extra spaces, confirm quotation marks are correct, or create a new key in Groq Console. Update the secret, not `app.py`.

### Rate limit reached / status 429

Wait and retry. Check your current account limits in Groq Console. Shorter prompts and fewer rapid requests can help.

### Model unavailable or request rejected

Check Groq's official Supported Models page. If the model changed, edit only `GROQ_MODEL` in `app.py`, commit the update, and reboot the app.

### `ModuleNotFoundError`

Confirm `requirements.txt` is at the repository root and named exactly. Locally, run `pip install -r requirements.txt`.

### App does not deploy

Open **Manage app → Logs**, read the first error, confirm the repository/branch/main-file path, and verify that Python files uploaded completely.

### Network or connection error

Retry after checking the connection and Groq service status. A temporary provider or hosting interruption may resolve itself.

### Output-format error

Retry once. The app rejects responses missing any required section instead of displaying incomplete output.

## Updating after deployment

1. Open a file in GitHub and select the pencil icon.
2. Make the change and commit it to the deployed branch.
3. Streamlit Community Cloud normally redeploys automatically.
4. If it does not, open **Manage app** and select **Reboot app**.
5. Never put the API key in a code update; edit it only under app Secrets.

## Security notes

- Never commit `.streamlit/secrets.toml` or `.env`.
- The example secrets file contains a placeholder only.
- Never print, log, or display API keys.
- If a key is exposed, revoke it immediately in Groq Console and create a new one.
- Treat AI output as a draft and verify it before publishing.

## Future improvements

- Post history stored safely for the current session
- Multiple content variants
- Language and brand-voice controls
- Platform-specific character counter
- Editable templates
- Export to Markdown or PDF

## License

This project is provided under the MIT License. You may use, modify, and distribute it with appropriate attribution. Add a separate `LICENSE` file before public distribution if you want GitHub to detect the license automatically.
