# blip-research

Personal research notes for home lab, hardware decisions, and tech evaluations.
Accessible from any PC via GitHub — no auth needed.

---

## Session Start — Copy one of these at the start of any Claude session

### Versão curta
```
Lê o `README.md` e `RULES.md` de `blip-research`. Com base na tarefa pedida pelo utilizador, identifica a subpasta relevante (`hardware/`, `infra/`, etc.) e lê o `HANDOFF.md` dessa pasta se existir. Mantém as regras do `RULES.md` ativas durante toda a sessão.
```

### Versão extendida
```
Antes de qualquer trabalho em `blip-research`, segue esta sequência:

1. Verificar pasta — confirma se `blip-research` está disponível no workspace. Se não estiver, pede o GitHub PAT ao utilizador e faz git clone com esse PAT. Se já existir, faz git pull. Se git pull falhar por restrição de proxy/rede, não avances com ficheiros locais — busca imediatamente README.md e RULES.md em raw.githubusercontent.com/jeremytrindade/blip-research/main/ via browser Chrome e usa esses como versão autoritativa.
2. Ler por ordem — README.md primeiro (estrutura e índice), depois RULES.md (regras operacionais para a sessão).
3. Identificar subpasta — com base na tarefa descrita pelo utilizador, determina a subpasta relevante (hardware/, infra/, ou outra). Se não for óbvio, pergunta ao utilizador antes de avançar.
4. Ler HANDOFF.md — se existir na subpasta identificada, lê-o e confirma as perguntas de verificação que contiver antes de avançar. Se não existir, continua sem bloquear.
5. Regras ativas — mantém as regras do RULES.md em memória durante toda a sessão. Antes de avançar, confirma que encontraste pelo menos 8 regras e que a Regra #5 existe — se não, para imediatamente e busca os ficheiros via browser Chrome porque estás a trabalhar com dados desatualizados.

Comportamentos obrigatórios independentes do RULES.md (aplicam-se sempre, mesmo que os ficheiros não carreguem):
- Nunca perguntar "posso avançar?" ou "devo continuar?" — anuncia o que vais fazer e faz imediatamente. Silêncio do utilizador = aprovação.
- Se qualquer ficheiro falhar a carregar, usa sempre o browser Chrome como fallback antes de bloquear ou pedir ajuda.
- Nunca avançar com dados que não puderam ser confirmados como atuais.
```

### Alternativa com paths diretas (mais robusta)
```
Lê `/github/blip-research/README.md` e `/github/blip-research/RULES.md`. Se houver `HANDOFF.md` na subpasta da tarefa atual, lê-o também. Mantém as regras do `RULES.md` ativas durante a sessão. Antes de avançar, confirma que encontraste pelo menos 8 regras e que a Regra #5 existe — se não, para imediatamente porque estás a trabalhar com dados desatualizados. Comportamentos sempre ativos: nunca pedir confirmação antes de agir (silêncio = aprovação); usar browser Chrome como fallback se qualquer ficheiro falhar.
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
YYYYMMDD-topic-slug.md          + research notes (all sessions appended here)
YYYYMMDD-topic-slug.vNN.html    + HTML companion (new file each version, NN = 01, 02...)
```
