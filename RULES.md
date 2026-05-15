# blip-research — Operating Rules

## Rule #1 — Git Workflow (Commits)
Never use the GitHub web editor to commit files.
Always use the proper git CLI workflow:
```
git pull
git add .
git commit -m "message"
git push
```
Requires: GitHub PAT (classic, repo scope)
Setup: `git remote set-url origin https://<TOKEN>@github.com/jeremytrindade/blip-research.git`

## Rule #2 — Browser Navigation Fallback
When the `navigate` MCP tool fails with a site-blocked error:
1. Try `window.location.href` via `javascript_tool` instead
2. Open a fresh tab with `tabs_create_mcp`, then navigate
3. Use the `computer` tool to type the URL in the address bar

Known hard blocks (blocked even in Chrome extension): reddit.com — all tool interactions are blocked even if the page loads visually. Content from Reddit must be pasted by the user.

Note: Claude in Chrome can access sites that the `navigate` MCP tool cannot. These are two separate blocklists. Always try Chrome-based tools before giving up.

## Rule #3 — Research File Structure
- Naming: `YYYYMMDD-topic-slug.md`
- Required sections: Date, Source URLs, Context, per-item findings (price, condition, specs, verdict), Final Recommendation
- `README.md` index must be updated in the same commit as any new research file

## Rule #4 — Source Referencing
Secondary sources that change or inform verdicts go in an `## Alternative Context` section.
Include: author name, publication date, and a brief summary of why this source matters.
