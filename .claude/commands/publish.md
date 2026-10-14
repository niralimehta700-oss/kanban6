---
description: Security-scan, screenshot, document and deploy the IT PMO board to GitHub and GitHub Pages
---

Publish this project. Stop and report if any step fails.

1. **Security scan (before anything is uploaded).** Check every file that will be committed:
   - Search for secrets: API keys, tokens, passwords, private keys, `.env` files, real email addresses other than in `FORMSUBMIT_ENDPOINT`.
   - In `index.html`, confirm all user-provided text is rendered through `escapeHtml()`, there is no `eval`/`new Function`/inline event-handler attributes built from data, and no external scripts, stylesheets or fonts are loaded.
   - Confirm no browser storage (localStorage, sessionStorage, IndexedDB, cookies) is used.
   - Use the cybersecurity-analyst skill if it is installed. Report findings; do not publish while a high-severity finding is open.
2. **Screenshot.** Use the Playwright MCP tools: `browser_navigate` to the GitHub Pages URL (`https://<owner>.github.io/<repo>/`), or to the local `index.html` if Pages is not live yet, then `browser_take_screenshot` with a full-page capture saved to `docs/screenshot.png`.
3. **README.** Write or refresh `README.md` with: a one-paragraph description, the live site link, a feature list, how to run it locally, the FormSubmit activation note, and a `## Screenshot` section containing `![Website screenshot](docs/screenshot.png)`.
4. **Commit and push.** Stage the changes, commit with a clear message, and `git push -u origin <current branch>`. If there is no `origin`, ask for the repo.
5. **Repo About.** Run `gh repo edit --description "IT PMO Kanban board: single-file vanilla HTML/CSS/JS" --homepage "https://<owner>.github.io/<repo>/" --add-topic kanban --add-topic project-management --add-topic vanilla-js`.
6. **GitHub Pages.** Make sure Pages builds from GitHub Actions: `gh api -X POST repos/<owner>/<repo>/pages -f build_type=workflow` (ignore "already exists"), then confirm the `Deploy to GitHub Pages` workflow in `.github/workflows/pages.yml` ran green with `gh run list --workflow pages.yml --limit 1`.
7. **Report** the security findings, the screenshot path, the commit, the pushed branch and the live URL.
