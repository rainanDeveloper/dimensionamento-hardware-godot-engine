# Dimensionamento de Hardware para Godot Engine
### Introdução à Computação

---

## Slide 1 — Capa

**Dimensionamento de Hardware**
para desenvolvimento de jogos com o Godot Engine

*Introdução à Computação*
[Rainan Miranda de Jesus]

---

## Slide 2 — Objetivo e Metodologia

> **Restrição do professor:** nenhum componente selecionado pode ter sido lançado antes de 2021.

Essa regra foi respeitada desde o início do processo de escolha — não ajustada depois.

**Metodologia (5 passos):**

1. **Requisitos** — Levantar specs oficiais do Godot
2. **Comparação técnica** — Analisar arquitetura e specs
3. **Benchmark** — Comparar desempenho real
4. **Preço** — Levantar custo de cada opção
5. **Decisão** — Escolher o melhor custo-benefício

---

## Slide 3 — Requisitos Oficiais do Godot Engine

**Números-chave:**
- **8 GB** de RAM — editor nativo (mínimo)
- **Vulkan 1.2** — suporte total de GPU exigido

Esses dois números ancoram as escolhas de CPU, memória e GPU nos slides seguintes.

| Componente | Requisito mínimo (editor nativo) |
|---|---|
| CPU | x86_64 com SSE4.2, 4 núcleos físicos ou mais (ex.: Ryzen 5 1600, i5-6600K) |
| GPU | Dedicada, com suporte total a Vulkan 1.2 (ex.: GTX 1050, RX 460) |
| RAM | 8 GB (editor nativo) / 12 GB (editor web) |
| Armazenamento | 1,5 GB (executável, projeto, templates e cache) |
| Sistema operacional | Windows 10, macOS 10.15, Linux (distribuição lançada após 2020) |

*Fonte: documentação oficial do Godot Engine (system_requirements)*

---

## Slide 4 — CPU: Comparação Técnica

**AMD Ryzen 5 5600 vs. Intel Core i5-11600K**

| | Ryzen 5 5600 | i5-11600K |
|---|---|---|
| Núcleos / Threads | 6 / 12 | 6 / 12 |
| Cache L2 (por núcleo) | **512 KB** | 256 KB |
| Cache L3 | **32 MB** | 12 MB |
| Litografia | 7 nm | 14 nm |
| TDP (consumo) | 65 W | 125 W |

Mesmo número de núcleos/threads — a diferença está em cache, litografia e consumo: caches maiores reduzem acessos à RAM e o processo de 7nm melhora eficiência energética.

---

## Slide 5 — CPU: Desempenho e Preço

**Score agregado (Technical City):** Ryzen 5 5600 = 12,58 vs. i5-11600K = 11,40 (**+10,4%** Ryzen)

| | Ryzen 5 5600 | i5-11600K |
|---|---|---|
| Preço (Amazon BR) | **R$ 974,66** — escolhido | R$ 1.944,27 (+99% mais caro) |

*Preços de referência (Amazon BR) — reconferir próximo à data da apresentação.*

**O Ryzen é melhor em tudo? Não** — e essa nuance fortalece a escolha:
- GeekBench 5 single-core: **Intel vence por 7,6%**
- GeekBench 5 multi-core: **empate técnico** (Ryzen +0,4%)
- A vantagem do Ryzen aparece no agregado e no uso multi-thread — o cenário mais relevante para compilar e exportar projetos no Godot.

---

## Slide 6 — Placa-mãe

**Cadeia lógica de decisão:**

Processador (Ryzen 5 5600 define o socket) → Socket AM4 (requer chipset compatível) → Chipset B550 (PCIe 4.0 + overclock, ampla oferta) → **Modelo escolhido: Gigabyte B550M AORUS ELITE**

**Pergunta provável:** "Por que não usar a A520, mais barata?"
A A520 não oferece PCIe 4.0 nem overclock — perderíamos a vantagem de banda do SSD NVMe e da comunicação com a GPU. A B550 entrega esses recursos com bom custo-benefício.

---

## Slide 7 — Memória RAM

**Escolhido:** Kingston Fury Beast DDR4 — **2 x 8 GB** (dual channel, 16 GB no total) — **3200 MHz**

Frequência nativa suportada pelo Ryzen 5 5600.

**Por que 2x8GB em vez de 1x16GB?**
Configuração dual channel dobra a banda de comunicação com o processador — um detalhe que vai além do requisito básico do Godot (8 GB).

**Coerência entre componentes:**
O kit escolhido roda na frequência nativa suportada pelo processador, sem precisar de XMP/overclock de memória.

*Requisito Godot: 8 GB (editor nativo) / 12 GB (editor web) — atendido com folga.*

---

## Slide 8 — GPU

**NVIDIA GeForce GTX 1050** (Pascal — lançamento em 2016)

- Suporte total a Vulkan 1.2 — requisito exigido pelo Godot
- É literalmente o exemplo oficial da documentação do Godot para GPU mínima recomendada
- Atende renderer Forward e Mobile do motor

⚠️ **Lembrete para o dia da apresentação:** a regra de "nada antes de 2021" foi definida pelo professor para o processador. Confirmar antes se ela também se aplica à GPU — para responder com segurança se perguntado ao vivo.

---

## Slide 9 — Armazenamento

| Requisito do Godot | Escolhido |
|---|---|
| 1,5 GB (executável + projeto + templates + cache) | **500 GB NVMe** — SSD M.2, ~R$ 500–600 |

**Por que NVMe, e não SATA?**
O requisito real do Godot é baixíssimo (1,5 GB) — o espaço extra é conforto, não necessidade. Já a velocidade do NVMe reduz diretamente o tempo de carregamento do editor e de exportação de builds, algo que se repete o tempo todo durante o desenvolvimento.

---

## Slide 10 — Fonte de Alimentação

**Consumo estimado por componente:**
- CPU (Ryzen 5 5600): 90 W
- GPU (GTX 1050): 75 W
- Placa-mãe: 40 W
- Memória + SSD: 10 W

**Consumo total estimado: ~215 W**

**Fonte escolhida: 500 W** (~R$ 200,00) — mais que o dobro do consumo real, margem para estabilidade, picos e upgrades futuros.

**Reforço a citar:** mencionar a certificação **80+ (mínimo Bronze)** da fonte real comprada — critério de eficiência valorizado em dimensionamento.

---

## Slide 11 — Resumo Final da Configuração

| Componente | Escolha | Preço |
|---|---|---|
| CPU | AMD Ryzen 5 5600 | R$ 974,66 |
| Placa-mãe | Gigabyte B550M AORUS ELITE | a confirmar |
| Memória | Kingston Fury Beast 2x8GB 3200MHz | a confirmar |
| GPU | NVIDIA GeForce GTX 1050 | a confirmar |
| Armazenamento | SSD NVMe M.2 500GB | R$ 500–600 |
| Fonte | 500 W | R$ 200,00 |

⚠️ Valores de placa-mãe, memória e GPU ainda em levantamento — o custo total estimado gira em torno de **R$ 2.500–3.000**, a confirmar antes da apresentação.

---

## Slide 12 — Fontes

- Documentação oficial do Godot Engine — Requisitos do Sistema
- Technical City — Comparativo Core i5-11600K vs Ryzen 5 5600
- AMD — Página oficial de chipsets AM4
- Amazon BR — Preços de referência dos componentes

**Obrigado!**

---

## Perguntas prováveis e respostas rápidas

- **"Por que não um processador Intel mais recente (12ª/13ª geração)?"** → Poderia ter sido considerado, mas dentro do custo-benefício levantado, o Ryzen 5 5600 já atende com folga os requisitos do Godot por um preço bem menor; o trabalho focou em atender bem o requisito com o menor custo, não em maximizar poder de processamento.
- **"O Ryzen é melhor em tudo?"** → Não — em single-core o Intel vence; a vantagem do Ryzen aparece no agregado e no multi-core, que é o cenário mais relevante para compilar/exportar projetos.
- **"Por que GTX 1050 se é uma GPU de 2016?"** → É o exemplo oficial da documentação do Godot para a GPU mínima recomendada, com suporte total a Vulkan 1.2. (Confirmar antes se essa data também precisa respeitar a regra do professor.)
- **"Por que 500W se o consumo é só 215W?"** → Margem de segurança para estabilidade, picos de consumo, envelhecimento de componentes e upgrades futuros — prática padrão em dimensionamento de fonte.
