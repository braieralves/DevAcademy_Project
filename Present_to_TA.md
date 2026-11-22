# Roteiro para apresentar o Capstone ao TA

## 1. Contexto — 1 minuto

Estou participando do DEV Academy FY27 e estou estruturando meu Capstone em torno de um problema diretamente relacionado ao trabalho de suporte em Azure Monitoring.

O foco será **troubleshooting de métricas Prometheus ausentes no Azure Monitor**.

A ideia não é simplesmente desenvolver uma ferramenta. Quero primeiro entender o problema usando casos reais, medir como o troubleshooting funciona atualmente e só depois construir um MVP baseado nas evidências encontradas.

---

## 2. Problema — 1 minuto

O cenário que quero investigar é:

> **Por que métricas Prometheus esperadas não estão disponíveis no Azure Monitor workspace e como podemos reduzir o tempo necessário para identificar onde está a falha?**

O problema pode aparecer em diferentes pontos:

- target discovery;
- scraping;
- configuração;
- `ama-metrics`;
- DCR/DCE;
- conectividade;
- AMPLS/DNS;
- ingestion/publication;
- consulta das métricas.

A hipótese é que parte do troubleshooting atual contém checks repetitivos e exige navegação por diferentes componentes até o failure domain ser identificado.

---

## 3. Pesquisa antes da solução — 2 minutos

Antes de desenvolver qualquer MVP, pretendo analisar aproximadamente **15 a 30 casos** relacionados a missing Prometheus metrics.

Para cada caso, quero identificar:

- sintoma;
- checks realizados;
- evidências coletadas;
- failure domain;
- causa identificada;
- tempo aproximado de diagnóstico;
- atividades repetitivas;
- dificuldades encontradas.

Também pretendo conversar com **5 a 8 Support Engineers**.

Quero comparar o que aparece nos casos com aquilo que os engenheiros relatam como suas principais dificuldades.

O objetivo dessa etapa é responder:

> **Qual parte do troubleshooting realmente apresenta uma oportunidade mensurável de melhoria?**

---

## 4. Baseline — 1 minuto

Com esses dados, quero construir uma baseline do processo atual.

Pretendo medir principalmente:

- diagnostic time;
- número de verificações manuais;
- evidence completeness;
- diagnostic accuracy;
- pontos onde ocorre retrabalho.

Somente depois disso será definido exatamente o que entra no MVP.

---

## 5. MVP — 1 minuto

A ideia inicial é desenvolver um MVP que ajude o engenheiro a percorrer o fluxo diagnóstico.

Por exemplo:

**Missing metric → Source → Target Discovery → Scrape → ama-metrics → Configuration → DCR/DCE → Connectivity → Ingestion → Query**

O objetivo não é substituir o engenheiro nem corrigir automaticamente o ambiente.

O MVP deve ajudar a:

- organizar os checks;
- identificar evidências necessárias;
- eliminar hipóteses;
- identificar o provável failure domain;
- indicar o próximo passo.

O engenheiro continua tomando a decisão.

---

## 6. Experimento — 1 minuto

Depois pretendo testar o MVP usando aproximadamente **8 a 12 cenários**.

A comparação será:

> **Manual troubleshooting vs. MVP-assisted troubleshooting**

Pretendo medir:

- diagnostic time;
- diagnostic accuracy;
- evidence completeness;
- quantidade de verificações manuais;
- feedback dos engenheiros.

Assim, o Capstone não ficará baseado apenas na demonstração de uma ferramenta. Haverá uma comparação objetiva entre o processo atual e a solução proposta.

---

## 7. Onde preciso da sua ajuda — 2 minutos

É principalmente aqui que gostaria da sua participação como mentor.

Não preciso que você desenvolva o projeto comigo.

Gostaria que você atuasse como **technical mentor e reviewer**, ajudando a desafiar minhas decisões em checkpoints específicos.

Principalmente:

### Problema

Quero validar se o problema e o escopo fazem sentido tecnicamente.

### Pesquisa

Depois de analisar os casos, gostaria que você desafiasse os padrões e failure domains que identifiquei.

### Troubleshooting flow

Quero que você revise se os checks estão corretos, se algo importante está faltando e se estou fazendo alguma suposição errada.

### MVP

Antes de desenvolver, quero validar se a solução realmente responde ao problema encontrado na pesquisa.

### Experimento

Gostaria de ajuda para validar os cenários e, principalmente, definir **antes dos testes** o que será considerado um diagnóstico correto.

### Resultados

Depois do experimento, gostaria que você desafiasse minhas conclusões e verificasse se os dados realmente suportam aquilo que estou afirmando.

### Capstone final

Por último, gostaria de um review técnico da apresentação antes da entrega.

---

## 8. Como funcionaria a mentoria — 30 segundos

Não estou pensando em reuniões semanais nem em consumir muito do seu tempo.

A proposta é ter alguns checkpoints durante o projeto:

**Problem → Research → MVP Design → Experiment → Results → Final Review**

Eu preparo e executo o trabalho entre os checkpoints e trago resultados concretos para discussão.

---

## 9. Pedido — 30 segundos

O que gostaria de pedir é se você poderia atuar como meu **Technical Advisor mentor durante o Capstone**.

A execução e o ownership continuam sendo meus.

O que considero realmente valioso na sua participação é ter alguém experiente que possa **questionar minhas decisões, identificar gaps e ajudar a validar tecnicamente o trabalho antes que eu avance para a próxima fase**.

A ideia é não chegar ao final do projeto e descobrir que alguma premissa fundamental estava errada.

Se fizer sentido para você, gostaria de contar com sua ajuda nesses checkpoints.
