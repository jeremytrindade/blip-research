# Handoff — Jetblip Node Upgrade Research

> Criado em 2026-05-17. Para continuar esta pesquisa numa nova sessao.
> **Instrucao para o proximo agente:** Le os ficheiros de regras listados na secao "Repos de Contexto" antes de qualquer acao.

---

## 1. Repos de Contexto — LER PRIMEIRO

Antes de qualquer pesquisa ou acao, clona ou le os seguintes repos:

```bash
# sovereign-lab — framework de versioning do hardware
git clone https://ghp_<PAT>@github.com/jeremytrindade/sovereign-lab.git /tmp/sovereign-lab

# blip-research — este repo, onde estao todos os ficheiros de pesquisa
git clone https://ghp_<PAT>@github.com/jeremytrindade/blip-research.git /tmp/blip-research
```

**Ficheiros criticos a ler:**
- `/tmp/sovereign-lab/README.md` — framework v0.x → v1.0 → v2.0 → v3.0, logica de upgrade
- `/tmp/sovereign-lab/HARDWARE.md` — decisoes de hardware verificadas, precos de abril 2026
- `/tmp/blip-research/hardware/jetblip-node-upgrade/20260517-lenovo-m720q-eu.md` — investigacao completa (394 linhas)
- `/tmp/blip-research/hardware/jetblip-node-upgrade/20260517-lenovo-m720q-eu.html` — versao HTML da investigacao

**PAT para git:** armazenado em `D:\credentials\credentials-v21\pc-20260517.txt`

---

## 2. Contexto do Projeto

### Setup Atual (v1.0)
- Hardware: **Raspberry Pi 5 4GB** a correr Ubuntu Server 24.04.4 LTS
- Stack: Docker + Portainer, automacoes domesticas, homelab
- OS alvo para qualquer nova maquina: **Ubuntu Server 24.04.4 LTS (Noble Numbat)** (Windows e irrelevante, a maquina e sempre limpa na chegada)

### Objetivo (v2.0)
- Substituir/complementar o RPi5 com um **Mini PC x86_64**
- Motivo: limitacoes ARM64 (imagens Docker sem suporte), CPU >70% em picos, necessidade de >6GB RAM
- Hardware alvo: **Lenovo ThinkCentre M720q Tiny** (sovereign-lab v2.0 de referencia)
  - PCIe riser 01AJ929 (NIC 2.5GbE ou quad-port)
  - Dual M.2 NVMe + 2.5" SATA
  - Max 64GB DDR4
  - i5-8500T (6c/6t Coffee Lake)
- O RPi5 nao e descartado — e reproposto para o proximo projeto v1.0

### Versioning sovereign-lab
```
v0.x = ideia/prototipo
v1.0 = RPi5 8GB a correr (atual: RPi5 4GB, estamos em v1.x)
v1.9 = RPi5 atingiu bottleneck
v2.0 = M720q Tiny em producao
v2.9 = M720q estavel, pronto para escalar
v3.0 = cluster / scale
```

---

## 3. Resumo da Investigacao (Sessoes 1, 2, 3)

### Sessao 1 — Pesquisa inicial (mercado PT + EU)
- Mercado PT: JANS.it (M720q i5-8400T 219EUR Grade A, melhor PT), PcComponentes, Tonitrus, WeBuy
- Amazon EU: M720q i5-9400T ~€299 (Amazon.de), HP G3 ~€165 (Amazon IT)
- Tiers definidos: Tier 1 = 6th-9th gen DDR4, Tier 2 = 4th gen DDR3, Tier 3 = AMD entry/Celeron (evitar)

### Sessao 2 — Fontes adicionais verificadas
- Back Market PT: M720q i5-8500T confirmado a €249.37
- Refurbed.pt: i3 €194.99, i5-8400T €240.99, i5-8500T €256.99, i5-9400T €264.99
- AfBshop.de / itsco.de: sem stock
- Amazon.de M720q: 5 configs, €289–384
- HP EliteDesk G3/G4/G5 Amazon IT: €165–299

### Sessao 3 — Lista 1 + Lista 2 (eBay.de ao vivo, comerciais apenas)

#### Lista 1 — Sweet Spots < €200 total (eBay.de, Gewerblich)

| # | Modelo | CPU | RAM/SSD | Total | Vendedor |
|---|--------|-----|---------|-------|----------|
| 1 | HP EliteDesk 800 G3 Mini 65W | i5-7500T 4c DDR4 | 8GB/256GB+WiFi+Win11 | €190.00 | mb_ekokompiuteriai LT (100%) |
| 2 | Lenovo M910q Tiny | i5-7500T 4c DDR4 | 8GB/256GB+WiFi/BT+Win11 | €184.80 | hells_dells (100%, 70k) |
| 3 | Lenovo M710q Tiny | i5-7th 4c DDR4 | 16GB/240GB+WiFi | €183.90 | dealo24_de (99.6%, 3yr) |
| 4 | HP EliteDesk 800 G4 Mini | i3-9300T 4c DDR4 | 8GB/512GB+Win11 | €179.45 | dealstunter NL (100%) |
| 5 | HP EliteDesk 800 G3 DM | i5-7500T 4c DDR4 | 8GB/240GB | €157.70 | technik-guenstiger (99.1%) |
| 6 | Lenovo M710q | i5-7400T 4c DDR4 | 8GB/256GB+Win11 | €148.99 | trade-serv (100%) |
| 7 | HP EliteDesk 800 G3 DM | i5-6500T 4c DDR4 | 8GB/256GB, 1yr | €134.00 | rn-tec (99.3%) |
| 8 | HP EliteDesk 800 G3 Mini | i5-6500T 4c DDR4 | 8GB/256GB+Win11 | €110.00 | pcline24 (99.9%, 219k) |

**Nota M720q:** Em abril 2026 a enter-leszno (eBay.de, PL comercial) vendia M720q i5-8500T/8GB/256GB/WiFi a €177–187 free EU ship. Em maio 2026, menor preco encontrado = €232.90 total. Monitorizar enter-leszno.

#### Lista 2 — Top 10 por Specs (sem limite financeiro)

| # | Modelo | CPU | Cores | iGPU | Preco eBay.de | SL Tier |
|---|--------|-----|-------|------|----------------|---------|
| 1 | Lenovo M90q Gen 2 | i7-11700T | 8c/16t | Intel Xe 32EU | ~€511 | v2.5 |
| 2 | HP EliteDesk 800 G8 Mini | i5-11500T | 6c/12t | Intel Xe 24EU | ~€434–474 | v2.5 |
| 3 | HP EliteDesk 800 G6 Mini | i5-10500T | 6c/12t | UHD 630 | €289–349 | v2.2 |
| 4 | Lenovo M920x Tiny | i7-9700T+RX460 | 8c/8t | UHD 630 + Radeon RX460 | €366–490 | v2.1+dGPU |
| 5 | HP EliteDesk 800 G4 Mini | i7-8700T | 6c/12t | UHD 630 | ~€299–315 | v2.1 |
| 6 | Lenovo M920q | i7-8700T | 6c/12t | UHD 630 + PCIe riser | €289–435 | v2.0+ |
| 7 | HP ProDesk 405 G8 Mini | Ryzen 5 Pro 5650GE | 6c/12t | Vega 7 448SP | ~€300–400 | v2.2 AMD |
| 8 | Lenovo M70q Gen 2 | i5-11400T | 6c/12t | UHD 730 32EU | €385–400 | v2.3 |
| 9 | HP EliteDesk 800 G5 Mini | i5-9500T | 6c/6t | UHD 630 | €215–268 | v2.0 HP |
| 10 | Lenovo ThinkCentre M720q | i5-8500T | 6c/6t | UHD 630 + PCIe riser | €232–294 | v2.0 ref. |

---

## 4. Sobre o OS — Ubuntu Server (Windows e irrelevante)

**A maquina sera sempre instalada com Ubuntu Server.** Windows 11 que venha pre-instalado e completamente irrelevante para este caso de uso. Nao pagar extra por configuracoes "sem OS" vs "com Win11" no mercado refurbished europeu — o diferencial de preco e normalmente zero ou negligenciavel.

Stack previsto para a v2.0:
```
Ubuntu Server 24.04.4 LTS
├── Docker + Portainer
├── Proxmox VE (opcional, se virtualizar varias VMs)
├── Ollama (iGPU via vaapi/OpenCL)
└── Servicos migrados do RPi5
```

---

## 5. Proximos Passos Sugeridos

- [ ] Monitorizar enter-leszno (eBay.de) para M720q i5-8500T < €200
- [ ] Verificar stock JANS.it M720q i5-8400T a €219 (Grade A, 24m garantia, Portugal)
- [ ] Decidir entre v2.0 exato (M720q ~€232–294) ou budget <€200 (M910q/M710q)
- [ ] Apos compra: Ubuntu Server 24.04.4 LTS + Docker + migrar stack do RPi5
- [ ] Reutilizar RPi5 4GB para proximo projeto v1.0 (sovereign-lab re-use principle)
- [ ] Eventual upgrade RAM para 16–32GB DDR4 SO-DIMM (M720q suporta ate 64GB)

---

## 6. Ficheiros do Repo

```
blip-research/
└── hardware/
    └── jetblip-node-upgrade/
        ├── 20260517-lenovo-m720q-eu.md     # investigacao completa (394 linhas)
        ├── 20260517-lenovo-m720q-eu.html   # versao HTML com design blip-rules (1594 linhas)
        └── HANDOFF.md                      # este ficheiro
```

---

## 7. Commits Relevantes

| Commit | Descricao |
|--------|-----------|
| `cdc7b46` | Criacao inicial da estrutura e README |
| `0546c41` | Sessao 2: Back Market PT, Refurbed, Amazon.de, HP EliteDesk |
| `0676487` | Sessao 3: Lista 1 (<200EUR) + Lista 2 (top 10 specs) |

---

*Handoff gerado automaticamente pelo agente Cowork em 2026-05-17.*
