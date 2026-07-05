# AI Job Search

## Custom Commands (`.opencode/commands/`)
- `/setup` — populates profile from `documents/`, CV import, or interview. Re-run with `--section search` to update search queries only.
- `/apply <url|text>` — evaluate fit → draft CV + cover letter → spawn reviewer subagent → revise → compile & inspect PDFs.
- `/expand` — scans documents, GitHub, online profiles for hidden competencies. Additive only.
- `/reset profile|documents|all` — destructive. Requires typing `RESET` to confirm.

## Skills (auto-loaded by opencode)
- `.claude/skills/job-application-assistant/` — profile, writing rules, templates, evaluation framework, interview prep
- `.claude/skills/job-scraper/` — `/scrape` orchestration, search queries
- `.claude/skills/upskill/` — gap analysis
- `.agents/skills/*/` — 5 Bun-based CLI tools for Danish + LinkedIn job portals

## LaTeX Compilation (mandatory, never skip)
- **CV:** `cd cv && lualatex main_<company>.tex` — exactly 2 pages. Use `\needspace` for orphan prevention, `\enlargethispage` for overflow.
- **Cover letter:** `cd cover_letters && xelatex cover_<company>_<role>.tex` — exactly 1 page. Use `xelatex` (cover.cls requires fontspec).
- Bullet font mismatch fix: close `\lettercontent{}`, wrap `\begin{itemize}` in `{\raggedright\fontspec[...]{Raleway-Medium}\fontsize{11pt}{13pt}\selectfont ...\par}`.
- CV uses moderncv banking style, blue color scheme.

## Job Search CLI Tools
- **Dependencies:** `bun install` in each `.agents/skills/*/cli/` directory (5 tools).
- **LinkedIn search** (`linkedin-search`): country-agnostic, no auth. Personal use only (ToS).
- Usage pattern for all tools: `search` → `detail <id>`.

## Salary Benchmarking (optional)
- `python salary_lookup.py "Company Name" --city "City" --json`
- Requires `salary_data.json` in repo root. Skipped if absent.

## Verification Checklist (required for every application)
- All claims match profile — never fabricate skills, experience, or achievements
- Independent verification of company claims via webfetch/websearch
- CV exactly 2 pages, cover letter exactly 1 page
- CV compiled with lualatex, cover letter with xelatex
- No orphaned `\cventry` titles, signature block visible
- No em-dashes, no cliches, no unverified company claims (see `03-writing-style.md`)

## What's Gitignored (personal files)
- `cv/main_*.tex` (except `main_example.tex`), `cover_letters/cover_*.tex` — application output
- `documents/*/`, `salary_data.json`, `job_search_tracker.csv`, `job_scraper/seen_jobs.json`
- `upskill/*.md`, `.agents/**/node_modules/`
