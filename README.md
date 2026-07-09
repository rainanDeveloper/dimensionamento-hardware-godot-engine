# Dimensionamento de Hardware para o Godot Engine

**Disciplina:** Introdução à Computação
**Autor:** Rainan Miranda de Jesus
**Software-alvo:** [Godot Engine](https://godotengine.org/) — motor de jogos *open-source*

> **Restrição do professor:** o **processador** não pode ter sido lançado antes de 2021.
> A regra vale **apenas para a CPU** — os demais componentes não têm restrição de data.
> Essa regra foi respeitada desde o início do processo de escolha — não ajustada depois.

---

## Sumário

- [Metodologia](#metodologia)
- [Requisitos oficiais do Godot](#requisitos-oficiais-do-godot)
- [Componentes escolhidos](#componentes-escolhidos)
  - [CPU (Processador)](#cpu-processador)
  - [Placa-mãe](#placa-mãe)
  - [Memória RAM](#memória-ram)
  - [GPU (Placa de vídeo)](#gpu-placa-de-vídeo)
  - [Armazenamento](#armazenamento)
  - [Fonte de alimentação](#fonte-de-alimentação)
  - [Cooler do processador](#cooler-do-processador)
  - [Gabinete](#gabinete)
  - [Sistema operacional](#sistema-operacional)
  - [Periféricos](#periféricos)
- [Resumo final da configuração](#resumo-final-da-configuração)
- [Perguntas prováveis e respostas rápidas](#perguntas-prováveis-e-respostas-rápidas)
- [Fontes](#fontes)

---

## Metodologia

O dimensionamento seguiu 5 passos, aplicados a cada componente:

1. **Requisitos** — levantar as especificações oficiais do Godot.
2. **Comparação técnica** — analisar arquitetura e especificações das opções.
3. **Benchmark** — comparar desempenho real (quando aplicável).
4. **Preço** — levantar o custo de cada opção.
5. **Decisão** — escolher o melhor custo-benefício.

O foco do trabalho foi **atender bem os requisitos com o menor custo**, e não maximizar poder de processamento. Cada escolha tem uma fonte por trás — nada foi "chutado".

---

## Requisitos oficiais do Godot

Fonte oficial: [Godot Engine — System Requirements](https://docs.godotengine.org/en/stable/about/system_requirements.html)

Requisitos **recomendados** para o editor nativo (PC desktop/laptop):

| Componente | Requisito |
|---|---|
| CPU | x86_64 com suporte a SSE4.2, 4 núcleos físicos ou mais, ou CPU ARMv8 (ex.: Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite) |
| GPU | Placa dedicada com suporte total a **Vulkan 1.2** (ex.: NVIDIA GTX 1050 / Pascal, AMD RX 460 / GCN 4.0); ou OpenGL 4.6 no renderizador de compatibilidade |
| RAM | 8 GB (editor nativo) / 12 GB (editor web) |
| Armazenamento | 1,5 GB (executável, arquivos de projeto, *export templates* e cache) |
| Sistema operacional | Windows 10, macOS 10.15, distribuição Linux lançada após 2020 |

**Dois números ancoram todas as escolhas seguintes:**

- **8 GB de RAM** (mínimo do editor nativo).
- **Vulkan 1.2** na GPU (suporte total exigido).

---

## Componentes escolhidos

### CPU (Processador)

**Escolhido: AMD Ryzen 5 5600**

Comparação: **AMD Ryzen 5 5600 vs. Intel Core i5-11600K**
Fonte do comparativo: [Technical City — Core i5-11600K vs Ryzen 5 5600](https://technical.city/en/cpu/Core-i5-11600K-vs-Ryzen-5-5600)

| | Ryzen 5 5600 | i5-11600K |
|---|---|---|
| Núcleos / Threads | 6 / 12 | 6 / 12 |
| Cache L2 (por núcleo) | **512 KB** | 256 KB |
| Cache L3 | **32 MB** | 12 MB |
| Litografia | **7 nm** | 14 nm |
| TDP (consumo) | **65 W** | 125 W |
| Score agregado (Technical City) | **12,58** | 11,40 |
| Preço (Amazon BR) | **R$ 974,66** | R$ 1.944,27 |

**Justificativas da escolha:**

- **Desempenho agregado ~10,4% superior** ao do i5-11600K, segundo o score agregado da Technical City (que reflete principalmente o Passmark).
- **Caches maiores** (L2 de 512 KB por núcleo vs. 256 KB; L3 de 32 MB vs. 12 MB) reduzem a frequência de acessos à RAM (mais lenta), melhorando cargas que reutilizam os mesmos dados — como compilar projeto, rodar o editor e exportar *builds*.
- **Litografia de 7 nm vs. 14 nm** → mais transistores na mesma área, maior eficiência energética e menor geração de calor.
- **Consumo menor** (65 W de TDP vs. 125 W) → mais fácil de refrigerar e adequado a uma estação que roda cargas de desenvolvimento por longos períodos.
- **Custo quase pela metade** (~R$ 975 vs. ~R$ 1.944 — ~99% mais barato).
- Atende com folga o requisito do Godot (4 núcleos x86_64 com SSE4.2) e respeita a regra de "nada antes de 2021" (lançado em 2022).

**Nuance honesta (fortalece a escolha):** o Ryzen **não** vence em tudo. Nos testes individuais da mesma página:

- GeekBench 5 *single-core*: o **Intel vence por ~7,6%**.
- GeekBench 5 *multi-core*: **empate técnico** (Ryzen +0,4%).
- A vantagem do Ryzen aparece no **agregado** e no uso **multi-thread**, que é o cenário mais relevante para compilar e exportar projetos no Godot.

Preços de referência (Amazon BR — reconferir próximo à data): [Ryzen 5 5600](https://www.amazon.com.br/s?k=AMD+Ryzen+5+5600) · [i5-11600K](https://www.amazon.com.br/s?k=Intel+Core+i5-11600k).

---

### Placa-mãe

**Escolhida: Gigabyte B550M AORUS ELITE** (Socket AM4, chipset B550)

Cadeia lógica de decisão: **processador define o socket → socket define os chipsets compatíveis → chipset define o modelo.**

- **Socket AM4** — exigido pelo Ryzen 5 5600 (ver [Technical City](https://technical.city/en/cpu/Core-i5-11600K-vs-Ryzen-5-5600), campo *Socket AM4*).
- **Chipset B550** — dentre os compatíveis com AM4 ([AMD — Chipsets AM4](https://www.amd.com/en/products/processors/chipsets/am4.html)):
  - Tem **PCIe 4.0**, aproveitando a banda do SSD NVMe e da GPU.
  - Suporta **overclock**.
  - É **amplamente disponível** e com boa variedade de modelos.
- **Modelo Gigabyte B550M AORUS ELITE** — bom preço dentre as opções B550 / AM4.
- **Coerência a verificar:** confirmar no manual da placa se o slot M.2 principal é PCIe 4.0 (Gen4) — em muitas B550, o segundo slot M.2, se existir, é Gen3 ou SATA.

**Por que não a A520 (mais barata)?** A A520 **não** oferece PCIe 4.0 nem overclock — perderíamos a vantagem de banda do SSD NVMe e da comunicação com a GPU.

---

### Memória RAM

**Escolhida: 2 × Kingston Fury Beast DDR4 8 GB 3200 MHz (16 GB em dual channel)**

- Requisito do Godot: **8 GB** (editor nativo) / 12 GB (editor web) — atendido com folga.
- **16 GB no total** — com dois pentes de 8 GB alcança-se 16 GB facilmente, dobrando o requisito mínimo.
- **Dual channel** (2×8 GB em vez de 1×16 GB) dobra a banda de comunicação com o processador — detalhe técnico acima do básico.
- **3200 MHz é a frequência nativa suportada pelo Ryzen 5 5600** (ver especificação na [Technical City](https://technical.city/en/cpu/Core-i5-11600K-vs-Ryzen-5-5600)) → o kit roda na frequência nativa, **sem precisar de XMP/overclock de memória**.
- Escolha do modelo pelo bom preço entre as opções.

---

### GPU (Placa de vídeo)

**Escolhida: NVIDIA GeForce GTX 1050** (arquitetura Pascal, 2016)

- **Suporte total a Vulkan 1.2** — requisito exigido pelo Godot.
- É **literalmente o exemplo oficial** da [documentação do Godot](https://docs.godotengine.org/en/stable/about/system_requirements.html) para a GPU mínima recomendada.
- Atende os renderizadores **Forward** e **Mobile** do motor.
- A GTX 1050 é de 2016, mas isso **não é problema**: a restrição de data de 2021 vale **apenas para o processador**. A escolha ainda é tecnicamente sólida por ser o exemplo oficial do Godot.

---

### Armazenamento

**Escolhido: SSD NVMe M.2 500 GB** (~R$ 500–600)

- Requisito real do Godot é baixíssimo: **1,5 GB**.
- **500 GB** é escolha de **conforto e futuro**, não de necessidade: comporta sistema operacional, ferramentas de desenvolvimento, arquivos de projeto, *builds* exportadas e expansão futura.
- **NVMe (e não SATA)** foi escolhido pela **velocidade** — reduz diretamente o tempo de carregamento do editor e de exportação de *builds*, algo que se repete o tempo todo durante o desenvolvimento.
- Aproveita o **PCIe 4.0** da placa-mãe B550.

---

### Fonte de alimentação

**Escolhida: Fonte de 500 W** (~R$ 200,00), preferencialmente com certificação **80+ (mínimo Bronze)**

Consumo estimado por componente:

| Componente | Consumo aprox. |
|---|---|
| CPU (Ryzen 5 5600) | ~90 W (carga máxima) |
| GPU (GTX 1050) | ~75 W |
| Placa-mãe | ~40 W |
| Memória + SSD | ~10 W |
| **Total estimado** | **~215 W** |

**Justificativas:**

- **500 W é mais que o dobro** do consumo real estimado (~215 W) → margem para estabilidade, picos de consumo, envelhecimento dos componentes e upgrades futuros — prática padrão em dimensionamento de fonte.
- **Certificação 80+ (mínimo Bronze)** — critério de eficiência energética valorizado em dimensionamento; reduz desperdício e aquecimento.

---

### Cooler do processador

**Escolhido: Cooler *stock* AMD Wraith Stealth (incluso com o Ryzen 5 5600)**

- O Ryzen 5 5600 **já acompanha** o cooler Wraith Stealth de fábrica — **custo adicional zero**.
- É suficiente para o TDP de **65 W** do processador em cargas de desenvolvimento, sem overclock agressivo.
- Um cooler *aftermarket* só seria necessário para overclock pesado ou operação silenciosa — fora do escopo deste dimensionamento.

---

### Gabinete

**Escolhido: Gabinete Mini Tower / Micro-ATX com boa ventilação** (~R$ 200–300)

- **Compatível com placa-mãe Micro-ATX (mATX)** — formato da Gigabyte B550M AORUS ELITE.
- **Espaço para a GPU** — a GTX 1050 é curta, cabe em praticamente qualquer gabinete.
- **Fluxo de ar adequado** (com ao menos um fan frontal e um traseiro) — importante para dissipar o calor em uso prolongado de desenvolvimento.
- **Baias/suportes** para SSD M.2 (na placa-mãe) e futura expansão de armazenamento.
- Escolha por **custo-benefício**, priorizando ventilação e compatibilidade de formato em vez de estética.

---

### Sistema operacional

**Escolhido: Linux (distribuição lançada após 2020) ou Windows 10/11**

- O Godot **suporta oficialmente** Windows 10, macOS 10.15 e Linux (distribuição pós-2020) — ver [requisitos oficiais](https://docs.godotengine.org/en/stable/about/system_requirements.html).
- **Linux** é uma opção **sem custo de licença**, coerente com um projeto centrado em ferramenta *open-source* (o próprio Godot é open-source).
- Alternativa: **Windows 10/11** caso a compatibilidade com outras ferramentas do fluxo de trabalho seja necessária.

---

### Periféricos

Itens necessários para operar a máquina (não cobertos pelos requisitos do Godot, mas indispensáveis na prática):

- **Monitor Full HD (1080p), ~23"–24"** — resolução suficiente para o editor do Godot com bom espaço de trabalho e custo acessível (~R$ 700–900).
- **Teclado + mouse** — periféricos básicos com fio, custo-benefício (~R$ 100–200 o conjunto). Um mouse com boa precisão ajuda no posicionamento de nós e edição de cenas.
- **(Opcional) Headset/áudio** — útil para desenvolvimento e teste de áudio nos jogos.

> Os periféricos foram dimensionados pelo **custo-benefício**, sem exigências especiais além de conforto e confiabilidade — o Godot não impõe requisitos específicos de entrada/saída.

---

## Resumo final da configuração

| Componente | Escolha | Preço (referência) |
|---|---|---|
| CPU | AMD Ryzen 5 5600 | R$ 974,66 |
| Placa-mãe | Gigabyte B550M AORUS ELITE | a confirmar |
| Memória | Kingston Fury Beast 2×8 GB 3200 MHz | a confirmar |
| GPU | NVIDIA GeForce GTX 1050 | a confirmar |
| Armazenamento | SSD NVMe M.2 500 GB | R$ 500–600 |
| Fonte | 500 W (80+ Bronze) | ~R$ 200,00 |
| Cooler | AMD Wraith Stealth (incluso) | R$ 0,00 |
| Gabinete | Mini Tower Micro-ATX ventilado | R$ 200–300 |
| Sistema operacional | Linux (pós-2020) ou Windows 10/11 | R$ 0,00 (Linux) |
| Monitor | Full HD 23"–24" | R$ 700–900 |
| Teclado + mouse | Conjunto com fio | R$ 100–200 |

> ⚠️ Valores de placa-mãe, memória e GPU ainda em levantamento. Somando as estimativas, o **custo total** da máquina (sem periféricos) gira em torno de **R$ 2.500–3.000**, e com periféricos em torno de **R$ 3.300–4.100** — a reconferir próximo à data.

---

## Perguntas prováveis e respostas rápidas

- **"Por que não um processador Intel mais recente (12ª/13ª geração)?"**
  Poderia ter sido considerado, mas dentro do custo-benefício levantado, o Ryzen 5 5600 já atende com folga os requisitos do Godot por um preço bem menor. O trabalho focou em **atender bem o requisito com o menor custo**, não em maximizar poder de processamento.

- **"O Ryzen é melhor em tudo?"**
  Não — em *single-core* o Intel vence (~7,6%); a vantagem do Ryzen aparece no **agregado** e no **multi-core**, que é o cenário mais relevante para compilar e exportar projetos.

- **"Por que GTX 1050 se é uma GPU de 2016?"**
  É o **exemplo oficial** da documentação do Godot para a GPU mínima recomendada, com suporte total a Vulkan 1.2. A restrição de data de 2021 vale **apenas para o processador**, então a GPU de 2016 é permitida.

- **"Por que 500 W se o consumo é só ~215 W?"**
  Margem de segurança para estabilidade, picos de consumo, envelhecimento de componentes e upgrades futuros — prática padrão em dimensionamento de fonte.

- **"Por que não a placa-mãe A520, mais barata?"**
  A A520 não oferece PCIe 4.0 nem overclock — perderíamos a banda do SSD NVMe e da GPU.

---

## Fontes

- [Godot Engine — System Requirements (documentação oficial)](https://docs.godotengine.org/en/stable/about/system_requirements.html)
- [Technical City — Core i5-11600K vs Ryzen 5 5600 (comparativo de CPU)](https://technical.city/en/cpu/Core-i5-11600K-vs-Ryzen-5-5600)
- [AMD — Chipsets AM4 (página oficial)](https://www.amd.com/en/products/processors/chipsets/am4.html)
- Amazon BR — preços de referência dos componentes:
  [Ryzen 5 5600](https://www.amazon.com.br/s?k=AMD+Ryzen+5+5600) ·
  [Intel Core i5-11600K](https://www.amazon.com.br/s?k=Intel+Core+i5-11600k)
