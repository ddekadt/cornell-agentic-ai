# Gemini CLI — Free Setup Guide (Windows)

> **Up to date as of 11 September 2026.** If you are reading this later, assume some of it has changed.

Gemini CLI is a terminal-based agentic AI from Google. Free with a personal Google account, subject to rate limits.

> **Already have an agent?** If Claude Code, Codex CLI or Gemini CLI already works in your terminal, skip to section 7 and come to the workshop with what you have. However, you must be able to run **in the terminal** — the Codex app, the Claude desktop app and browser chatbots are not sufficient. If you cannot do this, ask your agent for help getting to the terminal. 

Use **PowerShell** throughout (Start → "PowerShell"). If you have **Windows Terminal** — standard on Windows 11, free in the Microsoft Store otherwise — use that instead and run PowerShell inside it. It handles colour and pasting better, and Gemini CLI is easier to read in it.

## 1. Let PowerShell run scripts

Do this first, or npm will be blocked twice — once installing, once running.

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
```

If Cornell IT manages your laptop you may get *"overridden by a policy defined at a more specific scope"*. Use **cmd** instead (Start → "cmd") and add `.cmd` to the commands below: `npm.cmd install -g @google/gemini-cli`, then `gemini.cmd`.

## 2. Install Node.js

Open PowerShell, and type `node --version`. If it's missing or below v20, get the **LTS (v24)** installer from [nodejs.org](https://nodejs.org/), or run:

```powershell
winget install --id OpenJS.NodeJS.LTS -e --accept-source-agreements --accept-package-agreements
```

If Windows says *"Windows protected your PC"*, click **More info → Run anyway**. Close PowerShell completely and reopen it, or Windows won't see the install. Then re-check.

## 3. Install Gemini CLI

```powershell
npm install -g @google/gemini-cli
```

Ignore the warning about `install scripts`, `keytar` and `node-pty`.

Verify with `gemini --version`.

## 4. Get an API key

At [aistudio.google.com/apikey](https://aistudio.google.com/apikey), login to your Google account, and click **Create API key**. You should not need to provide a credit card.

If asked to accept terms or pick a Cloud project, take the default.

Select the key and copy it to your clipboard.

## 5. Sign in

Start in a scratch folder (i.e. the folder for this workshop), not your user folder. Launch PowerShell from that folder, or navigate to the directory using `dir` and `cd`, then type `gemini` and press enter.

You should see:

```
> Sign in with Google      ← highlighted by default, no longer works
  Use Gemini API Key       ← use this one
  Vertex AI
```

Google retired "Sign in with Google" in June 2026, but it's still listed first and pre-selected. Press ↓ once and choose **Use Gemini API Key**, then paste with **Ctrl+V** or right-click (in Windows Terminal, Ctrl+Shift+V). Your key may be visible on screen as you paste, so don't do this while screen-sharing.

It will then ask about the folder. Choose **Trust folder**. In a trusted folder the agent creates, edits and deletes files and runs commands without asking each time.

## 6. Try it out

Type and press enter: 

```
Create a file called hello.txt containing today's date, then read it back to me.
```

An approval prompt and a new file in the directory means you're set up. Leave with `/quit`.

## 7. Before Friday — the rest of the toolchain

- **git** — `git --version`. If missing, install [Git for Windows](https://git-scm.com/download/win).
- **Clone the repo** — [https://github.com/ddekadt/cornell-agentic-ai](https://github.com/ddekadt/cornell-agentic-ai).
- **R or Python that can render.** Render any trivial `.qmd` or `.Rmd` to HTML once.
- **Install some packages now.** R: `sf`, `readxl`, `ggplot2`, `rmarkdown`. Python: `geopandas`, `openpyxl`, `matplotlib`, `pandas`. 

## Useful commands inside the CLI

- `/help` — list commands
- `/model` — list models and change between them
- `/auth` — change how you're signed in
- `/stats` — daily quota used
- `/clear` — start a fresh context
- `/quit` — exit
- `Ctrl+C` — cancel; press again to exit

## Limits & cautions

- **250 model requests per day**, resetting at midnight Pacific (3am Eastern). You can monitor this with `/stats`. If you run out, a second personal Google account gives you a second key.
- There is also a per-minute limit. The agent pauses, reports a quota error and retries itself.
- **Your API key is a password.** Don't paste it into documents, chats, or anything you might commit to git. Don't tell it to an agent. If it leaks, delete it and make another.
- Don't paste secrets or private data into the agent. 

## If something goes wrong

- **Red text ending in `[object Object]`** — look for `API_KEY_INVALID`. Type `/auth` and choose **Use Gemini API Key**. The box pre-fills with your old key, so press **Ctrl+C to clear it** before pasting.
- **`UNSUPPORTED_CLIENT`** — you chose "Sign in with Google". Type `/auth` and switch.
- **"running scripts is disabled on this system"** — you skipped section 1.
- **"gemini is not recognized"** — reopen PowerShell; check you did section 1; then try `$env:Path += ";$(npm config get prefix)"`.
- **Asked for your key every launch** — run `setx GEMINI_API_KEY "your-key"`, then reopen PowerShell.
- **"Ripgrep is not available"** — harmless.
