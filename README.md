# Job Desk

A private job-search desk that runs as a [claude.ai](https://claude.ai) artifact. Upload your CV, answer a few questions about what you're looking for, and every job ad you paste in is scored against your profile. Each job then gets interview prep, a research prompt and a cover-letter draft, all written by Claude from your real CV.

Job Desk is a lightweight, browser-only companion to **[ai-job-search](https://github.com/ai-job-search-dev/ai-job-search)** by Mads Lorentzen. Its scoring framework, onboarding questions and application workflow are adapted from that project. If you want daily automated job searches, tailored LaTeX CVs and cover letters, and a drafter-plus-reviewer workflow, use ai-job-search with Claude Code.

## What it does

1. **Setup**
   - **CV upload:** PDF, Word or plain text. The file is read in your browser and only its text is sent to Claude.
   - **LinkedIn:** your profile link, plus an optional LinkedIn "Save to PDF" export for skills and your About text.
   - **Preferences:** target roles, industries, seniority, home city and commute, on-site/hybrid/remote, relocation, willingness to travel, minimum and target salary, contract type, hours, company size, notice period, start date, work permit, languages, confidential search, must-haves, deal-breakers, and facts that must never appear in applications.
   - **Review:** Claude summarises your CV into a profile you can correct before anything is scored.
2. **Score a job ad.** Paste a posting and get a fit score (technical 30%, experience 25%, culture 15%, career 30%; location pass/fail), a verdict, requirements, your gaps and warnings. Language and work-permit checks run first.
3. **Prepare with Claude**, for each job:
   - interview questions
   - questions to ask the interviewers
   - a 60-second pitch
   - honest answers to your gaps
   - STAR stories
   - salary talk
   - a cover-letter draft
4. **Research prompt** for each job, to paste into a Claude chat with web search.
5. **Search for new jobs:** one button searches LinkedIn for your target roles posted in the last 7 days (in your city and/or remote), one search per click, skips jobs you already have, and quick-scores the rest. Automatic search uses the Claude desktop app's built-in browser and currently works for the artifact's owner only. Everyone else can paste a results page and import it.
6. **Search ideas:** LinkedIn, Indeed and Google Jobs links for your target roles, plus suggestions for alternative titles and companies.
7. **Humanizer:** strips typical AI phrasing from English or German text without changing facts.
8. **Your data:** you can track a status and notes for each job, download everything as JSON, or delete it all.

## Privacy

- **Private storage:** each person's profile and jobs are stored under the artifact's `data/users/<id>` area. Only that person can read it; the person who published the page can't.
- **What goes to Claude:** CV text, job ads and your questions are sent to Claude to generate answers.
- **What isn't kept:** the CV file itself is not stored, only the extracted text and the summary you approve.
- **What's in the page:** the page contains no personal data. Everything is entered by whoever opens it.

## Use it

### Option 1: open a shared link
If someone shared their published Job Desk with you, open the link while signed in to claude.ai and follow the setup. Your data stays private to your account.

### Option 2: publish your own copy
1. Download `index.html` from this repository.
2. In Claude (claude.ai or Claude Code), ask: *"Publish this file as an artifact with the capabilities sample, db, user, downloads, and mcp with the host server host:claude_browser (tools navigate, get_page_text, find)."*
3. Open the artifact and run the setup. To let others use it, share the artifact from its **Share** menu. Each person gets their own private profile.

The page needs these claude.ai artifact capabilities:

| Capability | Used for |
|---|---|
| `sample` | Claude answers: CV summary, scoring, prep, humanizer |
| `db` + `user` | Private per-person storage of profile and jobs |
| `downloads` | "Download my data" export |
| `mcp` → `host:claude_browser` (`navigate`, `get_page_text`, `find`) | "Search now": reads LinkedIn's public job search in the Claude desktop app's browser |

It does not work as a static site (for example GitHub Pages), because these capabilities only exist inside claude.ai.

### Libraries
- **PDF text extraction:** [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 (Apache 2.0).
- **Word (.docx) text extraction:** [mammoth.js](https://github.com/mwilliamson/mammoth.js) 1.6.0 (BSD-2).
- **Fonts:** Bricolage Grotesque and IBM Plex from Google Fonts (OFL).

All are loaded from cdnjs and Google Fonts.

## Limits

- **Automatic search is owner-only and on demand.** "Search now" works in the Claude desktop app for the artifact's owner; other people use the paste import. There's no scheduled daily search in the page: use ai-job-search for that.
- **Quick scores are rough.** Found jobs are scored from title, company and location only. Paste the full ad under "Add a job" for a proper score.
- **No live research.** Claude's answers inside the page have no web access. Use the research prompt in a chat with web search to check company facts.
- **Check everything.** Review every application text before sending it.

## Credits

- **[ai-job-search](https://github.com/ai-job-search-dev/ai-job-search)** by Mads Lorentzen, MIT licence: the fit-scoring framework, onboarding questions, honest-gap and STAR interview approach, and writing-style rules that Job Desk adapts. See [NOTICE.md](NOTICE.md).
- **[blader/humanizer](https://github.com/blader/humanizer)** and **[F-DK/humanizer-de](https://github.com/F-DK/humanizer-de)**: the patterns the humanizer removes.

## Licence

MIT, see [LICENSE](LICENSE).
