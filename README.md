# NexusMeet - Escopo e Justificativas

## 1. Definição do Produto e Problema

**Produto:** 
*NexusMeet* – Uma plataforma inteligente de gestão de reuniões corporativas focada em agendamento otimizado via IA, transcrição automatizada e extração de plano de ação.

**Problema:** 
Equipes corporativas perdem, em média, 30% do seu tempo útil tentando conciliar agendas, documentando atas manualmente e rastreando tarefas (follow-ups) que se perdem após as reuniões. Há uma clara ineficiência administrativa e quebra de produtividade devido à falta de centralização das informações discutidas e decisões tomadas.

## 2. Personas e Stakeholders

### Personas
* **Persona 1: Helena (Gerente de Produto)**
  * *Perfil:* Lida com múltiplas equipes e tem a agenda sempre lotada. 
  * *Necessidade:* Precisa marcar reuniões rapidamente e garantir que as decisões sejam documentadas sem esforço manual.
* **Persona 2: Carlos (Desenvolvedor Sênior)**
  * *Perfil:* Focado em código, detesta interrupções e reuniões longas sem propósito.
  * *Necessidade:* Quer saber exatamente o que precisa fazer (tarefas) sem precisar ler uma ata de 5 páginas.

### Stakeholders
* **Diretor de TI:** Preocupa-se com a segurança dos dados, custos de infraestrutura e viabilidade de integração com ferramentas já existentes (SSO, Google Workspace, Jira).
* **Diretor de RH:** Focado na adesão da ferramenta pelos colaboradores e na redução do esgotamento causado pelo excesso de reuniões ("Zoom fatigue").

## 3. Justificativa Técnica das Decisões

A priorização do backlog do *NexusMeet* foi fundamentada em diretrizes de mitigação de riscos técnicos, entrega rápida de valor e gestão de escopo. Utilizou-se a técnica MoSCoW para separar estritamente o que é essencial para o funcionamento do fluxo principal (MVP) daquilo que representa melhorias incrementais ou desvios complexos de engenharia.

**1. Foco do Minimum Viable Product (Must Have):**
As histórias classificadas como "Must Have" formam o núcleo indissociável da proposta de valor. Sem o login seguro via SSO e a leitura de calendário, a funcionalidade principal de agendamento por IA seria impossível, pois o algoritmo depende do consumo de dados de disponibilidade. Da mesma forma, a gravação e a transcrição alimentam o modelo de linguagem que gera o resumo automatizado. Tecnicamente, este fluxo exige a integração com APIs de calendário e o uso de modelos de processamento de linguagem natural (NLP) em nuvem. Garantir essa infraestrutura é a prioridade zero do ciclo de desenvolvimento, validando o modelo de negócio imediatamente.

**2. Automação de Processos e Escalabilidade (Should Have):**
Funcionalidades como extração de tarefas e integração com o Jira adicionam alto valor, mas sua ausência não impede o uso primário do sistema. Elas requerem maior refinamento na lógica de *Machine Learning*, especialmente no reconhecimento de entidades nomeadas (NER) para associar comandos a usuários específicos. Foram priorizadas logo após o MVP pois atendem diretamente à dor de desenvolvedores e da gerência de TI, consolidando a plataforma como um *hub* de produtividade.

**3. Funcionalidades Acessórias (Could Have):**
Itens como exportação em PDF, comandos de voz estruturados e painéis gerenciais foram alocados como "Could Have". Do ponto de vista técnico, a criação de dashboards analíticos exige a implementação de um pipeline de dados secundário e ferramentas de visualização que consumiriam tempo de desenvolvimento na fase inicial. 

**4. Redução de Risco e Custo Operacional (Won't Have):**
Decisões drásticas foram tomadas para proteger o orçamento e o escopo. A escolha de **não** hospedar vídeos em infraestrutura própria elimina um custo massivo de servidores (armazenamento e processamento). O sistema atuará de forma *headless* com relação à infraestrutura de vídeo, delegando o streaming para plataformas terceiras consolidadas (Zoom/Teams) e focando apenas no processamento de texto. Similarmente, a tradução simultânea de áudio com baixa latência adicionaria uma complexidade proibitiva para esta fase, sendo postergada para futuros roadmaps.

---

## Execução da Sprint 1

**Duração da Sprint:** 2 Semanas (10 dias úteis)

### 1. Sprint Planning

**Objetivo da Sprint:**  
Estabelecer a infraestrutura inicial de acesso seguro ao sistema e a integração bidirecional com calendários corporativos, formando a base de dados estrutural indispensável para o futuro motor de agendamento por Inteligência Artificial.

**Histórias Selecionadas e Sprint Backlog:**  
Para atingir o objetivo, a equipa selecionou as tarefas fundamentais de maior risco técnico do MVP (Must Have), utilizando a sequência de *Fibonacci* para estimar os *Story Points* (SP).

| ID | História de Usuário | Critérios de Aceitação | Pontos (SP) |
| :--- | :--- | :--- | :--- |
| **US01** | Como utilizador, quero fazer login utilizando o SSO corporativo (Google/Microsoft) para aceder ao sistema com segurança. | 1. Autenticação via OAuth2.<br>2. Bloqueio se credenciais forem revogadas.<br>3. Criação de perfil no 1º login. | 5 SP |
| **US02** | Como utilizador, quero sincronizar a minha agenda profissional para que o sistema leia os meus horários livres. | 1. Sincronização bidirecional.<br>2. Atualização de status em tempo real. | 8 SP |
| **US06** | Como organizador, quero poder cancelar ou reagendar a reunião com um clique, notificando todos. | 1. Remoção automática nas agendas.<br>2. Disparo de e-mail de notificação. | 3 SP |
| **Total** | | | **16 SP** |

### 2. Definição de Pronto (Definition of Done - DoD)
Uma história de utilizador só é considerada "Pronta" na Sprint atual se cumprir todos os seguintes critérios:
* O código foi desenvolvido, revisto por pelo menos um colega (*Pull Request* aprovado) e fundido na ramificação principal.
* A cobertura de testes unitários da nova funcionalidade é superior a 80%.
* Todos os critérios de aceitação específicos da história foram validados e testados.
* A funcionalidade foi implementada e está operacional no ambiente de *Staging* (Homologação).
* Não existem defeitos (*bugs*) impeditivos conhecidos.

### 3. Registo da Execução da Sprint e Acompanhamento
A execução foi acompanhada diariamente (*Daily Scrum*) e o progresso foi registado no painel Kanban (GitHub Projects). O fluxo de trabalho decorreu da seguinte forma:
* **Dias 1 a 3:** Configuração da infraestrutura do projeto e implementação do *backend* para autenticação OAuth2 (US01).
* **Dias 4 a 5:** Finalização do *frontend* do ecrã de login e validação dos tokens de acesso. A **US01 foi movida para *Done*** no 5º dia.
* **Dias 6 a 8:** Foco intensivo na US02. A equipa enfrentou um desafio técnico com as permissões da Microsoft Graph API, o que exigiu investigação extra (*Spike*). A sincronização foi concluída e a **US02 movida para *Done*** no 8º dia.
* **Dia 9:** Implementação da lógica de exclusão de eventos e disparo de e-mails via SMTP (US06). Tarefa concluída rapidamente devido à arquitetura estabelecida nos dias anteriores. **US06 movida para *Done***.
* **Dia 10:** Testes finais de integração no ambiente de *Staging*, verificação da Definição de Pronto (DoD) e preparação para a *Review*.

### 4. Sprint Review
* **Participantes:** Equipa de Desenvolvimento, Product Owner e Diretor de TI (Stakeholder).
* **Resultados Apresentados:** A equipa demonstrou o acesso ao NexusMeet através de uma conta Google simulada, a importação instantânea da agenda e o cancelamento de um evento com notificação por e-mail recebida em tempo real.
* **Feedback e Aceitação:** O Diretor de TI aprovou a implementação da segurança OAuth2 (US01) e o desempenho da API de calendário (US02 e US06). Todas as histórias entregues cumpriram a DoD. O objetivo da Sprint foi considerado **100% atingido**.

### 5. Retrospectiva da Sprint
Realizada imediatamente após a *Review*, a equipa levantou os seguintes pontos para melhoria contínua:
* **O que correu bem:** A arquitetura do sistema provou ser escalável. A comunicação durante o bloqueio com a API da Microsoft foi rápida e eficiente.
* **O que pode ser melhorado:** O processo de implantação (*deploy*) para o ambiente de *Staging* foi manual e consumiu tempo desnecessário no Dia 10.
* **Plano de Ação para a Sprint 2:** A equipa técnica comprometeu-se a configurar um fluxo básico de CI/CD (Integração e Entrega Contínuas) através do GitHub Actions já no primeiro dia da próxima Sprint, para automatizar as implantações.

### 6. Métricas da Sprint: Velocity e Burndown
* **Velocity (Velocidade):** A equipa planeou e comprometeu-se com 16 *Story Points*. Todas as histórias foram concluídas. Portanto, o **Velocity atual da equipa é de 16 pontos**.
* **Gráfico de Burndown (Tabela de Registo de Queima):**

| Dia da Sprint | Pontos Restantes (Real) | Histórias Concluídas | Status |
| :---: | :---: | :--- | :--- |
| **Dia 0 (Início)** | 16 SP | Nenhuma | Planeamento concluído. |
| **Dia 3** | 16 SP | Nenhuma | Desenvolvimento em curso. |
| **Dia 5** | 11 SP | US01 concluída (-5 SP) | Login operante. |
| **Dia 8** | 3 SP | US02 concluída (-8 SP) | API de Calendário resolvida. |
| **Dia 9** | 0 SP | US06 concluída (-3 SP) | Notificações prontas. |
| **Dia 10 (Fim)** | **0 SP** | Revisão Final | **Meta Atingida.** |

---

## Gestão de Mudança (Change Request)

### 1. Requisito Original
* **ID da História:** `[US05] Geração de resumo automatizado por IA`
* **Descrição Original:** Como participante, quero receber um resumo gerado por IA logo após a reunião, para revisar as decisões tomadas.
* **Critérios de Aceitação Originais:**
  1. Resumo enviado em até 5 minutos após o fim da reunião.
  2. Separação visual por tópicos principais.
* **Prioridade e Estimativa Originais:** *Must Have* | 5 Story Points.

### 2. Mudança Solicitada
O Diretor de RH solicitou a inclusão obrigatória de um "Termómetro de Sentimento" nos resumos gerados. O sistema deverá analisar o tom da conversa (Positivo, Neutro, Negativo ou Tenso) e incluir esse indicador no cabeçalho do documento final.

### 3. Motivo da Mudança
A alteração visa atender a uma nova diretriz estratégica do departamento de Recursos Humanos focada na saúde mental corporativa. O objetivo é mapear equipas sob elevado nível de stress ou desgaste emocional crónico (*Zoom fatigue*), permitindo intervenções preventivas de gestão.

### 4. Análise de Impacto
* **Impacto Arquitetural e Técnico:** A inclusão da análise de sentimento exige uma instrução adicional (*prompt engineering*) no modelo de *Machine Learning* (LLM), o que aumentará o consumo de *tokens* (custo financeiro por API) em aproximadamente 15% por reunião.
* **Impacto no Desempenho (Performance):** A adição desta camada de processamento de texto implicará uma maior latência. O sistema não conseguirá garantir o envio do resumo no limite restrito de 5 minutos utilizando a infraestrutura de servidores orçamentada para o MVP.
* **Impacto no Esforço (Estimativas):** A complexidade da história aumenta, forçando a reavaliação da US05 de 5 para 8 Story Points.

### 5. Decisão Tomada e Justificativa Técnica
**Decisão:** A mudança foi **Aprovada com Condicionante de Escopo** (Renegociação).

**Justificativa:** O valor estratégico que a análise de sentimento acrescenta à plataforma para os decisores (RH) é imenso e alinha-se perfeitamente com a dor central do utilizador. No entanto, para absorver este novo requisito sem comprometer o orçamento do projeto com servidores de alta performance, a equipa técnica (juntamente com o *Product Owner*) decidiu flexibilizar o critério de aceitação de tempo de resposta. O envio do resumo passará de 5 para 10 minutos após a reunião, acomodando o tempo extra de processamento da IA.

### 6. Alterações Realizadas no Backlog
O cartão da `[US05]` no GitHub Projects foi atualizado para refletir o novo acordo:
* **Estimativa atualizada:** De 5 SP para 8 SP.
* **Critérios de Aceitação Atualizados:**
  1. Resumo enviado em até 10 minutos após o fim da reunião.
  2. Separação visual por tópicos principais.
  3. *(NOVO)* Inclusão de um indicador visual de "Clima da Reunião" (Positivo, Neutro, Negativo ou Tenso).

### 7. Rastreabilidade da Mudança

--- 

## Entrega 4: Requisitos Não Funcionais e Arquitetura

### 1. Requisitos Não Funcionais (RNFs) Levantados e Classificados

Os requisitos não funcionais abaixo foram definidos para garantir a estabilidade, a proteção e a eficiência da plataforma **NexusMeet**. Cada RNF descreve o que o sistema deve atingir, de forma mensurável e sem prescrever a tecnologia; o *como* está registrado nas decisões arquiteturais da Seção 3. Os requisitos estão classificados em cinco categorias de qualidade: Segurança, Desempenho, Usabilidade, Disponibilidade e Confiabilidade.

* **[RNF-01] Segurança (Autenticação):** O sistema deve delegar a autenticação dos usuários a provedores de identidade corporativos (IdP) por meio do protocolo OAuth2/OpenID Connect, sem armazenar senhas na base de dados local.
* **[RNF-02] Desempenho (Busca):** A pesquisa textual no histórico de reuniões (transcrições e resumos) deve retornar os resultados completos na interface do usuário em menos de 2 segundos.
* **[RNF-03] Desempenho (Processamento por IA):** O processamento do áudio e a devolução do resumo gerado por IA com análise de sentimento não devem exceder o tempo limite de 10 minutos após o término da reunião.
* **[RNF-04] Usabilidade (Ações rápidas):** O usuário deve conseguir cancelar ou reagendar uma reunião com um único clique, e o sistema deve exibir o resultado da ação (confirmação ou mensagem de erro) em até 1 segundo, em 95% das ocorrências.
* **[RNF-05] Segurança (Proteção de dados em repouso):** Todos os dados persistidos pela plataforma (banco de dados, transcrições, resumos, gravações de áudio, índice de busca e backups) devem ser armazenados criptografados com AES-256, com as chaves de criptografia mantidas separadas dos dados e rotacionadas no mínimo uma vez por ano.
* **[RNF-06] Disponibilidade:** A plataforma deve ter disponibilidade mensal mínima de 99,5% (no máximo cerca de 3 h 36 min de indisponibilidade em um mês de 30 dias), e a falha de um único componente não deve interromper o serviço.
* **[RNF-07] Confiabilidade:** Nenhum evento de término de reunião pode ser perdido, e falhas temporárias no processamento do resumo (por exemplo, indisponibilidade da API de IA) devem ser tratadas automaticamente por novas tentativas, de modo que ao menos 99% das reuniões encerradas tenham o resumo gerado com sucesso. Os dados devem ter backup diário, com perda máxima aceitável de 24 horas (RPO).

---

### 2. Relações de Rastreabilidade (RNF x Histórias de Usuário)

Para manter a consistência do backlog, cada RNF foi associado às histórias de usuário que ele afeta. A matriz indica o impacto principal (**Principal**), em que o RNF determina diretamente os critérios de aceitação da história, e o impacto secundário (**Secundário**), em que a história depende do RNF para funcionar corretamente.

| RNF | Categoria | US01 (Login via SSO corporativo) | US05 (Resumo automatizado por IA) | US06 (Cancelamento e reagendamento com um clique) | US07 (Busca de palavras-chave no histórico) |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **RNF-01** | Segurança (autenticação) | **Principal** | Secundário | Secundário | Secundário |
| **RNF-02** | Desempenho (busca) | — | Secundário | — | **Principal** |
| **RNF-03** | Desempenho (IA) | — | **Principal** | — | Secundário |
| **RNF-04** | Usabilidade | — | — | **Principal** | — |
| **RNF-05** | Segurança (dados em repouso) | Secundário | **Principal** | Secundário | **Principal** |
| **RNF-06** | Disponibilidade | **Principal** | Secundário | Secundário | Secundário |
| **RNF-07** | Confiabilidade | — | **Principal** | Secundário | Secundário |

**Justificativa dos vínculos:**
* **RNF-01:** Principal em US01 (fluxo de login via IdP); em US05, US06 e US07 o acesso exige um token válido emitido pelo IdP.
* **RNF-02:** Principal em US07 (tempo de busca); em US05, os resumos gerados precisam ser indexados para poderem ser encontrados.
* **RNF-03:** Principal em US05 (janela de 10 minutos); em US07, o conteúdo pesquisável só existe depois que o processamento termina.
* **RNF-04:** Principal em US06, cujo critério de aceitação é a ação em um clique com retorno visual em até 1 segundo.
* **RNF-05:** Principal em US05 (áudio, transcrições e resumos armazenados) e em US07 (o índice de busca contém o texto das reuniões); em US01 e US06 protege dados de perfil, sessão e agendamento.
* **RNF-06:** Principal em US01, pois sem o login nenhuma outra história é acessível; em US05, US06 e US07 a indisponibilidade impede o uso da funcionalidade.
* **RNF-07:** Principal em US05 (nenhum evento de fim de reunião pode ser perdido); em US06, as alterações de agenda devem ser gravadas de forma durável; em US07, o índice deve poder ser reconstruído a partir dos dados com backup.

---

### 3. Decisões Arquiteturais e Justificativas Técnicas

As restrições impostas pelos RNFs moldaram diretamente as decisões a seguir. Cada RNF é atendido por ao menos uma decisão arquitetural específica, conforme a tabela abaixo:

| Decisão | Tema | RNF atendido |
| :--- | :--- | :--- |
| **Decisão 1** | Delegação de Identidade (Federated Identity) | RNF-01 (Segurança - autenticação) |
| **Decisão 2** | Motor de Busca Indexada (Elasticsearch) | RNF-02 (Desempenho - busca) |
| **Decisão 3** | Processamento Assíncrono com Filas de Mensagens | RNF-03 (Desempenho - IA) |
| **Decisão 4** | Frontend SPA com atualização otimista | RNF-04 (Usabilidade) |
| **Decisão 5** | Criptografia em Repouso com Gerenciamento de Chaves (KMS) | RNF-05 (Segurança - dados em repouso) |
| **Decisão 6** | Alta Disponibilidade com Redundância e Failover | RNF-06 (Disponibilidade) |
| **Decisão 7** | Tolerância a Falhas no Processamento Assíncrono e Backups | RNF-07 (Confiabilidade) |

#### Decisão 1: Delegação de Identidade (Federated Identity)
* **Motivação:** Atender ao RNF-01 (Segurança - autenticação).
* **Justificativa:** Em vez de construir um sistema próprio de gestão de credenciais, o que aumentaria a superfície de ataque e exigiria conformidade pesada com regulamentações de proteção de dados, optou-se por utilizar o Microsoft Entra ID (antigo Azure Active Directory) e o Google Workspace Identity como provedores de identidade. Isso transfere a responsabilidade pela segurança da senha para a infraestrutura do cliente corporativo: quando um funcionário é desligado e sua conta é desativada no IdP, o NexusMeet deixa de receber tokens válidos para ele, e o acesso é encerrado, no máximo, quando expirar o token de acesso, configurado com validade curta (por exemplo, 15 minutos).

#### Decisão 2: Motor de Busca Indexada (Elasticsearch)
* **Motivação:** Atender ao RNF-02 (Desempenho – busca).
* **Justificativa:** Realizar consultas tradicionais (como `LIKE`) em bases de dados relacionais abrangendo milhares de linhas de texto (transcrições) degradaria a performance do sistema. A adoção de um motor de busca baseado em índice invertido (como Elasticsearch ou Algolia) é a decisão mais adequada para garantir a indexação eficiente e o tempo de resposta inferior a 2 segundos exigido pelo RNF-02. O índice é atualizado ao final do processamento de cada reunião (Decisão 3), de modo que transcrições e resumos se tornem pesquisáveis assim que ficam prontos.

#### Decisão 3: Processamento Assíncrono com Filas de Mensagens (Message Queues)
* **Motivação:** Atender ao RNF-03 (Desempenho – IA).
* **Justificativa:** O envio de grandes blocos de texto para APIs de Inteligência Artificial causa latência severa. Se o servidor principal aguardasse essa resposta, bloquearia os usuários. A decisão foi implementar uma arquitetura assíncrona baseada em mensageria: quando a reunião termina, o evento entra em uma fila e processadores em segundo plano (*workers*) geram o resumo dentro da janela de 10 minutos, sem afetar a estabilidade do servidor principal. Os *workers* podem ser escalados de forma independente, conforme o volume de reuniões encerradas.

#### Decisão 4: Arquitetura Frontend SPA (Single Page Application)
* **Motivação:** Atender ao RNF-04 (Usabilidade).
* **Justificativa:** O RNF-04 define o resultado esperado (ação em um clique, com retorno visual em até 1 segundo); a SPA é a solução adotada para alcançá-lo. A necessidade de ações fluidas ditou a separação total entre a interface (React ou Vue) e o servidor de dados (APIs RESTful). Nessa arquitetura, a interface aplica a atualização otimista: ao clicar em cancelar, o estado visual é atualizado instantaneamente enquanto a instrução é enviada ao servidor em segundo plano, sem recarregar a página. Se o servidor rejeitar a operação, a interface reverte a mudança e exibe uma mensagem de erro, mantendo o limite de 1 segundo para o retorno ao usuário.

#### Decisão 5: Criptografia em Repouso com Gerenciamento de Chaves (KMS)
* **Motivação:** Atender ao RNF-05 (Segurança - proteção de dados em repouso).
* **Justificativa:** Implementar AES-256 manualmente no código da aplicação aumentaria a complexidade e o risco de erros criptográficos. Optou-se por usar a criptografia em repouso nativa dos serviços gerenciados, com as chaves mestras em um serviço de gerenciamento de chaves (KMS), como AWS KMS, Azure Key Vault ou Google Cloud KMS, aplicando *envelope encryption*: cada dado é cifrado com uma chave de dados, que por sua vez é cifrada pela chave mestra mantida no KMS. Com isso, (i) as chaves ficam separadas dos dados; (ii) a rotação anual da chave mestra não exige recifrar todo o conteúdo; e (iii) o acesso às chaves é restrito pelo princípio do menor privilégio e auditado.

| Componente | Dados protegidos | Mecanismo (AES-256) |
| :--- | :--- | :--- |
| **Banco de dados relacional** | Identificadores de usuários, reuniões e agendamentos | Criptografia transparente do serviço gerenciado, com chave mestra no KMS |
| **Armazenamento de objetos** | Gravações de áudio e arquivos de transcrição | Criptografia no lado do servidor (SSE) com chave do KMS |
| **Índice de busca (Elasticsearch)** | Texto indexado de transcrições e resumos | Criptografia dos volumes e *snapshots* do *cluster*, com chave do KMS |
| **Backups e snapshots** | Cópias de todos os itens acima | Herdam a criptografia da origem; chaves gerenciadas no KMS |

Como a Decisão 2 replica o texto das transcrições no índice de busca, o índice também precisa ser cifrado; caso contrário, o conteúdo ficaria exposto em texto claro mesmo com o banco de dados protegido. Complementarmente, toda comunicação entre os componentes utiliza TLS 1.2 ou superior.

#### Decisão 6: Alta Disponibilidade com Redundância e Failover
* **Motivação:** Atender ao RNF-06 (Disponibilidade).
* **Justificativa:** Para atingir 99,5% de disponibilidade mensal, eliminam-se os pontos únicos de falha: (i) a API da aplicação é *stateless* e executa em no mínimo duas instâncias, em zonas de disponibilidade distintas, atrás de um balanceador de carga com verificação de saúde (*health checks*) que retira do tráfego as instâncias com falha; (ii) o banco de dados opera com réplica em espera e *failover* automático; (iii) o *cluster* de busca mantém ao menos uma réplica de cada *shard*; e (iv) os *workers* da fila são independentes e substituíveis individualmente. Em razão da Decisão 1, o login depende da disponibilidade do IdP corporativo, que está fora do controle da plataforma; as sessões já iniciadas continuam válidas até a expiração do token de acesso.

#### Decisão 7: Tolerância a Falhas no Processamento Assíncrono e Backups
* **Motivação:** Atender ao RNF-07 (Confiabilidade).
* **Justificativa:** Complementa a Decisão 3 para que o processamento assíncrono seja confiável: (i) a fila é durável, com mensagens persistidas em disco e removidas somente após a confirmação (*ack*) do *worker*, evitando a perda do evento de término de reunião; (ii) falhas temporárias, como indisponibilidade ou *timeout* da API de IA, disparam até 3 novas tentativas com espera progressiva (*backoff* exponencial), dimensionada para caber, sempre que possível, na janela de 10 minutos do RNF-03; (iii) as mensagens que esgotam as tentativas vão para uma fila de mensagens mortas (*Dead Letter Queue*), com alerta e reprocessamento posterior, e o usuário é notificado de que o resumo está atrasado; (iv) o processamento é idempotente, usando o identificador da reunião como chave, para que uma reentrega da mensagem não gere resumos duplicados; e (v) *backups* automáticos diários, com retenção de 30 dias, permitem a recuperação dos dados com perda máxima de 24 horas (RPO).

---

### 4. Histórico de Revisões

| Versão | Alterações |
| :--- | :--- |
| **1.0** | Versão original: 4 RNFs e 4 decisões arquiteturais. |
| **2.0** | (a) RNF-01 dividido: a proteção de dados em repouso (AES-256) passou a ser o RNF-05, com decisão arquitetural própria (Decisão 5).<br>(b) RNF-04 reescrito como requisito mensurável, sem citar tecnologia; a SPA permanece como solução na Decisão 4.<br>(c) Incluídos o RNF-06 (Disponibilidade) e o RNF-07 (Confiabilidade), com as Decisões 6 e 7.<br>(d) Matriz de rastreabilidade ampliada: cada RNF passou a ser ligado a mais de uma história de usuário (impacto principal e secundário) e a uma decisão arquitetural. |

#### Decisão 5: Criptografia em Repouso com Gerenciamento de Chaves (KMS)
* **Motivação:** Atender ao RNF-05 (Segurança - proteção de dados em repouso).
* **Justificativa:** Implementar AES-256 manualmente no código da aplicação aumentaria a complexidade e o risco de erros criptográficos[cite: 13]. Optou-se por usar a criptografia em repouso nativa dos serviços gerenciados, com as chaves mestras em um serviço de gerenciamento de chaves (KMS), como AWS KMS, Azure Key Vault ou Google Cloud KMS, aplicando *envelope encryption*: cada dado é cifrado com uma chave de dados, que por sua vez é cifrada pela chave mestra mantida no KMS. Com isso, (i) as chaves ficam separadas dos dados; (ii) a rotação anual da chave mestra não exige recifrar todo o conteúdo; e (iii) o acesso às chaves é restrito pelo princípio do menor privilégio e auditado.

| Componente | Dados protegidos | Mecanismo (AES-256) |
| :--- | :--- | :--- |
| **Banco de dados relacional** | Identificadores de usuários, reuniões e agendamentos[cit | Criptografia transparente do serviço gerenciado, com chave mestra no KMS[cite: 13] |
| **Armazenamento de objetos** | Gravações de áudio e arquivos de transcrição[cite: 13] | Criptografia no lado do servidor (SSE) com chave do KMS[cite: 13] |
| **Índice de busca (Elasticsearch)** | Texto indexado de transcrições e resumos[cite: 13] | Criptografia dos volumes e *snapshots* do *cluster*, com chave do KMS[cite: 13] |
| **Backups e snapshots** | Cópias de todos os itens acima[cite: 13] | Herdam a criptografia da origem; chaves gerenciadas no KMS[cite: 13] |

Como a Decisão 2 replica o texto das transcrições no índice de busca, o índice também precisa ser cifrado; caso contrário, o conteúdo ficaria exposto em texto claro mesmo com o banco de dados protegido[cite: 13]. Complementarmente, toda comunicação entre os componentes utiliza TLS 1.2 ou superior[cite: 13].

#### Decisão 6: Alta Disponibilidade com Redundância e Failover
* **Motivação:** Atender ao RNF-06 (Disponibilidade)[cite: 14].
* **Justificativa:** Para atingir 99,5% de disponibilidade mensal, eliminam-se os pontos únicos de falha: (i) a API da aplicação é *stateless* e executa em no mínimo duas instâncias, em zonas de disponibilidade distintas, atrás de um balanceador de carga com verificação de saúde (*health checks*) que retira do tráfego as instâncias com falha; (ii) o banco de dados opera com réplica em espera e *failover* automático; (iii) o *cluster* de busca mantém ao menos uma réplica de cada *shard*; e (iv) os *workers* da fila são independentes e substituíveis individualmente[cite: 14]. Em razão da Decisão 1, o login depende da disponibilidade do IdP corporativo, que está fora do controle da plataforma; as sessões já iniciadas continuam válidas até a expiração do token de acesso[cite: 14].

#### Decisão 7: Tolerância a Falhas no Processamento Assíncrono e Backups
* **Motivação:** Atender ao RNF-07 (Confiabilidade)[cite: 14].
* **Justificativa:** Complementa a Decisão 3 para que o processamento assíncrono seja confiável: (i) a fila é durável, com mensagens persistidas em disco e removidas somente após a confirmação (*ack*) do *worker*, evitando a perda do evento de término de reunião; (ii) falhas temporárias, como indisponibilidade ou *timeout* da API de IA, disparam até 3 novas tentativas com espera progressiva (*backoff* exponencial), dimensionada para caber, sempre que possível, na janela de 10 minutos do RNF-03; (iii) as mensagens que esgotam as tentativas vão para uma fila de mensagens mortas (*Dead Letter Queue*), com alerta e reprocessamento posterior, e o usuário é notificado de que o resumo está atrasado; (iv) o processamento é idempotente, usando o identificador da reunião como chave, para que uma reentrega da mensagem não gere resumos duplicados; e (v) *backups* automáticos diários, com retenção de 30 dias, permitem a recuperação dos dados com perda máxima de 24 horas.

---

### 4. Histórico de Revisões

| Versão | Alterações |
| :--- | :--- |
| **1.0** | Versão original: 4 RNFs e 4 decisões arquiteturais[cite: 14]. |
| **2.0** | (a) RNF-01 dividido: a proteção de dados em repouso (AES-256) passou a ser o RNF-05, com decisão arquitetural própria (Decisão 5)[cite: 14].<br>(b) RNF-04 reescrito como requisito mensurável, sem citar tecnologia; a SPA permanece como solução na Decisão 4[cite: 14].<br>(c) Incluídos o RNF-06 (Disponibilidade) e o RNF-07 (Confiabilidade), com as Decisões 6 e 7[cite: 14].<br>(d) Matriz de rastreabilidade ampliada: cada RNF passou a ser ligado a mais de uma história de usuário (impacto principal e secundário) e a uma decisão arquitetural[cite: 14]. |

--- 

## Entrega 5: Análise de Desempenho e Qualidade do Processo

**Integrantes do Grupo:** [Nome 1], [Nome 2], [Nome 3]

### 1. Métricas Coletadas e Dados das Sprints

A análise de desempenho do projeto NexusMeet baseou-se nos dados extraídos de duas Sprints completas de desenvolvimento.

**Tabela de Dados Consolidados:**

| Métrica | Sprint 1 | Sprint 2 | Variação |
| :--- | :---: | :---: | :---: |
| **Pontos Planejados** | 16 SP | 21 SP | +31.25% |
| **Pontos Entregues (Velocity)** | 16 SP | 13 SP | -18.75% |
| **Histórias Planejadas** | 3 | 4 | +1 |
| **Histórias Concluídas** | 3 | 2 | -1 |
| **Defeitos (Bugs) Reportados** | 1 | 4 | +300% |
| **Taxa de Conclusão** | 100% | 61.9% | -38.1% |

### 2. Análise da Velocity e Gráficos de Burndown

**Análise da Velocity:**
A *Velocity* da equipa demonstrou uma instabilidade considerável. Na Sprint 1, a equipa entregou os 16 Story Points planeados, atingindo uma taxa de sucesso de 100%. Encorajada por este resultado, a equipa assumiu 21 Story Points na Sprint 2. Contudo, apenas 13 pontos foram efetivamente entregues. Esta quebra de 18.75% na velocidade real, combinada com o aumento do volume de trabalho assumido, indica uma falha de planeamento (sobrecarga) e a necessidade de calibrar a capacidade produtiva da equipa em torno de uma média de 14 a 15 pontos por Sprint.

**Análise do Burndown:**
* **Burndown Sprint 1:** O gráfico apresentou uma quebra saudável em "escada", com entregas consistentes nos dias 5, 8 e 9, resultando em 0 pontos restantes no último dia. O fluxo de trabalho foi constante e alinhado com a linha ideal.
* **Burndown Sprint 2:** O gráfico evidenciou uma linha horizontal prolongada nos primeiros 7 dias, sem qualquer entrega de valor (*flatline*). Apenas no dia 8 ocorreu a primeira descida acentuada (entrega de 8 pontos). O término da Sprint com 8 pontos residuais comprova que as tarefas ficaram bloqueadas ou em fase de testes por demasiado tempo, sem chegar a *Done*.

### 3. Gargalos Identificados e Causas

A degradação das métricas na Sprint 2 permitiu a identificação de dois gargalos principais no processo:

1.  **Gargalo de *Deploy* e Testes (Ambiente de Staging):** A análise do Burndown (*flatline* inicial) revelou que as tarefas estavam terminadas a nível de código, mas bloqueadas na fase de implementação (*deploy*) no ambiente de testes.
    *   *Causa:* O processo de *deploy* manual exigia a intervenção de um único programador, criando um afunilamento de tarefas na coluna "Em Teste" do painel Kanban.
2.  **Aumento da Taxa de Defeitos (Bugs):** O aumento de 1 para 4 defeitos reportados na Sprint 2 causou retrabalho significativo.
    *   *Causa:* A pressão para entregar 21 pontos (sobrecarga) levou a uma redução no tempo dedicado à revisão de código (*Code Review*) e falhas na validação da "Definição de Pronto" (DoD).

### 4. Melhorias Aplicadas e Impacto

A partir da análise das métricas na Retrospectiva da Sprint 2, a equipa aplicou imediatamente as seguintes melhorias ao processo:

1.  **Implementação de CI/CD (Melhoria de Processo):** Para resolver o gargalo de *deploy*, a equipa configurou um fluxo (pipeline) básico no GitHub Actions. O *deploy* para o ambiente de *Staging* passou a ser automático sempre que um *Pull Request* é aprovado.
    *   *Impacto:* A automação eliminou a dependência manual, o que deverá suavizar o gráfico de Burndown na Sprint 3, permitindo entregas mais rápidas e contínuas ao longo dos dias.
2.  **Limite de WIP (Work in Progress):** A equipa estabeleceu um limite máximo de 2 tarefas em simultâneo na coluna "Em Desenvolvimento" e reforçou o cumprimento estrito da DoD, exigindo aprovação de dois pares antes de avançar qualquer código.
    *   *Impacto:* Esta limitação forçará a equipa a focar-se em terminar tarefas antes de iniciar novas (reduzindo o paralelismo excessivo), com a expectativa de baixar a taxa de defeitos para o padrão inicial da Sprint 1.

### 5. Relatório de Qualidade do Processo

A análise global revela que a equipa possui maturidade técnica para executar o desenvolvimento, mas enfrentou dificuldades operacionais típicas na gestão da capacidade produtiva. O processo Scrum provou a sua eficácia não por evitar erros, mas por tornar a disfunção da Sprint 2 perfeitamente visível e mensurável através da quebra da *Velocity* e do formato anómalo do *Burndown*. 

As decisões tomadas (automação de CI/CD e imposição de limites de WIP) baseiam-se em dados empíricos e endereçam diretamente as causas raiz identificadas. Conclui-se que a qualidade do processo de inspeção e adaptação é alta, garantindo que a infraestrutura metodológica da equipa está agora mais robusta e preparada para as iterações subsequentes.
