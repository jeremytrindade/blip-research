# Handoff — Jetblip Node Upgrade Research

> Criado em 2026-05-17. Este ficheiro e o ponto de entrada para qualquer nova sessao.
> **REGRA #1:** Le TODOS os ficheiros listados na Secao 1 antes de fazer qualquer pesquisa ou acao.
> Esta conversa ficou com o contexto cheio (bugged). Uma nova sessao deve comecar aqui.

---

## 1. LER ESTES FICHEIROS PRIMEIRO — SEM EXCEPCOES

O utilizador tem dois repos clonados localmente. Le-os por esta ordem:

### 1.1 sovereign-lab (framework de regras e versioning)

Pasta local: `D:\jetblip\github\sovereign-lab\`

Le estes ficheiros nesta ordem:
1. `D:\jetblip\github\sovereign-lab\README.md` — framework de versioning v0.x → v1.0 → v2.0 → v3.0, logica de upgrade, principio de re-uso de hardware
2. `D:\jetblip\github\sovereign-lab\HARDWARE.md` — decisoes de hardware ja verificadas, precos de abril 2026, enter-leszno M720q €177–187

Se a pasta local nao estiver acessivel, clona com o PAT:
```bash
git clone https://ghp_<PAT>@github.com/jeremytrindade/sovereign-lab.git /tmp/sovereign-lab
```

### 1.2 blip-research (toda a investigacao de hardware)

Pasta local: `D:\jetblip\github\blip-research\`

Le estes ficheiros nesta ordem:
1. `D:\jetblip\github\blip-research\hardware\jetblip-node-upgrade\20260517-lenovo-m720q-eu.md` — investigacao completa, 3 sessoes, 394 linhas
2. `D:\jetblip\github\blip-research\hardware\jetblip-node-upgrade\HANDOFF.md` — este ficheiro

Se a pasta local nao estiver acessivel, clona:
```bash
git clone https://ghp_<PAT>@github.com/jeremytrindade/blip-research.git /tmp/blip-research
```

**PAT armazenado em:** `D:\credentials\credentials-v21\pc-20260517.txt`

### 1.3 Verificacao de leitura

Antes de continuar, confirma que sabes responder:
- Qual e o hardware sovereign-lab v2.0 de referencia? (R: Lenovo ThinkCentre M720q Tiny)
- Qual o preco do M720q no enter-leszno em abril 2026? (R: €177–187, free EU ship)
- Qual o menor preco total encontrado em maio 2026? (R: €232.90, itreturn Austria)
- Qual o OS alvo? (R: Ubuntu Server 24.04.4 LTS, Windows e irrelevante)

Se nao conseguires responder, volta a ler os ficheiros acima.

---

## 2. Contexto do Projeto

### Setup Atual (v1.0)
- Hardware: **Raspberry Pi 5 4GB** a correr **Ubuntu Server 24.04.4 LTS (Noble Numbat)**
- Stack: Docker + Portainer, automacoes domesticas, homelab
- OS alvo para qualquer nova maquina: **Ubuntu Server 24.04.4 LTS** — Windows pre-instalado e 100% irrelevante, a maquina e sempre limpa na chegada. Nao pagar extra por Win11.

### Objetivo (v2.0)
- Adquirir um **Mini PC x86_64** para substituir/complementar o RPi5
- Motivo: limitacoes ARM64 (imagens Docker sem suporte), CPU >70% em picos, necessidade de >6GB RAM
- Hardware alvo: **Lenovo ThinkCentre M720q Tiny** (sovereign-lab v2.0 de referencia)
  - Slot PCIe riser 01AJ929 para NIC 2.5GbE ou quad-port
  - Dual M.2 NVMe + slot 2.5" SATA
  - Max 64GB DDR4 SO-DIMM
  - i5-8500T (6c/6t, Coffee Lake, 35W TDP)
- O RPi5 **nao e descartado** — e reproposto para o proximo projeto v1.0 (sovereign-lab re-use principle)

### Versioning sovereign-lab
```
v0.x  = ideia/prototipo
v1.0  = RPi5 a correr em producao
v1.x  = RPi5 estavel mas a mostrar limitacoes  <-- ESTADO ATUAL
v1.9  = RPi5 atingiu bottleneck critico
v2.0  = M720q Tiny em producao
v2.9  = M720q estavel, pronto para escalar
v3.0  = cluster / scale
```

---

## 3. Investigacao Concluida (Sessoes 1, 2, 3)

### Sessao 1 — Mercado PT + Amazon EU
- JANS.it: M720q i5-8400T **€219** Grade A, 24m garantia (melhor preco PT)
- PcComponentes.pt, Tonitrus, WeBuy verificados
- Amazon IT: HP EliteDesk G3 ~€165 (mais barato confirmado com envio PT)
- Amazon.de: M720q i5-9400T ~€299
- Tiers: **Tier 1** = 6th-9th gen DDR4 (recomendado), Tier 2 = 4th gen DDR3, Tier 3 = AMD entry/Celeron (evitar)

### Sessao 2 — Fontes adicionais EU
- Back Market PT: M720q i5-8500T confirmado **€249.37**
- Refurbed.pt: i3 €194.99 / i5-8400T €240.99 / i5-8500T €256.99 / i5-9400T €264.99
- AfBshop.de / itsco.de: sem stock
- Amazon.de M720q: 5 configs €289–384
- HP EliteDesk G3/G4/G5 Amazon IT: €165–299

### Sessao 3 — Lista 1 + Lista 2 (eBay.de ao vivo, comerciais)

#### Lista 1 — Sweet Spots < €200 total (eBay.de, Gewerblicher Verkaufer)

> Nota M720q (sovereign-lab v2.0 target): em abril 2026 enter-leszno (eBay.de, PL comercial) vendia
> M720q i5-8500T/8GB/256GB/WiFi a **€177–187 free EU ship** (HARDWARE.md). Em maio 2026 o menor
> preco encontrado e €232.90 total (€199 base + €33.90 envio Austria). O M720q saiu do budget <€200.
> Monitorizar enter-leszno regularmente.

| # | Modelo | CPU | RAM / SSD | **Total** | Vendedor eBay.de |
|---|--------|-----|-----------|-----------|------------------|
| 1 | HP EliteDesk 800 G3 Mini 65W | i5-7500T 4c DDR4 | 8GB / 256GB + WiFi + Win11 | **€190.00** | mb_ekokompiuteriai LT (100%, 6k) |
| 2 | Lenovo ThinkCentre M910q Tiny | i5-7500T 4c DDR4 | 8GB / 256GB + WiFi/BT + Win11 | **€184.80** | hells_dells (100%, 70k) |
| 3 | Lenovo ThinkCentre M710q Tiny | i5-7th 4c DDR4 | 16GB / 240GB + WiFi | **€183.90** | dealo24_de (99.6%, 5.2k, 3yr) |
| 4 | HP EliteDesk 800 G4 Mini | i3-9300T 4c DDR4 | 8GB / 512GB + Win11 | **€179.45** | dealstunter NL (100%, 6.5k) |
| 5 | HP EliteDesk 800 G3 DM | i5-7500T 4c DDR4 | 8GB / 240GB | **€157.70** | technik-guenstiger (99.1%, 15k) |
| 6 | Lenovo ThinkCentre M710q | i5-7400T 4c DDR4 | 8GB / 256GB + Win11 | **€148.99** | trade-serv (100%, 1.1k) |
| 7 | HP EliteDesk 800 G3 DM | i5-6500T 4c DDR4 | 8GB / 256GB, 1yr garantia | **€134.00** | rn-tec (99.3%, 6.6k) |
| 8 | HP EliteDesk 800 G3 Mini | i5-6500T 4c DDR4 | 8GB / 256GB + Win11 | **€110.00** | pcline24 (99.9%, 219k) |

#### Lista 2 — Top 10 por Specs (sem limite financeiro)

> Foco: Docker multi-arch, Proxmox, Ollama, 24/7 silent, sovereign-lab v2.x+.

| # | Modelo | CPU | Cores | iGPU (Ollama) | Preco eBay.de | SL Tier |
|---|--------|-----|-------|---------------|----------------|---------|
| 1 | Lenovo M90q Gen 2 Tiny | i7-11700T | 8c/16t | Intel Xe 32EU | ~€511 | v2.5 |
| 2 | HP EliteDesk 800 G8 Mini | i5-11500T | 6c/12t | Intel Xe 24EU | ~€434–474 | v2.5 |
| 3 | HP EliteDesk 800 G6 Mini | i5-10500T | 6c/12t | Intel UHD 630 | €289–349 | v2.2 |
| 4 | Lenovo M920x Tiny | i7-9700T + RX460 4GB | 8c/8t | UHD 630 + Radeon RX460 | €366–490 | v2.1+dGPU |
| 5 | HP EliteDesk 800 G4 Mini | i7-8700T | 6c/12t | Intel UHD 630 | ~€299–315 | v2.1 |
| 6 | Lenovo ThinkCentre M920q | i7-8700T | 6c/12t | UHD 630 + PCIe riser | €289–435 | v2.0+ |
| 7 | HP ProDesk 405 G8 Mini | Ryzen 5 Pro 5650GE | 6c/12t | Radeon Vega 7 448SP | ~€300–400 | v2.2 AMD |
| 8 | Lenovo ThinkCentre M70q Gen 2 | i5-11400T | 6c/12t | Intel UHD 730 32EU | €385–400 | v2.3 |
| 9 | HP EliteDesk 800 G5 Mini | i5-9500T | 6c/6t | Intel UHD 630 | €215–268 | v2.0 HP |
| 10 | Lenovo ThinkCentre M720q | i5-8500T | 6c/6t | UHD 630 + PCIe riser | €232–294 | **v2.0 ref.** |

---

## 4. Stack OS — Ubuntu Server 24.04.4 LTS

**Windows pre-instalado e 100% irrelevante.** A maquina e sempre limpa na chegada e instalada com:

```
Ubuntu Server 24.04.4 LTS (Noble Numbat)   <-- mesmo OS do RPi5 atual
├── Docker + Portainer
├── Proxmox VE (opcional, para VMs)
├── Ollama (iGPU via vaapi / OpenCL)
└── Stack migrado do RPi5
```

Nao pagar diferencial de preco por "com Win11" vs "sem OS" no mercado refurbished EU.

---

---
### Sessao 4 — Componentes de Upgrade + Back Market PT confirmado
- Back Market PT: M720q i5-8500T/8GB/256GB **€249,37** confirmado via Chrome (condicao Excelente, 24m garantia, envio gratis)
- eBay.es / eBay.de (M720q completo): IGNORAR — todos vendedores EUA, portes €70–140
- PCIe Riser 01AJ929 (eBay, China): **€14,88–17** envio gratis (biz360d, heretom-auction, hk-estreet)
- PCIe Riser 01AJ940 (eBay, China): **€9,32–11** envio gratis (91fairdeals, diyinbox-us, e-city2008)
- RAM upgrade correcao: estimativa €25–35 errada. Real: +1x16GB ~€110 (se slot livre), kit 2x16GB ~€213, 1x32GB ~€247

---

## 5. Proximos Passos

- [ ] Monitorizar **enter-leszno** (eBay.de) para M720q i5-8500T < €200 com envio gratis EU
- [ ] Verificar stock **JANS.it** M720q i5-8400T €219 (Grade A, 24m garantia, PT)
- [ ] Verificar stock **Back Market PT** M720q i5-8500T (atualmente €249,37 / 8GB / Excelente)
- [ ] Decidir: v2.0 exato (M720q ~€232–294) ou budget <€200 (M910q/M710q da Lista 1)
- [ ] Apos compra: abrir M720q e verificar config RAM (1x16GB slot livre vs 2x8GB) antes de comprar upgrade
- [ ] RAM upgrade: +1x16GB ~€110 (se slot livre) ou kit 2x16GB ~€213 (se 2x8GB) — Amazon.es
- [ ] Riser PCIe: 01AJ929 a ~€15 (biz360d/heretom-auction eBay.es, China, 2–4 semanas)
- [ ] Apos compra: instalar Ubuntu Server 24.04.4 LTS + migrar stack do RPi5
- [ ] Reutilizar RPi5 4GB no proximo projeto v1.0 (re-use principle sovereign-lab)

---

## 6. Estrutura do Repo blip-research

```
D:\jetblip\github\blip-research\
└── hardware\
    └── jetblip-node-upgrade\
        ├── 20260517-lenovo-m720q-eu.md     <- investigacao completa (394 linhas)
        ├── 20260517-lenovo-m720q-eu.html   <- versao HTML com design (1594 linhas)
        └── HANDOFF.md                      <- este ficheiro
```

---

## 7. Historial de Commits

| Commit | Descricao |
|--------|-----------|
| `cdc7b46` | Criacao inicial da estrutura e README |
| `0546c41` | Sessao 2: Back Market PT, Refurbed, Amazon.de, HP EliteDesk |
| `0676487` | Sessao 3: Lista 1 (<200EUR) + Lista 2 (top 10 specs) |
| `60af676` | Adicao do HANDOFF.md |
| `76b03fe` | OS especificado: Ubuntu 24.04.4 LTS |
| `(atual)` | Sessao 4: Back Market PT confirmado, riser PCIe precos, RAM precos corretos |

---

## 8. Problemas Conhecidos (desta sessao bugged)

Para o proximo agente evitar os mesmos problemas:

- **NTFS mount stale:** O bash sandbox ve o NTFS mount (`/sessions/.../mnt/jetblip/`) com conteudo desatualizado. Sempre trabalhar numa clone fresca em `/tmp/` e fazer push para o GitHub. Nunca confiar no `wc -l` do path NTFS.
- **Git lock files NTFS:** `rm -f .git/HEAD.lock` falha com "Operation not permitted" em NTFS a partir do Linux. Solucao: clone fresca em `/tmp/` onde o Linux tem controlo total.
- **Remote URL placeholder:** O `.git/config` local pode ter `<SEU_PAT>` literal. Usar sempre clone em `/tmp/` com PAT no URL.
- **eBay filtro comercial:** `LH_SellerType=1` = privados (errado), `LH_SellerType=2` = comerciais (correto).
- **web_fetch provenance:** A ferramenta `web_fetch` so aceita URLs que apareceram em resultados anteriores. Usar `WebSearch` primeiro para obter URLs validos.

---

*Handoff gerado em 2026-05-17. Proxima sessao: ler Secao 1 antes de qualquer acao.*
