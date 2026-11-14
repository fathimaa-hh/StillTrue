# Hackathon submission draft — StillTrue

Use these values in the Global AI Hackathon submission form. Replace bracketed fields after publishing the repository and recording a demo. Do not submit the form until the public links and PPT upload are ready.

## Primary project

- **Theme:** AI Agents & Intelligent Systems
- **Problem Statement:** Build a Stale-Answer Detector for AI Applications
- **Project title:** StillTrue: Check What Changed
- **GitHub project URL:** `[ADD PUBLIC REPOSITORY URL AFTER PUBLISHING]`
- **Demo video link:** `[OPTIONAL — ADD VIDEO URL]`
- **PPT file:** `outputs/StillTrue-Pitch.pptx`
- **Also integrating a Tavily problem statement:** Yes — Stale-Answer Detector (same project uses Tavily and Bifrost)
- **Second project:** NA (not applied)

## Short project description

StillTrue checks time-sensitive claims inside AI-generated answers against live web sources. It flags each claim as Current, Outdated, or Can’t verify, shows source links and available dates, explains its evidence score, and suggests an update for a person to review. Public-interest focus modes cover health and safety, government benefits and visas, consumer and money questions, and general queries. StillTrue is a verification aid, not official or professional advice.

## Problem addressed

People increasingly receive confident AI answers about deadlines, eligibility, fees, rules, prices, and guidance. Those details can change after a model’s training data was collected. A stale answer can cause a missed application window, an unexpected cost, or unsafe decisions. People with less time or access to expert help may have the hardest time checking whether an answer is current.

## What is novel about this approach

The prototype makes source freshness and uncertainty visible in a public-interest workflow. It puts source links and dates next to each claim, offers public-sector-oriented search focus modes, and returns “Can’t verify” when evidence or model comparison is insufficient. Its score is presented as an evidence summary rather than a probability of truth.

## Architecture and sponsor technology use

- **Bifrost by Maxim AI:** OpenAI-compatible model gateway for claim extraction and comparison of claims with retrieved evidence.
- **Tavily:** Live web search for each time-sensitive claim.
- **Streamlit/Python:** Browser UI and orchestration.
- **Fallback behavior:** Local heuristic extraction if the model gateway is unavailable; uncertain comparison is labeled Can’t verify. The demo fixture is fictional and clearly labeled.

## Prototype walkthrough (about 2 minutes)

1. Open the app in preview mode and point out that the sample source and claim are illustrative, not live research.
2. Show the four focus modes and explain that they guide the search toward relevant public agencies.
3. Explain the live flow: extract claims through Bifrost, search with Tavily, compare evidence through Bifrost, then show claim status and source details.
4. If API credentials are configured, turn off preview mode and run one non-sensitive example question. Open an evidence panel and show the source link and date.
5. Close with the limitations: evidence score is not a probability, sources require human review, and the app is not professional advice.

## Slide deck notes

The pitch deck is included as `outputs/StillTrue-Pitch.pptx`. It covers the problem, intended users, workflow, sponsor roles, trust controls, prototype scope, and next steps. Replace the repository placeholder in this file and deck after the public GitHub repository exists.

## Form checklist

- [ ] Publish a public GitHub repository with this README and the app files.
- [ ] Confirm the chosen problem statement in the form is the Stale-Answer Detector.
- [ ] Upload the PPTX pitch deck.
- [ ] Add a demo video link if recorded.
- [ ] Ensure no API keys or private information are committed or shown.
- [ ] Submit the form before its deadline.
