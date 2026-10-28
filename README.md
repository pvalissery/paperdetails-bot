# paperdetails-bot

**Find the preprints.Simplify.  Keep the caveats.**

A small Next.js web app that searches recent arXiv preprints by keyword and drafts editable, simplified summaries.

## Features

- Live keyword search against the public arXiv Atom API
- Comma-separated keyword queries, date window, and result count
- Paper title, authors, abstract, categories, publication date, abstract/PDF links
- Edit, copy, or export the draft as `.md`
- Demo dataset for trying the interface without a live API request
- Responsive layout and clear preprint / human-review caveats

## Quick start

Requirements: Node.js 18.17+ (Node 20 LTS recommended) and npm.

```bash
git clone https://github.com/YOUR-USERNAME/paperdetails-bot.git
cd paperdetails-bot
npm install
cp .env.example .env.local
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

For a no-network preview, choose **Demo dataset** or click **Load sample papers**.

## How it works

1. The UI sends keywords, a date window, and a result limit to `/api/papers`.
2. The server route builds an arXiv query and fetches the public Atom API.
3. XML entries are parsed into paper metadata and filtered to the selected date window.
4. The browser turns the title and abstract into an editable Reddit Markdown draft.

The current summary generator is template-based and deterministic. It does **not** call an LLM and does not claim to infer methods or results beyond the abstract. The satire snippets are deliberately generic. For production-quality summaries, add a server-side LLM provider with evidence-grounded prompts and tests.

## Deploy

Deploy on Vercel or another Node-compatible host:

1. Push this repository to GitHub.
2. Import the repository into Vercel.
3. Deploy with the default Next.js settings.

**No API key** is required for the current template-based version. The app needs outbound network access to `export.arxiv.org` for live search.

## API

`GET /api/papers?q=single-cell%20proteomics&days=30&limit=8`

- `q`: required; comma-separated terms
- `days`: 1–365; default 30
- `limit`: 1–25; default 8

Returns `{ query, papers, source, fetchedAt }`, or an `error` object on failure.

## Responsible use

- Preprints are not necessarily peer reviewed.
- The abstract may omit limitations, methods, and contradictory evidence.
- Always open the paper and verify claims before posting.
- Satire targets inflated claims and academic hype, not researchers personally.
- Respect arXiv's API usage policies and each repository's terms.

## License

MIT — see `LICENSE`.
