---
title: twin-agent-pmi
app_file: app.py
sdk: gradio
sdk_version: 6.29.1
---
# Twin Agent PMI

A Gradio-based AI career twin that answers questions about a person's background, skills, experience, and professional interests. The application uses Gemini through an OpenAI-compatible API and serves as a conversational front end for a personal digital twin.

## Features

- Conversational career assistant powered by Gemini
- Profile context derived from a LinkedIn PDF and a local profile summary
- Gradio web interface with example prompts
- Contact-interest capture through Pushover
- Unanswered-question logging through Pushover
- Python 3.12 project configuration with `uv`

## Project structure

```text
.
├── app.py                 # Gradio application and chat flow
├── context.py             # Digital twin system prompt and profile context
├── tools.py               # Pushover tool definitions and handlers
├── styles.py              # Gradio interface styling and examples
├── linkedin.pdf           # LinkedIn profile PDF used as knowledge context
├── summary.txt            # Plain-text summary of the person's profile
├── requirements.txt       # Dependency list for standard pip installs
├── pyproject.toml         # Project metadata and uv configuration
└── uv.lock                # Reproducible uv dependency lockfile
```

## Requirements

- Python 3.12+
- A Google Gemini API key
- Pushover application token and user key for notifications
- A LinkedIn PDF named `linkedin.pdf`
- A profile summary named `summary.txt`
- `uv` (recommended) or `pip`

## Installation

Using `uv`:

```bash
uv sync
```

Alternatively, install the requirements with `pip`:

```bash
python3.12 -m pip install -r requirements.txt
```

## Configuration

Create a `.env` file in the project root with the following variables:

```env
GOOGLE_API_KEY=your_google_gemini_api_key
PUSHOVER_TOKEN=your_pushover_app_token
PUSHOVER_USER=your_pushover_user_key
```

The application loads these variables automatically with `python-dotenv`.

The profile context is loaded from:

- `linkedin.pdf` — the person's LinkedIn profile, converted to text
- `summary.txt` — a concise description of their professional background

> Ensure these files are present before starting the application. The source code does not generate or download them.

## Run the application

With `uv`:

```bash
uv run app.py
```

The command opens a local Gradio interface. A terminal URL will be displayed when the application starts.

## Usage

Ask the digital twin about topics such as:

- Career background and experience
- Technical skills and projects
- Professional goals and interests
- Ways to get in touch

The assistant stays in character and redirects unrelated questions back to professional topics. If it cannot answer a question, it records the question through Pushover and explains that it does not know the answer.

## Notes

- The app uses the Gemini model `gemini-3.5-flash-lite`.
- The current implementation records contact details and unanswered questions through Pushover rather than storing them locally.
- `summary.txt` and `linkedin.pdf` are required for the system prompt and profile context.

## License

This project is licensed under the [MIT License](LICENSE).

Copyright (c) 2026 Israel Friday.
