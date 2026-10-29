# Learning the Claude API with TypeScript

A hands-on, notebook-based course on the [Claude API](https://platform.claude.com/docs) using the
official [Anthropic TypeScript SDK](https://github.com/anthropics/anthropic-sdk-typescript) and the
[Deno Jupyter kernel](https://docs.deno.com/runtime/reference/cli/jupyter/).

## Lessons

| #   | Notebook                                 | Topics                                        |
| --- | ---------------------------------------- | --------------------------------------------- |
| 001 | [Requests](notebooks/001_requests.ipynb) | Load API key, send a message, print the reply |

## Setup

**1. Install Deno** (2.x)

```bash
brew install deno        # or see https://docs.deno.com/runtime/getting_started/installation/
```

**2. Register the Deno Jupyter kernel** (once per machine)

```bash
deno jupyter --install
```

**3. Add your API key**

```bash
cp .env.example .env
# then edit .env and paste your key from https://platform.claude.com/settings/keys
```

`.env` is git-ignored. Never print your key in a notebook cell: cell outputs are saved in the
`.ipynb` file and get committed with it.

**4. Open a notebook**

- **VS Code:** install the _Jupyter_ extension, open a notebook, and pick the **Deno** kernel (top
  right).
- **JupyterLab:** `pip install jupyterlab && jupyter lab`, then choose the **Deno** kernel.

## Project layout

```
.
├── .env.example       # template for your API key
└── notebooks/         # one notebook per lesson
```

There is no `deno.json`. Each notebook imports packages straight from npm with a pinned version
(`import Anthropic from "npm:@anthropic-ai/sdk@1.3.0"`). Deno downloads them on first run, so there
is nothing to install.

## Practices used in this project

- **Secrets in `.env`**, loaded with the `dotenv` npm package. The SDK reads `ANTHROPIC_API_KEY`
  from the environment, so the key never appears in code.
- **Pinned package versions** in every import, so lessons keep working when new versions ship.
- **Type-safe response handling:** check each content block's `type` before reading its `text`.
- **Clear outputs before committing** so responses (and anything sensitive) don't end up in git.

## Model and cost

Lessons use `claude-haiku-5-5`, the cheapest Claude model ($0.10 per million input tokens, $0.50 per
million output tokens). Lesson 001 makes one small request, which costs a fraction of a cent.
