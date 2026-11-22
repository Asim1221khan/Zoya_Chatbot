# Zoya: AI Chatbot (Streamlit + Groq)

Zoya is a dark-themed AI chatbot built with Python 3.11, Streamlit and the official Groq API.

## Features

- Chat interface built with `st.chat_message()` and `st.chat_input()`, with streaming replies
- Sidebar configuration: API key validation, model dropdown, custom model ID
- System role templates: General Assistant, Python Tutor, Machine Learning Expert, AI & Robotics Trainer, Data Analyst, plus a custom system prompt
- Settings: temperature, max response tokens, Top-P, frequency penalty, presence penalty, seed, stop sequences
- Toggles for streaming and conversation history, and a limit on how many messages are sent as context
- New chat, clear history, reset settings
- Export the conversation as TXT or JSON
- Friendly error messages for bad keys, rate limits, timeouts and connection problems
- The API key is never hardcoded, logged or exported

## Project structure

```
zoya-chatbot/
├── chatbot.py          # the app
├── requirements.txt    # pip dependencies
├── environment.yml     # conda environment (Python 3.11)
├── .env                # your Groq API key goes here
├── .gitignore          # keeps .env out of Git
├── .streamlit/
│   └── config.toml     # dark theme
└── README.md
```

---

## Full setup guide

### Step 1. Install Python 3.11 with Miniconda

Miniconda installs conda, which creates an isolated Python 3.11 environment for this project. You do not need to install Python separately.

**Windows**

1. Download the Miniconda installer (64-bit) from <https://docs.conda.io/en/latest/miniconda.html>.
2. Run the installer and keep the default options.
3. Open **Anaconda Prompt** from the Start menu. Use it for every command below.

**macOS**

1. Download the macOS installer from the same page (Apple Silicon or Intel, matching your Mac), or with Homebrew:
   ```bash
   brew install --cask miniconda
   ```
2. Initialise your shell, then close and reopen the Terminal:
   ```bash
   conda init zsh
   ```

**Linux**

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

Accept the prompts, then close and reopen the terminal.

Check that conda works:

```bash
conda --version
```

### Step 2. Unzip the project

Unzip `zoya-chatbot.zip`, then move into the folder:

```bash
cd path/to/zoya-chatbot
```

On Windows, for example: `cd C:\Users\YourName\Downloads\zoya-chatbot`.

### Step 3. Create the conda environment with Python 3.11

```bash
conda create -n zoya python=3.11 -y
conda activate zoya
```

Check the version. It should print `Python 3.11.x`:

```bash
python --version
```

> Shortcut: `conda env create -f environment.yml` creates the environment and installs the packages in one step. Then run `conda activate zoya` and skip Step 5.

### Step 4. Add your Groq API key

1. Create a free account at <https://console.groq.com> and open **API Keys**: <https://console.groq.com/keys>.
2. Click **Create API Key** and copy the key (it starts with `gsk_`).
3. Open the `.env` file in the project folder with any text editor. It is a hidden file. Enable "Show hidden files" in your file manager if you cannot see it.
4. Paste the key after the equals sign, with no quotes and no spaces:
   ```
   GROQ_API_KEY=gsk_your_key_here
   ```
5. Save the file.

Never share this file or upload it to GitHub. The included `.gitignore` already excludes it from Git.

### Step 5. Install the dependencies

With the `zoya` environment active and the terminal inside the project folder:

```bash
pip install -r requirements.txt
```

### Step 6. Run Zoya

```bash
streamlit run chatbot.py
```

Streamlit opens the app in your browser at <http://localhost:8501>. If it does not open, paste that address into your browser. Stop the app with `Ctrl + C` in the terminal.

### Step 7. Start chatting

1. Zoya reads your key from `.env`. In the sidebar, open **API connection** and press **Validate** to confirm the key works. This also loads the models available to your account.
2. Pick a model, or enter a custom model ID.
3. Choose a system role, adjust the settings if you like, and type a message at the bottom.

Next time, you only need:

```bash
conda activate zoya
cd path/to/zoya-chatbot
streamlit run chatbot.py
```

---

## Using the sidebar

| Section | What it does |
| --- | --- |
| API connection | Validate the key, or paste a different key to override `.env` for this session. **Remove key** clears the pasted key. |
| Model | Choose from your account's models. A custom model ID overrides the dropdown. |
| System role | Pick a template or write your own prompt. Editing a template switches the role to Custom. |
| Generation settings | Temperature, max tokens, Top-P, penalties, seed, stop sequences. |
| Conversation | Turn streaming and history on or off, and set how many recent messages are sent as context. |
| Chat actions | New chat, clear history, reset settings, export TXT or JSON. |

When history is off, each message is sent to the model on its own, so Zoya has no memory of earlier turns. The conversation stays visible on screen.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| `conda` is not recognised | Use Anaconda Prompt on Windows, or run `conda init` and reopen the terminal. |
| `streamlit` is not recognised | Run `conda activate zoya` first, then `pip install -r requirements.txt`. |
| "No key found" in the sidebar | Check that `.env` contains `GROQ_API_KEY=gsk_...` on one line, save it, and refresh the page. |
| "Authentication failed" | The key is wrong, expired or has extra spaces or quotes. Create a new key and paste it again. |
| "Model not found" | Press **Validate** to load your account's models, or check the custom model ID. |
| "Rate limit reached" | Wait a moment and try again, or choose a smaller model. |
| Port 8501 is busy | Run `streamlit run chatbot.py --server.port 8502`. |
| Changed `.env` but nothing happens | Refresh the browser page. If it still fails, stop the app and run it again. |

## Security notes

- The key lives only in `.env`, or in the sidebar field for the current session.
- It is never printed, logged, or written into exported chats.
- Error messages shown in the app have any key text removed.
- Do not commit `.env` to Git or send it to anyone.

## Updating dependencies

```bash
conda activate zoya
pip install --upgrade -r requirements.txt
```
# Zoya_Chatbot
