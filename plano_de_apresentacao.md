# Plano de Apresentação — Dimensionamento de Hardware (Godot Engine)

Este plano é só seu, para guiar a fala. O slide (PDF) é o que a turma vai ver. Tempo total sugerido: 8–10 minutos + perguntas.

---

## Antes de tudo: correções e melhorias que valem a pena

Conferi seus links (Technical City, AMD, docs do Godot). A boa notícia: **quase tudo está certo**, incluindo o ponto que você tinha dúvida.

1. **Cache L2 — está correto.** O Technical City confirma: 512 KB por núcleo no Ryzen 5 5600 contra 256 KB por núcleo no i5-11600K. Pode afirmar isso com confiança, inclusive se o professor perguntar diretamente — a fonte sustenta o número exato.

2. **Os 10,4% de desempenho — corretos, mas com uma nuance boa de saber.** Esse número vem do *score agregado* do Technical City (que reflete principalmente o Passmark, onde a diferença também é +10,4%). Só que, olhando os testes individuais listados na mesma página:
   - GeekBench 5 *single-core*: o **Intel vence por 7,6%**.
   - GeekBench 5 *multi-core*: **empate técnico** (Ryzen +0,4%).
   
   Ou seja, a vantagem do Ryzen é real no agregado (que pesa mais o Passmark, um benchmark multi-carga), mas não é uniforme em todos os testes. Isso não muda sua escolha — ela continua sendo a mais barata, mais eficiente e com o melhor agregado — mas é uma ótima resposta pronta se alguém perguntar "o Ryzen é melhor em tudo?". Seu argumento fica mais forte, não mais fraco, se você já citar isso proativamente.

3. **Formatação de preço.** No seu texto está "BRL 1.944.27" — no padrão brasileiro isso deveria ser **R$ 1.944,27** (vírgula decimal, ponto de milhar). Só ajustar a grafia; o valor em si eu não consegui reverificar ao vivo (a página de busca da Amazon não me deixa confirmar preço exato agora), então é bom só reconferir o valor perto da data da apresentação.

4. **GPU (GTX 1050) e a regra "nada antes de 2021".** Você escreveu que a regra do professor era sobre o **processador**. A GTX 1050 é de 2016. Isso é perfeitamente defensável (é literalmente o exemplo oficial do Godot para GPU), mas **vale confirmar com o professor antes** se a restrição de data era só para CPU ou para todos os componentes — para não ser pega de surpresa na hora. Deixei uma nota disso no próprio slide, como lembrete visual.

5. **Placa-mãe x SSD NVMe.** Um ponto fino que fortalece a apresentação: confirme no manual da Gigabyte B550M AORUS ELITE se o slot M.2 principal é PCIe 4.0 (Gen4) — em muitas B550 o segundo slot M.2, se existir, é Gen3 ou até SATA. Não muda a escolha, mas mostra que você pensou na coerência entre os componentes.

6. **Ponto de coerência que vale destacar (novo, a seu favor):** a especificação do Ryzen 5 5600 no Technical City lista memória suportada como **DDR4-3200** — exatamente a frequência do seu kit Kingston Fury Beast escolhido. Isso é uma boa frase de fechamento para a seção de memória: "o kit escolhido roda na frequência nativa suportada pelo processador, sem precisar de XMP/overclock de memória".

7. **Fonte de alimentação.** Sua conta de consumo (~215 W) e a escolha de 500 W estão bem justificadas (folga de mais do dobro). Só uma sugestão de reforço: mencione a certificação **80+ (mínimo Bronze)** da fonte que você comprar — é um critério de eficiência energética que qualquer professor de hardware valoriza ver citado.

8. **Preços faltando.** No seu documento só CPU, SSD e fonte têm preço registrado. Se possível, complete os valores de placa-mãe, memória e GPU antes do dia — o slide de fechamento já está com um aviso visual disso, mas seria bom já chegar com os números.

Fora esses pontos, a lógica de escolha (specs → benchmark → preço → decisão) está sólida e bem documentada com fontes. Isso é o que mais impressiona num trabalho de dimensionamento: você não "chutou" nada, cada escolha tem uma fonte por trás.

---

## Roteiro slide a slide

### Slide 1 — Capa
Fale seu nome, a disciplina e que o software escolhido foi o Godot Engine. Frase de abertura sugerida: *"Escolhi dimensionar uma máquina para desenvolvimento de jogos com o Godot Engine, um motor open-source, e vou mostrar como cheguei em cada componente a partir dos requisitos oficiais e de comparações técnicas."*

### Slide 2 — Objetivo e metodologia
Deixe claro logo de cara a restrição do professor (nada antes de 2021) — isso mostra que você respeitou a regra desde o início do processo, não que "ajeitou" depois. Explique rapidamente os 5 passos da metodologia como um roteiro do que vem a seguir.

### Slide 3 — Requisitos oficiais do Godot
Não precisa ler a tabela inteira em voz alta — aponte os dois números mais importantes: **8 GB de RAM** e **Vulkan 1.2** na GPU, porque são os que mais pesam na escolha dos componentes depois. Isso ancora tudo que vem a seguir.

### Slide 4 — CPU: comparação técnica
Aqui é o coração do trabalho. Destaque:
- Mesmo número de núcleos/threads — a diferença está em cache, litografia e consumo.
- **Cache L2 e L3 maiores no Ryzen** → menos acesso à memória RAM, mais performance em cargas repetitivas.
- **7nm vs 14nm** → mais eficiência energética, menos calor.
Se quiser, comente rapidamente por que isso importa para "cargas de desenvolvimento" (compilar projeto, rodar o editor, exportar builds por longos períodos).

### Slide 5 — CPU: desempenho e preço
Mostre o gráfico de barras e diga o número: Ryzen 12,58 vs Intel 11,40 (+10,4%). **Aqui é o momento de citar a nuance do item 2 acima**, proativamente: "vale dizer que em teste de núcleo único o Intel até leva vantagem, mas no agregado e no uso multi-thread, que é o que mais importa para compilar e rodar o motor, o Ryzen se sai melhor — e ainda custa a metade." Isso demonstra que você não escolheu olhando só um número favorável.

### Slide 6 — Placa-mãe
Explique a cadeia lógica: processador define o socket (AM4) → chipset precisa suportar a linha 5000 (B550 suporta) → modelo específico escolhido pelo custo-benefício. Se o professor perguntar "por que não A520 (mais barato)?", a resposta é: A520 não tem PCIe 4.0 nem overclock, então perde a vantagem de banda do SSD NVMe e da GPU.

### Slide 7 — Memória
Enfatize o "dual channel" (2x8GB em vez de 1x16GB) — é o tipo de detalhe técnico que mostra domínio do assunto além do básico. Feche com o ponto novo: a frequência 3200MHz bate exatamente com o que o processador suporta nativamente.

### Slide 8 — GPU
Cite que é literalmente o exemplo dado pela documentação oficial do Godot. Aqui, se você já resolveu a dúvida com o professor sobre a regra de data valer só para CPU, comente isso brevemente e com confiança; se não resolveu ainda, é melhor perguntar antes da apresentação para não ficar em dúvida ao vivo.

### Slide 9 — Armazenamento
Deixe claro que o requisito real é baixíssimo (1,5 GB) e que 500 GB é uma escolha de conforto e futuro, não de necessidade — e que NVMe (não SATA) foi escolhido pensando em tempo de carregamento do editor e de exportação de builds.

### Slide 10 — Fonte de alimentação
Mostre a conta simples (soma dos consumos) e a margem escolhida. Se já souber a certificação 80+ da fonte real que vai comprar, cite — reforça a escolha.

### Slide 11 — Resumo final
Feche retomando a tabela completa. Se ainda faltar preço de algum item, seja transparente: "os valores de placa-mãe, memória e GPU ainda estão em levantamento, mas o custo total gira em torno de X" (coloque uma estimativa se quiser).

### Slide 12 — Fontes
Só deixe a tela visível por alguns segundos e agradeça. Não precisa ler os links em voz alta.

---

## Perguntas prováveis e respostas rápidas

- **"Por que não um processador Intel mais recente (12ª/13ª geração)?"** → Poderia ter sido considerado, mas dentro do custo-benefício levantado, o Ryzen 5 5600 já atende com folga os requisitos do Godot por um preço bem menor; o trabalho focou em atender bem o requisito com o menor custo, não em maximizar poder de processamento.
- **"O Ryzen é melhor em tudo?"** → Não — em single-core o Intel vence; a vantagem do Ryzen aparece no agregado e no multi-core, que é o cenário mais relevante para compilar/exportar projetos.
- **"Por que GTX 1050 se é uma GPU de 2016?"** → É o exemplo oficial da documentação do Godot para a GPU mínima recomendada, com suporte total a Vulkan 1.2. (Confirme antes se essa data também precisa respeitar a regra do professor.)
- **"Por que 500W se o consumo é só 215W?"** → Margem de segurança para estabilidade, picos de consumo, envelhecimento de componentes e upgrades futuros — prática padrão em dimensionamento de fonte.
