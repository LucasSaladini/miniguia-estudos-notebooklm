# 📘 Caderno Temático Inteligente: Arquitetura de Microservices com NotebookLM

## 📝 Contexto e Objetivos
Este repositório foi desenvolvido como projeto final para a DIO (Digital Innovation One). O objetivo principal é explorar as capacidades de curadoria, síntese e análise do **NotebookLM**, utilizando a IA como um assistente de estudo avançado para dominar os conceitos e desafios da **Arquitetura de Microservices**.

**Objetivos de Estudo:**
* Compreender a transição de arquiteturas monolíticas para microsserviços.
* Analisar as estratégias de comunicação (síncrona e assíncrona) e gerenciamento de dados distribuídos.
* Mapear os principais desafios de implementação (decomposição, resiliência e deploy).
* Validar a precisão do NotebookLM em extrair insights baseando-se estritamente nas fontes fornecidas.

[Link para o NotebookLM](https://notebooklm.google.com/notebook/c2220264-76ef-46aa-929f-ae81d031ea5f)
---

## 📚 Curadoria de Fontes
Para alimentar o NotebookLM e garantir respostas técnicas de alta qualidade, foram selecionadas as seguintes fontes abertas (salvas em PDF e carregadas na ferramenta):

1. **Martin Fowler - Microservices** ([Link para o artigo original](https://martinfowler.com/articles/microservices.html)).
2. **Saga Design Pattern - Azure Architecture Center | Microsoft Learn** ([Link para a documentação](https://learn.microsoft.com/azure/architecture/reference-architectures/saga/saga)).
3. **Top 10 Microservices Design Patterns And How To Choose - Octopus Deploy** ([Link para o guia](https://octopus.com/blog/top-10-microservices-design-patterns)).

---

## 🧠 Engenharia de Prompts e "Cicatrizes" (Troubleshooting)
O mercado valoriza o raciocínio por trás do resultado. Abaixo está a documentação de como os prompts foram refinados para extrair o melhor da IA, incluindo os erros e correções de rota.

### 🧪 Experimento 1: O Prompt Superficial vs. Refinado
* **Prompt Inicial (Ingênuo):** *"Me explica o que são microsserviços com base nos textos."*
* **Resultado da IA (A primeira "Cicatriz"):** A arquitetura de microsserviços é uma abordagem de desenvolvimento de software que decompõe uma aplicação única em uma suíte de pequenos serviços modulares. Cada um desses serviços opera em seu próprio processo e se comunica com os outros através de mecanismos leves, geralmente APIs HTTP (REST) ou barramentos de mensagens
* **Prompt Refinado (Engenharia de Prompt):** *"Agindo como um Arquiteto de Software Sênior, analise as fontes fornecidas e crie uma tabela comparativa entre Arquitetura Monolítica e Arquitetura de Microservices. A tabela deve conter os seguintes critérios: Escalabilidade, Deploy, Gerenciamento de Banco de Dados e Complexidade de Código. Adicione uma nota de rodapé citando qual das fontes aborda com mais detalhes a questão de dados."*
* **Resultado da IA:**

| Critério | Arquitetura Monolítica | Arquitetura de Microsserviços |
| :--- | :--- | :--- |
| **Escalabilidade** | **Escalabilidade Vertical ou por Replicação Total:** O sistema escala replicando toda a stack da aplicação em múltiplos servidores. Não é possível isolar partes específicas para escalar individualmente. | **Escalabilidade Horizontal Granular:** Permite escalar apenas os serviços que estão sob alta carga. Diferentes serviços podem ter demandas computacionais distintas e serem ajustados de forma independente. |
| **Deploy** | **Unidade Única:** O deploy é feito como um único executável lógico. Qualquer pequena alteração exige o rebuild e o redeploy de toda a aplicação, o que pode tornar os ciclos lentos e arriscados. | **Independente e Contínuo:** Cada serviço é uma unidade de implantação autônoma. Isso permite lançamentos mais frequentes e rápidos, reduzindo o risco de que uma falha em um deploy derrube todo o sistema. |
| **Gerenciamento de Banco de Dados** | **Centralizado e Compartilhado:** Utiliza geralmente um único banco de dados (muitas vezes relacional) para todo o sistema. As transações ACID garantem consistência forte de forma nativa. | **Descentralizado (Database per Service):** Cada serviço gerencia seus próprios dados. Isso promove a "Persistência Poliglota", mas exige o gerenciamento de consistência eventual e padrões como Sagas. |
| **Complexidade de Código** | **Menor Complexidade Inicial:** A lógica reside em um único processo, facilitando o desenvolvimento e testes iniciais. Contudo, pode degradar para um "monolito de lama" sem disciplina modular rigorosa. | **Alta Complexidade Distribuída:** Introduz desafios como latência de rede, falhas parciais e dificuldade em manter a consistência. Exige maturidade em DevOps, automação e observabilidade avançada. |

Nota de rodapé da IA: A questão de dados distribuídos e transações longas é abordada com maior profundidade na documentação do Azure Architecture Center (Microsoft Learn), que detalha especificamente o padrão Saga para mitigar a ausência de transações ACID locais.

### 🩹 Cicatrizes e Solução de Problemas (Troubleshooting)
* **O Desafio:** Durante os testes, o NotebookLM misturou conceitos gerais de internet com o que estava escrito especificamente nos PDFs sobre "Bounded Context".
* **A Solução:** Ajustei o prompt para incluir uma restrição severa de escopo: *"Utilize **apenas** o capítulo X da fonte Y para explicar o conceito de Bounded Context. Se a informação não estiver explicitamente no texto, responda que não encontrou."* Isso eliminou a alucinação da IA.

---

## 🎓 Miniguia de Estudo (Entrega Final)

### 📌 Resumos Estruturados
*(Gerado pelo NotebookLM e revisado por mim)*

* **O Princípio da Descentralização:** Diferente do monolito, cada microsserviço possui sua própria base de dados (Database-per-service), evitando o acoplamento, mas gerando o desafio de consistência eventual.
* **Comunicação entre Serviços:** O sucesso da arquitetura depende de APIs bem definidas (REST/gRPC) para comunicação síncrona e sistemas de mensageria (RabbitMQ/Kafka) para comunicação assíncrona baseada em eventos.

### 📖 Glossário de Conceitos Fundamentais

Abaixo estão os termos essenciais extraídos das fontes para rápida consulta, organizados em ordem alfabética:

#### 📂 Letras A - C

| Termo Técnico | Definição e Aplicação Prática |
| :--- | :--- |
| **ACID** | *(Atomicidade, Consistência, Isolamento e Durabilidade)*: Conjunto de propriedades que garantem que as transações de banco de dados sejam processadas de forma confiável. Em microsserviços, garantir ACID em múltiplos serviços é complexo, levando à adoção da consistência eventual. |
| **API Gateway** | Um ponto de entrada único para todos os clientes que gerencia o roteamento de requisições, composição de dados de múltiplos serviços e autenticação. |
| **Backends for Frontends (BFF)** | Padrão que propõe a criação de serviços de backend separados para diferentes tipos de clientes (como mobile e desktop) para otimizar a experiência do usuário. |
| **Bulkhead (Mampara)** | Padrão de resiliência que isola elementos de uma aplicação em "pools" para que, se um falhar, os outros continuem funcionando, evitando falhas em cascata. |
| **CAP (Teorema)** | Afirma que um sistema distribuído só pode garantir duas de três propriedades simultaneamente: Consistência (C), Disponibilidade (A) e Tolerância a Partições (P). |
| **Circuit Breaker (Disjuntor)** | Mecanismo que interrompe chamadas para um serviço que está falhando ou lento, protegendo o sistema de um colapso total e permitindo que o serviço recupere sua saúde. |
| **CQRS** | *(Command Query Responsibility Segregation)*: Padrão que separa as operações de leitura (Query) das operações de escrita (Command) em modelos de dados diferentes para otimizar performance e escalabilidade. |

---

#### 📂 Letras D - I

| Termo Técnico | Definição e Aplicação Prática |
| :--- | :--- |
| **Database per Service** | Princípio onde cada serviço possui e gerencia seu próprio banco de dados, garantindo o desacoplamento e permitindo o uso de tecnologias de armazenamento específicas para cada necessidade. |
| **Decomposição por Capacidade de Negócio** | Estratégia de dividir o sistema com base em funções de negócio (ex: pagamentos, inventário) em vez de camadas técnicas. |
| **Discovery (Descoberta de Serviço)** | Mecanismo automático onde as instâncias de serviços se registram e são localizadas dinamicamente dentro da rede, essencial em ambientes que escalam rapidamente. |
| **Eventual Consistency (Consistência Eventual)** | Modelo de dados onde não há garantia de que todos os nós verão o dado mais recente imediatamente, mas o sistema garante que, se não houver novas atualizações, todos os nós eventualmente se tornarão consistentes. |
| **gRPC** | Um framework de comunicação de alta performance que utiliza HTTP/2 e serialização binária (Protocol Buffers), sendo mais eficiente que o REST tradicional para comunicações internas. |
| **Infrastructure as Code (IaC)** | Abordagem para definir e gerenciar infraestrutura de rede e computação através de código fonte, permitindo automação e reprodutibilidade. |

---

#### 📂 Letras L - S

| Termo Técnico | Definição e Aplicação Prática |
| :--- | :--- |
| **Lei de Conway** | Observação de que o design dos sistemas de software acaba refletindo a estrutura de comunicação da organização que o criou. |
| **Microservice Premium** | O custo adicional em termos de complexidade operacional e de rede que uma organização paga ao escolher microsserviços em vez de um monolito. |
| **Monolito** | Estilo arquitetural onde toda a funcionalidade do sistema reside em um único executável lógico e processo. |
| **Observabilidade** | Capacidade de entender o estado interno de um sistema distribuído através de três pilares: Métricas, Logs e Rastreamento Distribuído (Tracing). |
| **Persistência Poliglota** | Prática de utilizar diferentes tecnologias de banco de dados (ex: SQL para transações e NoSQL para buscas) dentro da mesma aplicação, dependendo da necessidade de cada serviço. |
| **Saga (Padrão)** | Sequência de transações locais que coordena a consistência de dados entre múltiplos serviços. Se uma transação falha, a Saga executa transações compensatórias para desfazer as alterações anteriores. |
| **Service Mesh** | Camada de infraestrutura dedicada para gerenciar a comunicação serviço-a-serviço, geralmente usando proxies como Sidecars para tratar segurança, observabilidade e tráfego. |

---

#### 📂 Letras T - Z

| Termo Técnico | Definição e Aplicação Prática |
| :--- | :--- |
| **Transactional Outbox** | Padrão que garante a publicação confiável de eventos ao salvar a mensagem em uma tabela de "saída" no mesmo banco de dados da transação de negócio, evitando inconsistências por falhas de rede. |
| **You Build It, You Run It** | Filosofia de governança onde a equipe que desenvolve o serviço também é responsável por sua operação e suporte em produção, incentivando a qualidade e o contato direto com o usuário. |
| **Zero Trust** | Modelo de segurança que assume que a rede interna é tão insegura quanto a externa, exigindo autenticação e autorização rigorosas para cada interação entre serviços. |



### 🚀 Prompts Reutilizáveis para Revisões Futuras
Copie e cole estes prompts no NotebookLM sempre que precisar revisar este caderno temático:

1. **Para simular uma entrevista técnica:**
   > *"Com base nas fontes carregadas, aja como um tech lead me entrevistando para uma vaga de Engenheiro de Software. Faça 3 perguntas difíceis sobre os desafios de consistência de dados em microsserviços e avalie minhas respostas."*
2. **Para gerar um resumo rápido pós-estudo:**
   > *"Crie um sumário executivo em 5 bullet points focando exclusivamente nos antipadrões (erros comuns) de microsserviços citados nos textos."*
