# Handoff — blip-research (raiz)

> Criado em 2026-05-17. Este ficheiro e o indice de topo do repositorio.
> Le este ficheiro primeiro. Depois navega para a subpasta da tarefa e le o `HANDOFF.md` correspondente.

---

## 1. Como usar este ficheiro

Este `HANDOFF.md` de raiz existe para garantir que qualquer sessao Claude encontra sempre um ponto de entrada, independentemente da tarefa. Funciona como indice: aponta para as subpastas ativas e os seus proprios `HANDOFF.md` mais detalhados.

**Sequencia obrigatoria:**
1. Le `RULES.md` (regras operacionais para toda a sessao)
2. Identifica a area da tarefa (ver Seccao 2 abaixo)
3. Navega para a subpasta e le o `HANDOFF.md` correspondente
4. Le os ficheiros listados na Seccao 1 desse HANDOFF antes de qualquer trabalho

---

## 2. Areas Ativas

### 2.1 Hardware (subpasta: `hardware/`)

Investigacao de hardware para home lab. Ver `hardware/HANDOFF.md` para indice completo.

**Projeto principal ativo:** Upgrade sovereign-lab v1.0 (RPi5) para v2.0 (Mini PC x86)
**HANDOFF detalhado:** `hardware/jetblip-node-upgrade/HANDOFF.md`

Estado atual: pesquisa de mercado EU concluida (4 sessoes), aguarda decisao de compra.

---

### 2.2 Infra (subpasta: `infra/`)

Registos de configuracao de infraestrutura cloud. Ver `infra/HANDOFF.md`.

Estado atual: sem projetos ativos em curso. Ultimo registo: GCP OAuth client 2026-05-15.

---

## 3. Indice de Ficheiros (todos os topicos)

| Data | Area | Ficheiro | Estado |
|------|------|----------|--------|
| 2026-05-17 | Hardware | `hardware/jetblip-node-upgrade/20260517-lenovo-m720q-eu.md` | Ativo (4 sessoes) |
| 2026-05-17 | Hardware | `hardware/jetblip-node-upgrade/20260517-lenovo-m720q-eu.v01.html` | HTML companion v01 |
| 2026-05-15 | Hardware | `hardware/20260515-webuy-raspberry-pi.md` | Concluido |
| 2026-05-15 | Infra | `infra/20260515-gcp-oauth-jetblip.md` | Concluido |

---

## 4. Regras Criticas (resumo rapido)

Regras completas em `RULES.md`. Resumo:
- Git: sempre CLI a partir de clone em `/tmp/`, nunca editor web, nunca NTFS mount
- Ficheiros: `YYYYMMDD-topic-slug.md` + `YYYYMMDD-topic-slug.vNN.html` (obrigatorio)
- Commits: README.md e HTML companion no mesmo commit que qualquer novo ficheiro `.md`
- Trigger "use blip-research": ler HANDOFF, seguir regras, produzir HTML companion no final

---

## 5. Estrutura de Pastas

```
blip-research/
+-- HANDOFF.md                          <- este ficheiro (indice de topo)
+-- README.md                           <- frases de inicio de sessao + indice publico
+-- RULES.md                            <- regras operacionais completas
+-- hardware/
|   +-- HANDOFF.md                      <- indice da area hardware
|   +-- 20260515-webuy-raspberry-pi.md
|   +-- jetblip-node-upgrade/
|       +-- HANDOFF.md                  <- HANDOFF detalhado do projeto ativo
|       +-- 20260517-lenovo-m720q-eu.md
|       +-- 20260517-lenovo-m720q-eu.v01.html
+-- infra/
    +-- HANDOFF.md                      <- indice da area infra
    +-- 20260515-gcp-oauth-jetblip.md
```

---

*Gerado em 2026-05-17. Atualizar este ficheiro sempre que uma nova area ou projeto for criado.*
