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

**NTFS mount warning:** The bash sandbox may see a stale NTFS mount at the workspace path. Always work from a fresh `/tmp/` clone — never trust `wc -l` or file edits on the mounted NTFS path. Git lock files on NTFS cannot be deleted from Linux (`rm` returns "Operation not permitted"). Solution: clone fresh in `/tmp/` where Linux has full control.

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

## Rule #5 — HTML Companion File (MANDATORY)
Every completed research file **must** have an HTML companion. This is not optional.

### Naming convention
```
YYYYMMDD-topic-slug.vNN.html
```
Where `NN` is a zero-padded sequential version number starting at `01`.

Examples:
```
20260517-lenovo-m720q-eu.v01.html   ← first render
20260517-lenovo-m720q-eu.v02.html   ← updated after new sessions
20260601-rpi5-accessories.v01.html  ← new research file
```

**Never overwrite an existing `.vNN.html` file.** Always increment `NN` and create a new file. This preserves a visual history of how the research evolved.

### HTML file requirements
The companion HTML must:
- Be fully self-contained (no external dependencies — no CDN, no external fonts, no external scripts)
- Follow the blip-research dark theme token set (see existing `20260517-lenovo-m720q-eu.v01.html` as reference)
- Include a dark/light toggle (inherit the `[data-theme]` attribute pattern)
- Display all research findings in a readable, structured layout (tables, verdict badges, tier labels)
- Include the research date, session number, and source URLs
- Show version number and generation timestamp in the page footer
- Be committed in the same git commit as the `.md` file it accompanies

### When to update the HTML
- After each new research session is added to the `.md`
- After any verdict or price correction
- Increment `NN` each time — never edit an existing versioned HTML

## Rule #6 — "Use blip-research" Trigger
When the user says "use blip-research" or "go search X in blip-research" or equivalent, the agent must:

1. **Start from HANDOFF.md** — read `hardware/jetblip-node-upgrade/HANDOFF.md` (or the relevant folder's HANDOFF) before doing anything else
2. **Read all files listed in Section 1 of HANDOFF.md** — no exceptions
3. **Follow all RULES.md rules** for the entire session, including:
   - Use Claude in Chrome for price verification (Rule #2)
   - Produce an HTML companion on session completion (Rule #5)
   - Commit via git CLI from a fresh `/tmp/` clone (Rule #1)
   - Update README.md index and HANDOFF.md in the same commit
4. **Verify the HTML version number** — check existing `.vNN.html` files in the folder and increment `NN` correctly
5. **Never assume the mounted NTFS path is current** — always clone fresh (Rule #1 NTFS warning)
