# blip-research

Personal research notes for home lab, hardware decisions, and tech evaluations.
Accessible from any PC via GitHub — no auth needed.

---

## Session Start — Copy one of these at the start of any Claude session

### Quick start (paste this first, always)
```
Lê o README.md e RULES.md de blip-research. Depois lê o HANDOFF.md da pasta relevante antes de fazeres qualquer coisa.
```

### Extended start (use when starting fresh or if files may be missing)
```
Estamos a trabalhar no repositório blip-research. Antes de começares:
1. Verifica se tens acesso à pasta D:\jetblip\github\blip-research\ — se não existir ou estiver desatualizada, clona com: git clone https://ghp_<PAT>@github.com/jeremytrindade/blip-research.git /tmp/blip-research
2. Lê README.md e RULES.md na raiz do repo.
3. Lê o HANDOFF.md da pasta do projeto em que vamos trabalhar (ex: hardware/jetblip-node-upgrade/HANDOFF.md).
4. Confirma que sabes responder às perguntas de verificação do HANDOFF antes de continuares.
5. Todo o trabalho desta sessão segue as RULES.md — incluindo HTML companion obrigatório e commit via git CLI.
O PAT está em: D:\credentials\credentials-v21\pc-20260517.txt
```

---

## Structure

- `hardware/` — SBC and hardware purchase research
  - `hardware/jetblip-node-upgrade/` — Pi 5 → x86 upgrade research (M720q, EliteDesk, Optiplex, N100)
- `infra/` — Cloud infrastructure changes and configuration records

## Research Index

| Date | Category | Topic | Files |
|------|----------|-------|-------|
| 2026-05-17 | Hardware | Lenovo M720q Tiny EU market: PT stores + Amazon IT/FR/ES verified prices, alternatives tier list, eBay.de sweet spots, component pricing | [.md](hardware/jetblip-node-upgrade/20260517-lenovo-m720q-eu.md) · [.v01.html](hardware/jetblip-node-upgrade/20260517-lenovo-m720q-eu.v01.html) |
| 2026-05-15 | Hardware | WeBuy PT: Banana Pi M5, Raspberry Pi 3x2, Orange Pi 3 LTS | [hardware/20260515-webuy-raspberry-pi.md](hardware/20260515-webuy-raspberry-pi.md) |
| 2026-05-15 | Infra | GCP OAuth client: added my.jetblip.com origins and redirect URIs | [infra/20260515-gcp-oauth-jetblip.md](infra/20260515-gcp-oauth-jetblip.md) |

## File Naming Conventions

```
YYYYMMDD-topic-slug.md          ← research notes (all sessions appended here)
YYYYMMDD-topic-slug.vNN.html    ← HTML companion (new file each version, NN = 01, 02…)
```

See `RULES.md` for full rules including HTML companion requirements (Rule #5) and the "use blip-research" trigger behaviour (Rule #6).
