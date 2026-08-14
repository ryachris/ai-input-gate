# Input Gate

An AI input inspection checkpoint. Paste a piece of content you're about to hand to (or produce with) an AI system, a brief, a draft, a data summary, and it runs the text against four governance gates before it ships:

1. **Source of Truth**: is the content traceable to a named, identifiable source?
2. **Freshness**: is it dated, and is the date plausible for its claims?
3. **Claim Attribution**: are specific claims (numbers, quotes, entities) individually sourced?
4. **Named Owner**: is one accountable human named, not a team?

Each gate returns pass / needs review / fail with specific notes, plus an overall CLEARED / NEEDS REVIEW / BLOCKED stamp.

The tool is the working prototype for the [AI Input Governance Framework](FRAMEWORK.md), which defines all six gates (gates 5 and 6 are process controls, not text-inspectable, so the tool implements 1-4).

## Why

AI output looks polished regardless of input quality, so bad inputs no longer look bad; they get laundered into confident-sounding output and cost more review time, not less. Gating inputs is cheaper than auditing outputs. The full argument is in [FRAMEWORK.md](FRAMEWORK.md).

## Running it

The tool is a single HTML file that calls the Anthropic Messages API (Claude Sonnet). Two ways to run it:

### 1. In the browser with your own API key

Open the page (GitHub Pages or the local file), paste your Anthropic API key into the key field, paste your content, and run. The key is held in the page only for the duration of your session, is sent only to `api.anthropic.com`, and is never stored or transmitted anywhere else. Get a key at [console.anthropic.com](https://console.anthropic.com/).

### 2. As a Claude.ai artifact (no key needed)

Paste the contents of `index.html` into a Claude.ai conversation and ask Claude to render it as an artifact. Inside the artifact environment the API call is authenticated automatically, so the key field can be left empty.

## Limitations

- Implements gates 1-4 only; confidence tiering (gate 5) and change detection (gate 6) are process controls that live in your workflow, not in text inspection.
- The freshness gate checks whether a verification date is present, not whether it falls within the framework's category thresholds (30/90/180/365 days), which require knowing the input's category.
- It inspects what the text claims about itself. A well-formatted lie passes; this is a first-pass hygiene gate, not a fact-checker.

## Files

- `index.html`: the inspection tool (self-contained, no build step)
- `FRAMEWORK.md`: the six-gate governance framework the tool implements
- `LICENSE`: MIT

Built with Claude as part of an internal AI tooling challenge.
