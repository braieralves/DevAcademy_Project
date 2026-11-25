# DEV Academy FY27 Capstone

## Troubleshooting de métricas Prometheus ausentes no Azure Monitor

---

## 1. Visão geral

Este Capstone tem como objetivo melhorar e acelerar o troubleshooting de cenários em que métricas Prometheus esperadas não estão disponíveis no Azure Monitor workspace.

O projeto analisará casos reais ou derivados de casos reais para identificar sintomas recorrentes, etapas manuais, evidências necessárias e pontos de maior dificuldade no processo atual. Com base nessa pesquisa, será desenvolvido um MVP capaz de orientar o Support Engineer na identificação do estágio do pipeline em que a falha provavelmente está ocorrendo.

### Starter kit (semana 1)

Foi adicionado um kit inicial em:

`mvp-prometheus-diagnostic-starter/`

Com:
- prompt operacional;
- checklist de investigação;
- script leve de coleta de evidências.

### Estrutura do Capstone

**Problem → Evidence → Opportunity → MVP → Experiment → Measured Impact**

---

# 2. Definição do problema

## 2.1 Problem statement

Support Engineers recebem casos em que métricas Prometheus esperadas estão ausentes, incompletas, inconsistentes ou deixaram de estar disponíveis no Azure Monitor workspace.

O sintoma apresentado pelo cliente normalmente é simples, como “as métricas não aparecem”. Entretanto, a causa pode estar em diferentes componentes ou etapas do fluxo:

1. descoberta do target;
2. configuração de scraping;
3. disponibilidade do endpoint;
4. scrape da métrica;
5. processamento pelo `ama-metrics`;
6. Data Collection Rule;
7. Data Collection Endpoint;
8. conectividade privada ou pública;
9. AMPLS e resolução DNS;
10. autenticação ou autorização;
11. encaminhamento das métricas;
12. ingestão e publicação no Azure Monitor workspace;
13. consulta incorreta ou expectativa equivocada sobre a métrica.

Essa distribuição de possíveis causas torna o troubleshooting complexo, demorado e dependente da experiência individual do engenheiro.

---

## 2.2 Problema central

O processo atual de troubleshooting de métricas Prometheus ausentes pode exigir diversas verificações manuais, coleta de evidências em fontes diferentes e conhecimento especializado sobre o pipeline completo.

Não existe necessariamente uma sequência única e consistente para:

- validar o ambiente;
- confirmar se a métrica existe na origem;
- verificar se o target foi descoberto;
- confirmar se o target está sendo scraped;
- analisar a saúde dos componentes de coleta;
- validar DCR, DCE e associações;
- identificar problemas de conectividade;
- determinar se a falha está na coleta, no transporte ou na publicação;
- reunir evidências suficientes para o próximo passo ou para uma escalada.

Como resultado, casos semelhantes podem receber abordagens diferentes, apresentar coleta incompleta de evidências ou exigir mais tempo até a identificação do failure domain.

---

## 2.3 Pergunta principal da pesquisa

> Um processo diagnóstico orientado pode reduzir o tempo e o trabalho manual necessários para que Support Engineers identifiquem por que métricas Prometheus esperadas não estão disponíveis no Azure Monitor workspace?

---

## 2.4 Hipótese

Se as verificações mais importantes forem organizadas em um fluxo diagnóstico orientado, baseado em evidências de casos anteriores, então o Support Engineer poderá:

- identificar o failure domain mais rapidamente;
- executar menos verificações manuais;
- coletar evidências mais consistentes;
- reduzir hipóteses incorretas;
- selecionar o próximo passo de troubleshooting com maior confiança;
- produzir escaladas mais completas quando o problema não estiver no escopo de Monitoring.

---

## 2.5 Usuário-alvo

O usuário principal do MVP será o **Support Engineer responsável por investigar problemas relacionados a Azure Monitor Managed Service for Prometheus**.

Usuários secundários poderão incluir:

- Technical Advisors;
- Escalation Engineers;
- Incident Managers;
- engenheiros de produto que recebam escaladas;
- engenheiros de outras áreas envolvidos em conectividade, AKS ou configuração do ambiente.

---

## 2.6 Cenários incluídos

O projeto considera cenários como:

- métricas Prometheus completamente ausentes;
- apenas determinadas métricas ausentes;
- métricas coletadas parcialmente;
- métricas que estavam disponíveis e deixaram de aparecer;
- métricas disponíveis na origem, mas ausentes no workspace;
- targets não descobertos;
- targets descobertos, mas com estado `DOWN`;
- targets disponíveis, mas não scraped corretamente;
- endpoints inacessíveis;
- erros nos componentes `ama-metrics`;
- erros de configuração de scraping;
- seletores incorretos;
- problemas em ConfigMaps;
- associações incorretas de DCR ou DCE;
- problemas de conectividade, DNS, Private Endpoint ou AMPLS;
- falhas de autenticação ou autorização;
- erros no encaminhamento, ingestão ou publicação;
- consultas que não retornam uma métrica que deveria estar disponível.

---

## 2.7 Cenários fora do escopo inicial

O MVP inicial não pretende:

- diagnosticar todos os problemas possíveis de AKS;
- substituir a investigação de Self-Managed Prometheus;
- criar dashboards personalizados;
- desenvolver consultas específicas para cenários de negócio;
- substituir a atuação do Support Engineer;
- corrigir automaticamente configurações do cliente;
- executar alterações sem validação;
- solucionar problemas de visualização que pertençam exclusivamente ao Grafana;
- determinar automaticamente a causa raiz de qualquer falha possível;
- cobrir todos os produtos integrados ao Azure Monitor.

Esses limites mantêm o projeto focado no problema principal: **métricas Prometheus esperadas que não estão disponíveis no Azure Monitor workspace**.

---

# 3. Plano de pesquisa

## 3.1 Objetivo da pesquisa

Compreender como os casos de métricas Prometheus ausentes são investigados atualmente e identificar oportunidades concretas para reduzir tempo, esforço manual e inconsistência no diagnóstico.

A pesquisa deverá responder:

1. Com que frequência esses casos ocorrem?
2. Quais são os sintomas mais comuns?
3. Quais são as causas ou failure domains mais frequentes?
4. Quais verificações são repetidas em diferentes casos?
5. Quais evidências são essenciais para o diagnóstico?
6. Quais etapas consomem mais tempo?
7. Onde os Support Engineers encontram maior dificuldade?
8. Quais verificações podem ser orientadas ou automatizadas?
9. Como medir se o MVP realmente melhora o processo?

---

## 3.2 Fontes de evidência

A pesquisa poderá utilizar:

- casos de suporte encerrados;
- casos de suporte ativos, quando apropriado;
- notas técnicas;
- resumos de troubleshooting;
- comunicações com clientes;
- escaladas internas;
- colaborações com outras equipes;
- diagnósticos coletados do ambiente;
- scripts e comandos utilizados;
- orientações existentes;
- entrevistas com Support Engineers;
- feedback de Technical Advisors;
- documentação oficial utilizada durante as investigações.

Todos os dados utilizados deverão ser tratados de acordo com os requisitos aplicáveis de privacidade, segurança e confidencialidade. Informações identificáveis de clientes não deverão aparecer nos materiais do Capstone.

---

## 3.3 Critérios para seleção dos casos

### Critérios de inclusão

O caso poderá ser incluído quando:

- o sintoma principal envolver métricas Prometheus ausentes, incompletas ou indisponíveis;
- o Azure Monitor workspace fizer parte do fluxo investigado;
- existir informação suficiente para reconstruir pelo menos parte do troubleshooting;
- houver evidências sobre as verificações executadas;
- o caso ajudar a identificar um padrão, dificuldade ou failure domain;
- o caso representar um cenário relevante para o MVP.

### Critérios de exclusão

O caso deverá ser excluído quando:

- o problema for exclusivamente de visualização no Grafana;
- o cenário envolver apenas Self-Managed Prometheus;
- não existir informação suficiente para entender o problema;
- o caso estiver fora do escopo de Azure Monitor Managed Service for Prometheus;
- o sintoma não envolver realmente coleta ou disponibilidade de métricas;
- a utilização do caso apresentar riscos de privacidade ou confidencialidade;
- o caso for duplicado e não adicionar evidência nova.

---

## 3.4 Tamanho inicial da amostra

A pesquisa deverá começar com uma amostra pequena, porém representativa.

### Meta inicial

- analisar entre **15 e 30 casos**;
- buscar casos com diferentes sintomas;
- incluir, sempre que possível, diferentes failure domains;
- evitar que toda a amostra represente apenas uma única causa;
- expandir a amostra se os padrões encontrados ainda forem inconclusivos.

O objetivo não é produzir uma estatística definitiva de todos os casos existentes. O objetivo é encontrar evidência suficiente para definir um problema real, recorrente e adequado a um MVP.

---

## 3.5 Informações que deverão ser extraídas

Para cada caso, registrar:

| Campo | Descrição |
|---|---|
| Identificador anonimizado | Referência interna sem dados identificáveis do cliente |
| Sintoma reportado | Como o problema foi inicialmente descrito |
| Métrica afetada | Tipo ou categoria da métrica ausente |
| Escopo da ausência | Todas as métricas, algumas métricas ou uma métrica específica |
| Comportamento temporal | Nunca funcionou, parou de funcionar ou ocorre de forma intermitente |
| Ambiente | Componentes relevantes do ambiente |
| Configuração de acesso | Público, privado, Private Endpoint ou AMPLS |
| Target discovery | Se o target foi descoberto |
| Target status | `UP`, `DOWN`, ausente ou desconhecido |
| Scrape status | Se o scrape ocorreu corretamente |
| Saúde dos componentes | Estado dos componentes `ama-metrics` |
| DCR/DCE | Configuração, associações e problemas identificados |
| Conectividade | DNS, endpoints, firewall, proxy e rotas relevantes |
| Evidências coletadas | Logs, comandos, screenshots, bundles e resultados |
| Etapas executadas | Sequência do troubleshooting |
| Equipes envolvidas | Áreas necessárias para continuar a investigação |
| Failure domain | Área em que a falha foi isolada |
| Causa raiz | Causa confirmada, quando disponível |
| Resolução | Alteração ou ação que restaurou o funcionamento |
| Tempo de diagnóstico | Tempo aproximado até identificar o failure domain |
| Trabalho manual | Quantidade aproximada de verificações manuais |
| Dificuldades | Gaps, bloqueios ou verificações inconclusivas |
| Oportunidade para o MVP | Como uma orientação automatizada poderia ajudar |

---

## 3.6 Taxonomia inicial de failure domains

Os casos deverão ser classificados, inicialmente, nas seguintes categorias:

### FD1. Expectativa da métrica

- métrica incorreta;
- nome incorreto;
- labels inesperados;
- consulta inadequada;
- métrica não exposta pela aplicação;
- expectativa incompatível com a configuração.

### FD2. Descoberta do target

- target não descoberto;
- seletores incorretos;
- configuração incompatível;
- namespace não incluído;
- service ou pod não elegível.

### FD3. Scraping

- endpoint indisponível;
- porta incorreta;
- path incorreto;
- timeout;
- autenticação;
- certificado;
- resposta inválida;
- target com estado `DOWN`.

### FD4. Configuração

- ConfigMap incorreto;
- configuração não aplicada;
- parâmetros inválidos;
- conflito de configurações;
- configuração de keep-list inadequada;
- regras que descartam a métrica.

### FD5. Componentes de coleta

- pods `ama-metrics` não saudáveis;
- reinicializações;
- erros nos logs;
- problemas de recursos;
- falha de processamento;
- problema de extensão ou componente gerenciado.

### FD6. DCR e DCE

- DCR ausente;
- associação incorreta;
- DCE incorreto;
- resource ID inesperado;
- configuração inconsistente;
- alteração não propagada.

### FD7. Conectividade

- DNS;
- firewall;
- proxy;
- Private Endpoint;
- AMPLS;
- endpoint não permitido;
- rota ou resolução incorreta;
- bloqueio de comunicação.

### FD8. Ingestão ou publicação

- dados coletados, mas não encaminhados;
- falha entre componentes;
- erro de autenticação ou autorização;
- problema de publicação;
- indisponibilidade ou comportamento do serviço.

### FD9. Visualização ou consulta

- período incorreto;
- filtro incorreto;
- label incorreto;
- datasource incorreto;
- dashboard ou consulta incompatível;
- dados disponíveis, mas não encontrados pelo método utilizado.

### FD10. Fora do escopo de Monitoring

- problema na aplicação;
- problema no endpoint do cliente;
- configuração do cluster;
- infraestrutura externa;
- Self-Managed Prometheus;
- problema específico de outro produto.

A taxonomia deverá ser atualizada à medida que a análise dos casos revelar novos padrões.

---

## 3.7 Método de análise dos casos

### Etapa 1: Localização

Selecionar casos relacionados a termos e sintomas como:

- missing Prometheus metrics;
- Prometheus metrics not available;
- metrics not showing;
- metrics stopped;
- target down;
- scrape failure;
- `ama-metrics`;
- Azure Monitor workspace;
- DCR;
- DCE;
- AMPLS;
- Prometheus ingestion;
- intermittent metrics;
- partial metrics.

### Etapa 2: Triagem

Verificar se cada caso atende aos critérios de inclusão e se possui evidência suficiente.

### Etapa 3: Anonimização

Remover ou substituir:

- nomes de clientes;
- subscription IDs;
- tenant IDs;
- resource IDs;
- nomes de clusters;
- IPs;
- URLs privadas;
- nomes de pessoas;
- qualquer informação confidencial.

### Etapa 4: Extração

Preencher o modelo padronizado com as informações disponíveis em cada caso.

### Etapa 5: Classificação

Associar o caso a:

- sintoma;
- failure domain;
- causa;
- evidências utilizadas;
- etapas manuais;
- resultado final.

### Etapa 6: Identificação de padrões

Identificar:

- verificações recorrentes;
- evidências frequentemente ausentes;
- causas comuns;
- pontos de atraso;
- decisões que dependem de conhecimento especializado;
- etapas adequadas para automação ou orientação.

### Etapa 7: Priorização

Priorizar oportunidades de acordo com:

- frequência;
- impacto no tempo de diagnóstico;
- repetibilidade;
- disponibilidade dos dados;
- viabilidade técnica;
- adequação ao período do Capstone;
- capacidade de produzir impacto mensurável.

---

## 3.8 Entrevistas com Support Engineers

### Objetivo

Validar se os padrões encontrados nos casos correspondem à experiência dos engenheiros que realizam o troubleshooting.

### Participantes sugeridos

- entre **5 e 8 Support Engineers**;
- pelo menos um Technical Advisor ou especialista;
- engenheiros com diferentes níveis de experiência;
- profissionais que tenham trabalhado recentemente em casos de Prometheus metrics.

### Perguntas propostas

1. Quais são os primeiros checks realizados quando uma métrica está ausente?
2. Como é determinado se o problema está na origem, no scrape ou na ingestão?
3. Quais informações normalmente faltam no início do caso?
4. Quais verificações são repetidas com maior frequência?
5. Qual etapa costuma consumir mais tempo?
6. Em qual etapa existe maior risco de seguir uma hipótese incorreta?
7. Quais comandos, scripts ou ferramentas são utilizados?
8. Quais evidências são obrigatórias antes de uma escalada?
9. Que parte do processo poderia ser automatizada?
10. Que parte deve continuar dependendo da avaliação humana?
11. Qual seria o resultado mínimo necessário para que uma ferramenta fosse útil?
12. O que faria o engenheiro não confiar na recomendação do MVP?

---

## 3.9 Baseline do processo atual

Antes da implementação do MVP, deverá ser documentado como o troubleshooting é realizado sem assistência.

### Fluxo de referência

**Problema reportado → Validação do ambiente → Confirmação da métrica na origem → Descoberta do target → Validação do scrape → Saúde dos componentes → DCR/DCE → Conectividade → Ingestão/publicação → Isolamento do failure domain → Próximo passo ou escalada**

### Métricas da baseline

- tempo total até o diagnóstico;
- tempo até identificar o failure domain;
- número de verificações manuais;
- número de ferramentas ou fontes consultadas;
- quantidade de evidências coletadas;
- quantidade de evidências obrigatórias ausentes;
- número de hipóteses investigadas;
- correção do diagnóstico;
- necessidade de retrabalho;
- confiança do engenheiro;
- qualidade da recomendação de próximo passo.

---

## 3.10 Resultados esperados da pesquisa

A fase de pesquisa deverá produzir:

1. uma definição validada do problema;
2. uma taxonomia de sintomas e failure domains;
3. uma lista de verificações recorrentes;
4. uma lista de evidências obrigatórias;
5. um fluxo representando o processo atual;
6. uma baseline mensurável;
7. uma lista priorizada de oportunidades;
8. requisitos funcionais do MVP;
9. cenários para teste;
10. critérios claros de sucesso.

---

# 4. Definição do MVP

## 4.1 Objetivo do MVP

O MVP deverá ajudar o Support Engineer a identificar **em qual estágio do pipeline Prometheus a falha provavelmente está ocorrendo**.

A ferramenta deverá orientar o troubleshooting por meio de uma sequência lógica de validações, registrar as evidências utilizadas e recomendar o próximo passo.

---

## 4.2 Fluxo diagnóstico proposto

**Métrica ausente**

↓

**A métrica está sendo exposta na origem?**

↓

**O target foi descoberto?**

↓

**O target está `UP` e sendo scraped?**

↓

**Os componentes `ama-metrics` estão saudáveis?**

↓

**A configuração de scraping está correta?**

↓

**DCR, DCE e associações estão corretas?**

↓

**Existe conectividade até os endpoints necessários?**

↓

**As métricas estão sendo encaminhadas e publicadas?**

↓

**A consulta utilizada para validar a métrica está correta?**

↓

**Failure domain identificado ou próximo passo recomendado**

---

## 4.3 Capacidades mínimas

O MVP deverá:

- receber informações básicas sobre o ambiente;
- registrar o comportamento esperado e o comportamento observado;
- conduzir uma sequência lógica de verificações;
- diferenciar coleta, transporte, ingestão e consulta;
- indicar quais evidências precisam ser coletadas;
- identificar verificações concluídas, pendentes ou inconclusivas;
- apresentar o provável failure domain;
- recomendar o próximo passo;
- indicar quando outra equipe deve ser envolvida;
- preservar o engenheiro como responsável pela decisão;
- gerar uma saída reutilizável na documentação do caso.

---

## 4.4 Saída esperada

A saída deverá conter:

- resumo do sintoma;
- informações relevantes do ambiente;
- verificações executadas;
- evidências encontradas;
- verificações pendentes;
- provável failure domain;
- nível de confiança;
- possíveis hipóteses;
- próximo passo recomendado;
- evidências necessárias para escalada;
- indicação de possível ownership por outra equipe.

---

# 5. Critérios de sucesso do MVP

## 5.1 Princípio de avaliação

O sucesso do MVP não será determinado apenas pela conclusão técnica da ferramenta.

O MVP será considerado eficaz se demonstrar melhoria mensurável em comparação com o troubleshooting manual, mantendo ou aumentando a qualidade do diagnóstico.

A comparação principal será:

> **Manual troubleshooting vs. MVP-assisted troubleshooting**

---

## 5.2 Critérios obrigatórios

### SC1. Redução do tempo de diagnóstico

O MVP deverá reduzir o tempo necessário para identificar o provável failure domain.

**Métrica:**

`Redução (%) = ((Tempo manual − Tempo com MVP) ÷ Tempo manual) × 100`

**Meta inicial:**

- redução média mínima de **20%**;
- objetivo desejável de **30% ou mais**.

---

### SC2. Correção do failure domain

O MVP deverá direcionar o engenheiro para o domínio correto da falha.

**Métrica:**

`Diagnostic accuracy = cenários com failure domain correto ÷ total de cenários`

**Meta inicial:**

- identificar corretamente o failure domain em pelo menos **80% dos cenários testados**;
- não produzir recomendações incorretas de alto risco;
- declarar resultado inconclusivo quando não houver evidência suficiente.

---

### SC3. Completude das evidências

O MVP deverá melhorar a consistência das evidências coletadas.

**Métrica:**

`Evidence completeness = evidências obrigatórias coletadas ÷ evidências obrigatórias esperadas`

**Meta inicial:**

- pelo menos **85% das evidências obrigatórias** coletadas ou explicitamente solicitadas;
- evidências ausentes claramente identificadas;
- nenhuma conclusão apresentada como confirmada sem evidência suficiente.

---

### SC4. Redução de verificações manuais

O MVP deverá reduzir verificações repetitivas que não agregam valor ao diagnóstico.

**Métrica:**

- número de checks manuais sem o MVP;
- número de checks manuais com o MVP;
- redução percentual;
- quantidade de verificações orientadas ou automatizadas.

**Meta inicial:**

- redução mínima de **20% nas etapas manuais repetitivas**;
- eliminação de pelo menos uma atividade recorrente de coleta ou organização de dados.

---

### SC5. Qualidade do próximo passo

A recomendação deverá ser tecnicamente adequada às evidências coletadas.

**Avaliação:**

- correta;
- parcialmente correta;
- incorreta;
- inconclusiva.

**Meta inicial:**

- pelo menos **80% das recomendações avaliadas como corretas**;
- nenhuma recomendação deve sugerir alterações destrutivas;
- ações corretivas devem depender da validação do engenheiro.

---

### SC6. Utilidade para o Support Engineer

O MVP deverá ser considerado útil pelos engenheiros participantes.

**Escala sugerida:**

1. Discordo totalmente  
2. Discordo  
3. Neutro  
4. Concordo  
5. Concordo totalmente

**Afirmações avaliadas:**

- o fluxo foi fácil de seguir;
- as verificações foram relevantes;
- a ferramenta ajudou a organizar a investigação;
- as evidências coletadas foram úteis;
- a recomendação final foi compreensível;
- a ferramenta reduziu esforço manual;
- a ferramenta seria utilizada em casos reais.

**Meta inicial:**

- média mínima de **4 em 5**;
- pelo menos **75% dos participantes** indicariam utilização futura.

---

### SC7. Transparência

O MVP deverá mostrar como chegou à recomendação.

**Meta:**

- listar as verificações executadas;
- relacionar cada conclusão à evidência correspondente;
- diferenciar fatos, hipóteses e dados ausentes;
- evitar diagnósticos sem explicação;
- permitir revisão pelo Support Engineer.

---

### SC8. Segurança e controle humano

O MVP deverá manter o engenheiro no controle.

**Meta:**

- não realizar alterações no ambiente;
- não executar correções automaticamente;
- não ocultar evidências;
- não apresentar hipótese como causa confirmada;
- solicitar validação antes de qualquer ação;
- informar quando o diagnóstico for inconclusivo.

---

## 5.3 Critérios desejáveis

Além dos critérios obrigatórios, o MVP poderá:

- gerar um resumo para as notas do caso;
- produzir uma checklist de evidências;
- recomendar documentação oficial;
- facilitar a preparação de escaladas;
- identificar possível ownership por outra equipe;
- comparar os resultados com padrões conhecidos;
- reutilizar diagnósticos previamente coletados;
- apresentar comandos necessários para validação;
- adaptar o fluxo de acordo com o ambiente público ou privado.

---

## 5.4 Critérios de falha

O MVP deverá ser considerado insuficiente se:

- não reduzir o tempo de diagnóstico;
- indicar frequentemente o failure domain incorreto;
- exigir mais esforço que o processo manual;
- ocultar a origem das recomendações;
- produzir resultados sem evidência;
- aumentar o risco de alteração incorreta;
- depender de dados que os Support Engineers normalmente não conseguem obter;
- tentar cobrir tantos cenários que o fluxo deixe de ser utilizável;
- não receber validação positiva dos usuários-alvo.

---

# 6. Plano de validação

## 6.1 Cenários de teste

Criar entre **8 e 12 cenários**, cobrindo diferentes failure domains.

Exemplos:

1. métrica não exposta na origem;
2. target não descoberto;
3. target `DOWN`;
4. configuração de scraping incorreta;
5. erro nos componentes `ama-metrics`;
6. associação incorreta de DCR;
7. problema relacionado a DCE;
8. bloqueio de conectividade;
9. problema de DNS ou AMPLS;
10. métrica coletada, mas não encontrada pela consulta;
11. problema pertencente a outra equipe;
12. cenário inconclusivo por falta de evidências.

---

## 6.2 Experimento

Cada cenário deverá ser investigado de duas formas:

### Grupo A: Troubleshooting manual

O engenheiro utiliza o processo atual, sem o MVP.

### Grupo B: Troubleshooting assistido

O engenheiro utiliza o MVP para orientar a investigação.

Sempre que possível, alternar a ordem ou utilizar participantes diferentes para reduzir o efeito de aprendizagem.

---

## 6.3 Dados coletados

Para cada execução, registrar:

- tempo total;
- tempo até identificar o failure domain;
- número de verificações;
- evidências coletadas;
- evidências ausentes;
- diagnóstico final;
- correção do diagnóstico;
- próximo passo recomendado;
- confiança do participante;
- dificuldade percebida;
- comentários qualitativos.

---

## 6.4 Matriz de avaliação

| Critério | Baseline | Com MVP | Meta |
|---|---:|---:|---:|
| Tempo médio de diagnóstico | A medir | A medir | Redução ≥ 20% |
| Correção do failure domain | A medir | A medir | ≥ 80% |
| Completude das evidências | A medir | A medir | ≥ 85% |
| Checks manuais | A medir | A medir | Redução ≥ 20% |
| Qualidade do próximo passo | A medir | A medir | ≥ 80% |
| Satisfação dos usuários | Não aplicável | A medir | ≥ 4/5 |
| Interesse em reutilizar | Não aplicável | A medir | ≥ 75% |

---

# 7. Entregáveis

## Pesquisa

- conjunto anonimizado de casos analisados;
- critérios de inclusão e exclusão;
- taxonomia de sintomas e failure domains;
- síntese das entrevistas;
- mapa do processo atual;
- baseline do troubleshooting;
- lista priorizada de oportunidades.

## Produto

- requisitos do MVP;
- fluxo diagnóstico;
- implementação funcional;
- documentação de utilização;
- formato de saída;
- registro das limitações.

## Validação

- cenários de teste;
- resultados do troubleshooting manual;
- resultados do troubleshooting assistido;
- comparação quantitativa;
- feedback qualitativo;
- análise dos critérios de sucesso.

## Capstone

- definição do problema;
- evidências;
- oportunidade;
- desenvolvimento do MVP;
- experimento;
- impacto medido;
- limitações;
- aprendizados;
- próximos passos.

---

# 8. Riscos e mitigação

| Risco | Mitigação |
|---|---|
| Escopo excessivamente amplo | Limitar o MVP à identificação do failure domain
