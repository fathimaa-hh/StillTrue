# StillTrue: Check what changed

**StillTrue** is a public-interest freshness checker for time-sensitive claims inside AI-generated answers. It is designed around a simple idea: when a chatbot gives a confident answer about a deadline, benefit, fee, rule, health recommendation, or software version, show people what current sources say and where the evidence comes from.

> **Important:** StillTrue is a verification aid, not medical, legal, financial, or government advice. The demo preview uses fictional fixture data. It does not perform a live search.

## What the prototype does

- Accepts a pasted answer and offers Health & safety, Benefits & visas, Consumer & money, and General focus modes.
- Extracts likely time-sensitive claims through a model routed by Bifrost, with a local heuristic fallback.
- Searches current web pages through Tavily and shows source links, snippets, publication dates when supplied, and a basic official-domain hint.
- Uses Bifrost to compare each claim with the retrieved text. When the model comparison is unavailable or uncertain, it reports **Can’t verify**.
- Shows a transparent 0–100 evidence score. The score is an evidence summary, **not** a probability of truth.
- Offers a self-contained demo preview so the interface can be explored without API credentials.

## Current prototype limits

This is a hackathon prototype, not a production-grade fact checker. Search snippets may omit context; publication dates may be missing; an official-looking domain is not a guarantee; models can misread evidence. The app does not independently establish a complete source-of-truth policy, does not yet provide a formally calibrated score, and never certifies medical or legal claims. Verify important decisions directly with the responsible agency or a qualified professional.

The app analyzes one answer at a time and does not save submissions to a database. The “suggested update” is generated from retrieved evidence and must be reviewed by a person.

## How the sponsor technologies fit

- **Tavily** provides live web search for each extracted claim.
- **Bifrost by Maxim AI** provides an OpenAI-compatible gateway for claim extraction and evidence comparison. Configure a provider/model in Bifrost; the app calls the `/chat/completions` route through the gateway.
- **Streamlit** provides the browser interface.

When Bifrost is unreachable, extraction falls back to a local sentence heuristic and evidence comparison returns **Can’t verify**. When Tavily credentials or service are unavailable, live checking stops with a clear error. The demo preview uses neither service.

## Run locally

Requires Python 3.10 or newer.

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
Copy-Item .env.example .env
streamlit run app.py
```

The first launch opens in demo preview mode. For live checks, configure both services:

### 1. Get a Tavily key

Create or sign in to a Tavily account at [app.tavily.com](https://app.tavily.com), then copy an API key from its dashboard. The project sends this key to Tavily from the Python server; it is never put in browser code.

### 2. Start Bifrost and connect a model provider

In a **second PowerShell window**, start Bifrost (this method needs Node.js and `npx` installed):

```powershell
npx -y @maximhq/bifrost
```

Keep that window open. Visit `http://localhost:8080`, open **Model Providers**, choose a provider such as OpenAI, and add that provider’s API key in Bifrost. The provider key is separate from the Tavily key. The sample model below is `openai/gpt-4o-mini`; use a model your configured provider supports. Provider API usage may incur charges, so check its billing and limits first. See the [Bifrost setup guide](https://docs.getbifrost.ai/quickstart/gateway/setting-up) and [provider configuration guide](https://docs.getbifrost.ai/quickstart/gateway/provider-configuration).

### 3. Put the keys in the project’s `.env`

In the StillTrue project folder, copy `.env.example` to `.env` and open `.env` in Notepad. Add the Tavily key. Keep the Bifrost URL and model as shown if you followed the local setup above:

Example `.env` values:

```dotenv
TAVILY_API_KEY=tvly-your_tavily_key
BIFROST_BASE_URL=http://localhost:8080/v1
BIFROST_API_KEY=
BIFROST_MODEL=openai/gpt-4o-mini
```

For a local Bifrost gateway with authentication disabled, leave `BIFROST_API_KEY` blank. If you enabled Bifrost authentication, put the Bifrost virtual key there; do not put your model provider key there. Save `.env`, restart StillTrue, and turn **Preview with demo data** off for a live check. Never commit `.env` or show either key in screenshots or recordings. `.gitignore` is set to exclude `.env` from Git.

## Repository layout

```text
app.py                 Streamlit interface and verification pipeline
requirements.txt        Python dependencies
.env.example            Environment variable template
.streamlit/config.toml  Theme and server defaults
SUBMISSION.md           Draft answers for the hackathon form
```

## Verification

The project was checked locally for Python syntax and the demo flow. Live provider calls require your own Tavily credentials and a running/configured Bifrost gateway. See `SUBMISSION.md` for the form fields and `outputs/StillTrue-Pitch.pptx` for the editable pitch deck.

## Responsible use

- Check the linked source itself and its date.
- Do not rely on this prototype for emergency, health, legal, financial, immigration, or benefits decisions.
- Treat retrieved web text as untrusted input.
- Use only authorized API credentials and follow provider terms.
- Clearly disclose AI use and third-party services in project submissions.

## License

No license has been selected yet. Add a license before inviting reuse or accepting contributions.
