# DEV Academy FY27 Capstone — Plano de Execução

## Projeto

**Accelerating Troubleshooting for Missing Prometheus Metrics in Azure Monitor**

### Objetivo

Pesquisar como problemas de métricas Prometheus ausentes são investigados atualmente e desenvolver um MVP que ajude Support Engineers a identificar mais rapidamente por que métricas esperadas não estão disponíveis no Azure Monitor workspace.

### Estrutura

**Problem → Evidence → Opportunity → MVP → Experiment → Measured Impact**

---

# 1. Cronograma executivo

| Fase | Período | Objetivo | Entregável |
|---|---|---|---|
| 0. Preparação | 23–27 nov. | Preparar pesquisa e organização | Research template + backlog |
| 1. Problem Discovery | 30 nov.–11 dez. | Encontrar e analisar casos | Dataset de casos |
| 2. User Research | 7–18 dez. | Validar problema com engenheiros | Entrevistas + findings |
| 3. Evidence & Baseline | 4–15 jan. | Quantificar problema atual | Baseline |
| 4. Opportunity | 18–22 jan. | Definir exatamente o MVP | MVP specification |
| 5. MVP Build | 25 jan.–12 fev. | Construir MVP funcional | MVP v1 |
| 6. Experiment | 15–26 fev. | Comparar manual vs. MVP | Dataset experimental |
| 7. Analysis | 1–5 mar. | Medir impacto | Resultados |
| 8. Capstone | 8–12 mar. | Consolidar narrativa | Capstone final |

> Dezembro deve ser usado principalmente para pesquisa e coleta de evidências. O desenvolvimento do MVP só começa depois que os dados mostrarem **qual problema vale a pena resolver**.

---

# 2. Fase 0 — Preparação

## 23–27 novembro de 2026

### Objetivo

Criar a estrutura necessária para que a pesquisa produza dados comparáveis.

### Atividades

- [ ] Criar página principal da wiki
- [ ] Criar backlog do projeto
- [ ] Criar template de análise de casos
- [ ] Definir critérios de inclusão/exclusão
- [ ] Definir regras de anonimização
- [ ] Criar taxonomia inicial de failure domains
- [ ] Definir termos para localizar casos
- [ ] Preparar roteiro das entrevistas
- [ ] Identificar possíveis Support Engineers participantes
- [ ] Identificar TA para atuar como mentor/reviewer

### Termos iniciais para pesquisa

- missing Prometheus metrics
- metrics not available
- Prometheus metrics missing
- metrics stopped
- target down
- scrape failure
- ama-metrics
- Azure Monitor workspace
- Prometheus ingestion
- DCR
- DCE
- AMPLS

### Deliverables

**D1 — Research Template**

**D2 — Case Selection Criteria**

**D3 — Initial Failure Domain Taxonomy**

**D4 — Interview Guide**

### Gate

Não iniciar análise em escala antes de existir um modelo consistente para registrar os casos.

---

# 3. Fase 1 — Problem Discovery

## 30 novembro – 11 dezembro de 2026

### Objetivo

Obter evidência de que missing Prometheus metrics é um problema recorrente e entender como esses casos são investigados.

### Meta

Analisar inicialmente:

**15–30 casos**

### Para cada caso registrar

- sintoma inicial;
- ambiente;
- métrica afetada;
- comportamento esperado;
- comportamento observado;
- target discovery;
- target status;
- scrape status;
- saúde do `ama-metrics`;
- configuração relevante;
- DCR/DCE;
- conectividade;
- evidências coletadas;
- comandos utilizados;
- sequência do troubleshooting;
- failure domain;
- causa, quando conhecida;
- resolução;
- tempo aproximado de diagnóstico;
- etapas manuais;
- gaps de troubleshooting.

### Classificar failure domain

- Metric expectation
- Target discovery
- Scraping
- Configuration
- ama-metrics
- DCR/DCE
- Connectivity
- Ingestion/publication
- Query/visualization
- Outside Monitoring

### Pergunta principal

> Quais verificações aparecem repetidamente em diferentes casos?

### Deliverables

**D5 — Case Dataset**

15–30 casos anonimizados e classificados.

**D6 — Initial Findings**

Resumo contendo:

- principais sintomas;
- principais failure domains;
- checks mais frequentes;
- evidências mais utilizadas;
- principais gaps.

### Gate

Ao final da fase deve existir evidência de que há **padrões repetitivos suficientes para justificar um MVP**.

---

# 4. Fase 2 — User Research

## 7–18 dezembro de 2026

Esta fase pode ocorrer parcialmente em paralelo com a análise dos casos.

### Objetivo

Descobrir se o comportamento observado nos casos corresponde à experiência real dos Support Engineers.

### Meta

Entrevistar:

**5–8 Support Engineers**

e obter review de pelo menos:

**1 Technical Advisor ou especialista**

### Perguntas principais

1. Qual é o primeiro check quando uma métrica está ausente?
2. Como determinar se o problema está na origem, scrape ou ingestão?
3. Quais evidências normalmente estão ausentes?
4. Qual check é executado repetidamente?
5. O que mais consome tempo?
6. Onde existe maior risco de seguir uma hipótese errada?
7. Quais comandos ou ferramentas são utilizados?
8. Quais evidências são necessárias antes de escalar?
9. O que poderia ser automatizado?
10. O que deveria continuar sob decisão humana?

### Não apresentar inicialmente a solução

O objetivo da entrevista é validar **o problema**, não convencer os participantes sobre o MVP.

### Deliverable

**D7 — User Research Findings**

Organizar os resultados em:

**Observed in Cases**

vs.

**Reported by Engineers**

vs.

**Validated Problem**

### Gate

Os dados dos casos e as entrevistas devem apontar para problemas semelhantes.

---

# 5. Fase 3 — Evidence & Baseline

## 4–15 janeiro de 2027

### Objetivo

Transformar as observações da pesquisa em uma baseline mensurável.

### Mapear processo atual

**Customer symptom**

↓

**Environment validation**

↓

**Metric source**

↓

**Target discovery**

↓

**Scrape**

↓

**ama-metrics**

↓

**DCR/DCE**

↓

**Connectivity**

↓

**Ingestion**

↓

**Query**

↓

**Failure domain**

### Medir

- tempo médio até identificar failure domain;
- quantidade de checks;
- número de ferramentas utilizadas;
- evidências coletadas;
- evidências ausentes;
- hipóteses investigadas;
- retrabalho;
- necessidade de escalada.

### Produzir tabela de frequência

| Failure domain | Casos | % da amostra | Checks repetitivos | Potencial de automação |
|---|---:|---:|---|---|
| Target discovery | TBD | TBD | TBD | TBD |
| Scraping | TBD | TBD | TBD | TBD |
| ama-metrics | TBD | TBD | TBD | TBD |
| DCR/DCE | TBD | TBD | TBD | TBD |
| Connectivity | TBD | TBD | TBD | TBD |
| Ingestion | TBD | TBD | TBD | TBD |

### Deliverables

**D8 — Current Troubleshooting Flow**

**D9 — Baseline**

**D10 — Failure Domain Frequency**

### Gate

Antes de construir qualquer ferramenta deve ser possível responder:

> **Qual parte do troubleshooting está consumindo tempo suficiente para justificar automação?**

---

# 6. Fase 4 — Opportunity Definition

## 18–22 janeiro de 2027

### Objetivo

Converter os resultados da pesquisa em requisitos concretos.

### Priorizar problemas usando

**Frequency × Time × Repetition × Automation feasibility**

### Pergunta central

> Qual é a menor intervenção capaz de produzir impacto mensurável?

### Definir

#### MVP deve fazer

- receber contexto do ambiente;
- determinar quais checks são necessários;
- coletar ou solicitar evidências;
- organizar resultados;
- identificar possível failure domain;
- informar evidências ausentes;
- recomendar próximo passo;
- produzir resumo reutilizável.

#### MVP não deve fazer

- corrigir automaticamente recursos;
- alterar ambiente;
- substituir engenheiro;
- diagnosticar qualquer problema de AKS;
- resolver Self-Managed Prometheus;
- garantir root cause sem evidência.

### Deliverable

**D11 — MVP Specification**

Deve conter:

- problem statement;
- usuário;
- input;
- diagnostic flow;
- output;
- constraints;
- success criteria.

### Gate

Realizar review com o TA.

Pergunta para o review:

> **Este MVP resolve o problema demonstrado pelos dados ou está sendo construída uma solução apenas porque tecnicamente é possível?**

Somente após essa validação começa a implementação.

---

# 7. Fase 5 — MVP Build

## 25 janeiro – 12 fevereiro de 2027

### Semana 1 — Diagnostic Engine

Construir a lógica:

**Missing metric**

↓

Metric exists at source?

↓

Target discovered?

↓

Target UP?

↓

Scrape working?

↓

ama-metrics healthy?

↓

Configuration correct?

↓

DCR/DCE correct?

↓

Connectivity working?

↓

Ingestion working?

↓

Query correct?

↓

**Failure domain / Next action**

### Semana 2 — Evidence Collection

Implementar:

- coleta de informações;
- validações;
- checks;
- tratamento de erros;
- classificação das evidências;
- identificação de dados ausentes.

### Semana 3 — Output

Produzir resultado estruturado:

**Symptom**

**Environment**

**Checks performed**

**Evidence**

**Missing evidence**

**Probable failure domain**

**Confidence**

**Recommended next step**

**Escalation evidence**

### Deliverable

**D12 — MVP v1**

### Gate

O MVP deverá conseguir processar os cenários selecionados para teste sem alterar o ambiente.

---

# 8. Fase 6 — Experiment

## 15–26 fevereiro de 2027

### Objetivo

Demonstrar se o MVP realmente melhora o troubleshooting.

### Preparar

**8–12 cenários**

Exemplos:

1. métrica não existe na origem;
2. target não descoberto;
3. target `DOWN`;
4. scrape incorreto;
5. erro `ama-metrics`;
6. DCR incorreta;
7. DCE/conectividade;
8. AMPLS/DNS;
9. ingestion;
10. query incorreta;
11. outside Monitoring;
12. evidência insuficiente.

---

## Experimento A

### Manual troubleshooting

Registrar:

- tempo;
- checks;
- evidências;
- diagnóstico;
- confidence.

---

## Experimento B

### MVP-assisted troubleshooting

Registrar exatamente as mesmas métricas.

---

## Comparação

### Tempo

Meta:

**≥20% redução**

Stretch goal:

**≥30%**

### Diagnostic accuracy

Meta:

**≥80%**

### Evidence completeness

Meta:

**≥85%**

### Manual checks

Meta:

**≥20% redução**

### Engineer satisfaction

Meta:

**≥4/5**

### Willingness to reuse

Meta:

**≥75%**

### Deliverable

**D13 — Experiment Dataset**

---

# 9. Fase 7 — Results & Analysis

## 1–5 março de 2027

### Objetivo

Determinar objetivamente se o MVP funcionou.

### Comparação principal

| Métrica | Manual | MVP | Diferença |
|---|---:|---:|---:|
| Diagnostic time | TBD | TBD | TBD |
| Manual checks | TBD | TBD | TBD |
| Diagnostic accuracy | TBD | TBD | TBD |
| Evidence completeness | TBD | TBD | TBD |
| Engineer confidence | TBD | TBD | TBD |

### Analisar também

- onde o MVP funcionou;
- onde falhou;
- falsos diagnósticos;
- cenários inconclusivos;
- feedback negativo;
- limitações;
- melhorias propostas.

Resultados negativos também devem ser documentados.

O objetivo do Capstone não é provar que a hipótese estava correta.

O objetivo é demonstrar um processo consistente:

**Hypothesis → Experiment → Evidence → Conclusion**

### Deliverable

**D14 — Measured Impact Report**

---

# 10. Fase 8 — Capstone Final

## 8–12 março de 2027

### Narrativa

## 1. Problem

Missing Prometheus metrics exige investigação através de diferentes partes do pipeline.

## 2. Evidence

Casos e entrevistas demonstraram onde o processo atual apresenta complexidade, repetição e perda de tempo.

## 3. Opportunity

Determinadas verificações poderiam ser executadas ou orientadas de maneira consistente.

## 4. MVP

Foi criado um fluxo diagnóstico para ajudar o Support Engineer a isolar o failure domain.

## 5. Experiment

O troubleshooting manual foi comparado com troubleshooting usando o MVP.

## 6. Measured Impact

Apresentar:

- tempo;
- accuracy;
- evidence completeness;
- manual effort;
- engineer feedback.

## 7. Learnings

O que funcionou e o que não funcionou.

## 8. Next Steps

Como a solução poderia evoluir depois do Capstone.

### Deliverables

**D15 — Final Capstone**

**D16 — Demo**

**D17 — Presentation**

---

# 11. Checkpoints com o TA

O TA não precisa participar da execução diária.

Utilizar checkpoints estratégicos.

### Checkpoint 1 — Problem

**Final de novembro**

Validar problem statement e pesquisa.

### Checkpoint 2 — Evidence

**Meados de janeiro**

Mostrar:

- casos;
- entrevistas;
- patterns;
- baseline.

Perguntar:

> A evidência realmente suporta o problema?

### Checkpoint 3 — MVP Design

**Final de janeiro**

Revisar arquitetura e diagnostic flow.

### Checkpoint 4 — Experiment

**Meados de fevereiro**

Revisar cenários e métricas antes dos testes.

### Checkpoint 5 — Results

**Início de março**

Desafiar conclusões e interpretação dos resultados.

### Checkpoint 6 — Final Capstone

**Antes da apresentação**

Review crítico da narrativa completa.

---

# 12. Definition of Done

O projeto será considerado concluído quando houver:

### Research

- [ ] 15–30 casos analisados
- [ ] casos anonimizados
- [ ] failure domains classificados
- [ ] 5–8 Support Engineers entrevistados
- [ ] principais patterns identificados

### Evidence

- [ ] problema validado
- [ ] baseline definida
- [ ] processo atual documentado
- [ ] oportunidade mensurável identificada

### MVP

- [ ] MVP funcional
- [ ] diagnostic flow implementado
- [ ] evidências registradas
- [ ] failure domain apresentado
- [ ] próximo passo recomendado
- [ ] engenheiro permanece no controle

### Experiment

- [ ] 8–12 cenários testados
- [ ] manual troubleshooting medido
- [ ] MVP-assisted troubleshooting medido
- [ ] métricas comparadas
- [ ] feedback coletado

### Impact

- [ ] diagnostic time calculado
- [ ] diagnostic accuracy calculada
- [ ] evidence completeness calculada
- [ ] manual effort comparado
- [ ] feedback analisado
- [ ] limitações documentadas

### Capstone

- [ ] Problem
- [ ] Evidence
- [ ] Opportunity
- [ ] MVP
- [ ] Experiment
- [ ] Measured Impact
- [ ] Learnings
- [ ] Next Steps

---

# 13. Regra principal do projeto

**Não construir primeiro e procurar um problema depois.**

A ordem deverá permanecer:

> **Descobrir → Medir → Validar → Priorizar → Construir → Experimentar → Medir impacto**

A força do Capstone não estará na complexidade técnica do MVP.

Estará na capacidade de demonstrar, com evidências:

> **“Este problema existe. Foi possível medi-lo. Uma solução focada foi construída. Ela foi testada contra o processo atual. Este foi o impacto observado.”**
