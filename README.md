# 📚 AI Chapter Question Generator

An AI-powered web app built with **Streamlit** and **Google Gemini**. Upload a chapter and get **20 MCQs, 5 short questions and 3 long questions** with model answers, created only from the chapter's content, in **English or Urdu**.

## Features

- Upload a chapter as **PDF, DOCX or TXT**; see the file name and a text preview
- Exactly **20 MCQs** (question, options A–D, correct answer, short explanation)
- Exactly **5 short questions** with simple model answers
- Exactly **3 long questions** with complete answers, headings and key points
- **Automatic model selection**: the app asks Google which Gemini models your API key can use and lists only those that support content generation (with a Refresh button)
- **Easy / Normal / Difficult** levels
- **English and Urdu** output (right-to-left display for Urdu)
- Tabs for MCQs, Short and Long questions; Show/Hide answer sections; "Show all answers" switch
- Download everything as a **TXT** file
- Loading indicator, validation of the question counts, and clear error messages (bad file, empty document, wrong API key, quota, no internet)
- API key is never hardcoded

## Technologies Used

- Python 3.10+
- Streamlit (user interface)
- Google Gemini API via Google AI Studio (`google-genai` library)
- pypdf and python-docx (reading files)
- GitHub (code) and Streamlit Community Cloud (hosting)

## Project Files

```
app.py            # the whole application
requirements.txt  # Python libraries
README.md         # this guide
```

## How to Get a Gemini API Key

1. Open <https://aistudio.google.com/apikey> and sign in with your Google account.
2. Click **Create API key** and copy it.
3. Keep it private. Never paste it into your code or upload it to GitHub.

## Install and Run on Your Computer

1. Install Python 3.10 or newer from <https://www.python.org/downloads/> (on Windows, tick **Add Python to PATH**).
2. Put the three project files in one folder, for example `chapter-question-generator`.
3. Open a terminal in that folder and create a virtual environment:

   ```bash
   python -m venv venv
   # Windows:
   venv\Scripts\activate
   # macOS / Linux:
   source venv/bin/activate
   ```

4. Install the libraries:

   ```bash
   pip install -r requirements.txt
   ```

5. Give the app your API key. The model dropdown in the sidebar fills itself once a valid key is present. Choose **one** option:

   - **Option A (easiest):** run the app and paste the key in the sidebar box.
   - **Option B (saved on your PC):** create a folder `.streamlit` and inside it a file `secrets.toml` containing:

     ```toml
     GEMINI_API_KEY = "paste-your-key-here"
     ```

6. Start the app:

   ```bash
   streamlit run app.py
   ```

   Your browser opens at <http://localhost:8501>.

## Upload the Project to GitHub

1. Create a free account at <https://github.com> and click **New repository**. Name it (for example `chapter-question-generator`), choose **Public**, and click **Create repository**.
2. **Protect your key first.** In your project folder create a file named `.gitignore` with this content:

   ```
   .streamlit/secrets.toml
   venv/
   __pycache__/
   ```

3. Install Git from <https://git-scm.com/downloads>, then run in your project folder (replace the URL with your repository's URL):

   ```bash
   git init
   git add app.py requirements.txt README.md .gitignore
   git commit -m "First version"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/chapter-question-generator.git
   git push -u origin main
   ```

   (Or use **Add file → Upload files** on the GitHub page and drag in `app.py`, `requirements.txt`, `README.md` and `.gitignore`. Do **not** upload `secrets.toml`.)
4. Refresh the GitHub page and check that your files are there and that no API key appears in any file.

## Deploy on Streamlit Community Cloud

1. Go to <https://share.streamlit.io> and sign in with **Continue with GitHub**. Allow access to your repository when asked.
2. Click **Create app** (or **New app**) and choose **Deploy a public app from GitHub**.
3. Select your repository, branch `main`, and main file path `app.py`.
4. Click **Advanced settings → Secrets** and paste:

   ```toml
   GEMINI_API_KEY = "paste-your-key-here"
   ```

5. Click **Deploy**. Wait a few minutes while the libraries install.
6. Your app gets a public link like `https://your-app-name.streamlit.app`. Share it with students and teachers.

To update the app later, change the files on GitHub (or `git push` again) and Streamlit redeploys automatically.

> Note: if you add your key under Secrets, everyone who uses your public app uses **your** Gemini quota. To avoid that, leave Secrets empty and let each user paste their own key in the sidebar.

## Troubleshooting

| Problem | Fix |
|---|---|
| "No text could be found" | The PDF is a scan (images). Use a text-based PDF, DOCX or TXT. |
| Urdu text looks broken after PDF upload | Some Urdu PDFs store text in a way that cannot be extracted properly. Use the DOCX or TXT version. |
| "API key was rejected" | Re-copy the key from Google AI Studio; make sure there are no spaces. |
| "Usage limit was reached" | Wait a minute, or choose a "flash-lite" model in the sidebar. |
| "Model is not available for your API key" | Pick another model in the sidebar. The list comes live from Google for your key, so it never contains models you cannot use. Click **Refresh models** if the list looks old. |
| "No Gemini models that support content generation" | Create a new key at <https://aistudio.google.com/apikey> and check that it belongs to a project with the Gemini API enabled. |
| Model list will not load | Check the key and your internet connection, then click **Refresh models**. |

## Important

AI can make mistakes. Always read the questions and answers before using them in a real exam or class.
