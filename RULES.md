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

## Rule #7 — README Health (End of Session)
At the end of any session in any blip-* repo, verify the README is up to date before the final commit.

### Checklist
- [ ] **Session-start phrase present** — the "## Session Start" block must exist. If missing, add it (see README.md of blip-research for the canonical Portuguese phrase).
- [ ] **Structure section current** — the `## Structure` section must reflect the actual files and folders that now exist after this session.
- [ ] **Research index updated** — if a new `.md` or `.html` file was created, the index table in README.md must include it (with both `.md` and `.vNN.html` links if applicable).
- [ ] **No broken references** — any file paths, commands, or links mentioned in the README must point to things that actually exist.

### When this applies
This rule applies to **every session** that produces a commit, including:
- Any blip-research research session (after adding new findings)
- Any blip-aij or automation update session
- Any session that creates, moves, or renames files in any blip-* repo
- Any session triggered by the "use blip-research" phrase (Rule #6)

### Automated backstop
The `blip-repo-health` repo runs a daily 5am task that audits one repo per day and applies these same checks automatically. Rule #7 is the manual per-session equivalent — do not rely on the automated task as a replacement for doing it at session end.

## Rule #8 — Nunca Pedir Confirmação Para Agir
O agente nunca deve fazer perguntas do tipo "posso avançar?", "queres que eu faça X?", "devo continuar?" antes de executar trabalho.

Regra: anuncia o que vais fazer e faz imediatamente. O silêncio do utilizador é aprovação implícita.

**Porquê:** em workflows assíncronos, se o utilizador não responder a uma pergunta de confirmação, o trabalho fica bloqueado ou perde-se. Projetos inteiros podem ficar em suspenso porque o agente esperou por um "sim" que nunca chegou.

**Exceção:** ações destrutivas ou irreversíveis que não possam ser desfeitas (ex: apagar ficheiros permanentemente, enviar emails em massa) podem requerer confirmação explícita — mas mesmo aí, propõe a ação com detalhes concretos e avança salvo objeção.

**Aplicação:** esta regra sobrepõe-se a qualquer comportamento padrão de pedir aprovação antes de agir. É válida em todas as sessões blip-*.
