# Plano de Mentoria com Technical Advisor

## DEV Academy FY27 Capstone
**Accelerating Troubleshooting for Missing Prometheus Metrics in Azure Monitor**

## 1. Objetivo da mentoria

Usar o Technical Advisor como **mentor técnico e reviewer** durante os principais checkpoints do Capstone.

O papel do TA será:

- validar decisões técnicas;
- desafiar pressupostos;
- identificar gaps na investigação;
- revisar o fluxo de troubleshooting;
- validar os critérios utilizados para determinar um diagnóstico correto;
- revisar cenários experimentais;
- avaliar criticamente os resultados.

O ownership do projeto, pesquisa, desenvolvimento do MVP, experimentação e apresentação permanece com o participante.

---

# 2. Onde preciso da ajuda do TA

## Checkpoint 1 — Validar o problema

### Ajuda necessária

Validar se o problema escolhido representa uma dificuldade real e relevante:

> Support Engineers podem gastar tempo significativo isolando por que métricas Prometheus esperadas não estão disponíveis no Azure Monitor workspace.

### O TA deverá ajudar a avaliar

- se o problema está bem definido;
- se o escopo está suficientemente específico;
- se existem tipos de casos importantes que ficaram fora da definição;
- se os failure domains iniciais fazem sentido;
- se o projeto está tentando resolver um problema grande demais.

### Resultado esperado

**Problem statement tecnicamente validado.**

---

# 3. Checkpoint 2 — Revisar a pesquisa de casos

Após analisar aproximadamente **15–30 casos**, apresentar os padrões encontrados.

### Ajuda necessária

O TA deverá desafiar a interpretação dos dados.

Perguntas para o TA:

- Os casos selecionados representam adequadamente esse tipo de problema?
- Existem failure domains importantes ausentes?
- Algum comportamento está sendo classificado incorretamente?
- As conclusões realmente são suportadas pelos casos?
- Existe algum viés na amostra?
- Alguma conclusão está sendo tratada como causa quando é apenas um sintoma?

### Resultado esperado

**Taxonomia de problemas e failure domains revisada.**

---

# 4. Checkpoint 3 — Validar o fluxo de troubleshooting

A pesquisa deverá resultar em um fluxo semelhante a:

**Missing Metric → Source → Target Discovery → Scrape → ama-metrics → Configuration → DCR/DCE → Connectivity → Ingestion → Query → Failure Domain**

### Ajuda necessária

Pedir ao TA para revisar criticamente esse fluxo.

### Perguntas principais

- A sequência técnica faz sentido?
- Existem checks ausentes?
- Existem checks executados na ordem errada?
- Quais checks são realmente obrigatórios?
- Quais checks dependem do resultado de verificações anteriores?
- Em quais pontos normalmente ocorre um diagnóstico incorreto?
- Onde termina Monitoring ownership?

### Resultado esperado

**Troubleshooting flow tecnicamente validado.**

Esse será um dos principais inputs para o MVP.

---

# 5. Checkpoint 4 — Validar a baseline

Antes de desenvolver o MVP, mostrar ao TA os dados do processo atual.

### Apresentar

- tempo aproximado de diagnóstico;
- checks mais frequentes;
- failure domains encontrados;
- evidências normalmente coletadas;
- evidências frequentemente ausentes;
- etapas repetitivas;
- principais pontos de dificuldade.

### Ajuda necessária

Responder principalmente:

> As métricas escolhidas realmente representam a dificuldade do troubleshooting?

E:

> Existe evidência suficiente para justificar a criação do MVP?

### Resultado esperado

**Baseline aceita como referência para o experimento.**

---

# 6. Checkpoint 5 — Definir o escopo final do MVP

Este é um dos checkpoints mais importantes.

A pesquisa pode encontrar dezenas de oportunidades.

O MVP não deve tentar resolver todas.

### Ajuda necessária

Revisar a priorização baseada em:

**Frequency × Diagnostic Time × Repetition × Automation Feasibility**

### Pedir ao TA para desafiar

- o que deve entrar no MVP;
- o que deve ficar fora;
- quais checks oferecem maior valor;
- quais verificações podem ser automatizadas;
- quais decisões precisam permanecer humanas;
- quais dados estarão realmente disponíveis;
- se a solução está ficando complexa demais.

### Resultado esperado

**MVP pequeno, realista e tecnicamente defensável.**

---

# 7. Checkpoint 6 — Review técnico do MVP

Após a primeira versão funcional, realizar um technical review.

### O TA deverá avaliar

- lógica de decisão;
- sequência dos checks;
- interpretação das evidências;
- validação dos inputs;
- tratamento de dados ausentes;
- classificação do failure domain;
- recomendações produzidas;
- possíveis falsos diagnósticos;
- situações em que o MVP deveria responder **inconclusive**.

### Pergunta crítica

> Existe algum cenário em que o MVP aparenta ter certeza do diagnóstico sem possuir evidência suficiente?

### Resultado esperado

**MVP tecnicamente seguro para iniciar os experimentos.**

---

# 8. Checkpoint 7 — Validar os cenários de teste

Antes do experimento, apresentar os **8–12 cenários** planejados.

### Exemplos

- target não descoberto;
- target `DOWN`;
- scrape incorreto;
- problema em `ama-metrics`;
- configuração incorreta;
- DCR/DCE;
- conectividade;
- DNS/AMPLS;
- ingestion;
- query incorreta;
- ownership de outra equipe;
- evidência insuficiente.

### Ajuda necessária

Validar:

- se os cenários são realistas;
- se existe diversidade suficiente;
- se algum cenário favorece artificialmente o MVP;
- se a causa/failure domain esperado está correto;
- qual evidência seria necessária para considerar o diagnóstico correto.

### Resultado esperado

**Test dataset validado antes do experimento.**

---

# 9. Checkpoint 8 — Definir o que significa “diagnóstico correto”

Esse ponto é especialmente importante para evitar avaliar o próprio projeto com critérios subjetivos.

### Para cada cenário, definir previamente

**Expected failure domain**

**Required evidence**

**Expected next action**

**Conditions for inconclusive result**

### Papel do TA

Atuar como reviewer independente desses critérios.

Não perguntar apenas:

> O resultado do MVP parece correto?

Definir **antes do experimento** o que será considerado correto.

### Resultado esperado

**Ground truth ou critérios de diagnóstico definidos antes dos testes.**

---

# 10. Checkpoint 9 — Revisar os resultados

Após comparar:

**Manual troubleshooting vs. MVP-assisted troubleshooting**

apresentar os resultados ao TA.

### Métricas

- diagnostic time;
- diagnostic accuracy;
- evidence completeness;
- quantidade de checks manuais;
- engineer feedback;
- confidence;
- willingness to reuse.

### Ajuda necessária

O TA deverá desafiar a interpretação:

- A melhoria observada foi realmente causada pelo MVP?
- O tamanho da amostra permite essa conclusão?
- Existem resultados contraditórios?
- Existem casos em que o processo manual foi melhor?
- Existem limitações não consideradas?
- Algum resultado foi interpretado de maneira otimista?

### Resultado esperado

**Conclusões baseadas nos dados, inclusive quando os resultados forem negativos.**

---

# 11. Checkpoint 10 — Review final do Capstone

Antes da apresentação final, realizar um último review.

### Apresentar a narrativa completa

**Problem**

↓

**Evidence**

↓

**Opportunity**

↓

**MVP**

↓

**Experiment**

↓

**Measured Impact**

↓

**Learnings**

↓

**Next Steps**

### Pedir ao TA para avaliar

- coerência da história;
- precisão técnica;
- evidência das afirmações;
- clareza dos resultados;
- limitações;
- possíveis perguntas difíceis da banca;
- pontos que precisam de mais evidência.

### Pergunta final ao TA

> Se este projeto fosse apresentado agora para uma audiência técnica que não participou dele, quais partes seriam questionadas?

### Resultado esperado

**Capstone tecnicamente defensável e pronto para apresentação.**

---

# 12. Cadência da mentoria

Não é necessário envolver o TA semanalmente em todas as atividades.

A mentoria pode ocorrer em checkpoints estratégicos:

| Momento | Review |
|---|---|
| Início | Problem statement |
| Após primeiros casos | Pesquisa e taxonomia |
| Após research | Troubleshooting flow |
| Antes do MVP | Baseline + oportunidade |
| MVP design | Arquitetura e diagnostic logic |
| Antes dos testes | Cenários + critérios de diagnóstico |
| Depois dos testes | Resultados |
| Antes da apresentação | Final Capstone review |

Reuniões de aproximadamente **30 minutos** podem ser suficientes quando o material for enviado antecipadamente.

---

# 13. O que não esperar do TA

O TA **não será responsável por**:

- desenvolver o MVP;
- realizar a pesquisa;
- analisar todos os casos;
- executar os testes;
- escrever o Capstone;
- tomar decisões pelo participante;
- assumir ownership técnico do projeto.

A responsabilidade do TA será:

> **Guide → Challenge → Review → Validate**

A responsabilidade do participante será:

> **Research → Decide → Build → Test → Measure → Present**

---

# 14. Resultado esperado da mentoria

Ao final do projeto, a participação do TA deverá permitir demonstrar que:

1. o problema foi tecnicamente revisado;
2. a pesquisa foi desafiada por alguém experiente;
3. o troubleshooting flow foi validado;
4. o MVP foi construído sobre evidências;
5. os testes utilizaram critérios definidos previamente;
6. os resultados receberam revisão independente;
7. as conclusões não dependem apenas da opinião de quem desenvolveu o projeto.

O objetivo da mentoria não é simplesmente ajudar a construir uma ferramenta melhor.

É tornar o processo completo do Capstone **mais rigoroso, tecnicamente defensável e baseado em evidências**.
