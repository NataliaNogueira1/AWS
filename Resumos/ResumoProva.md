# 📚 GUIA DE REVISÃO — AWS Academy Cloud Developing

> Material de revisão completo para prova teórica. Baseado nos 14 módulos do curso AWS Academy Cloud Developing + Projetos Práticos.

---

## 📋 Sumário

- [1. Resumo](#1-resumo)
- [2. Revisão Completa](#2-revisão-completa)
- [3. Tabelas Comparativas](#3-tabelas-comparativas)
- [4. Decore Antes da Prova](#4-decore-antes-da-prova)
---

## 1. RESUMO

### 1.1 Desenvolvimento na AWS (Módulo 2)

**Conceito:** O ciclo de vida de desenvolvimento de sistemas (SDLC) possui 6 fases: Planejar, Definir, Projetar, Desenvolver, Implantar e Manter.

**Definição:** Existem 3 formas de interagir com as APIs da AWS: Console de Gerenciamento, AWS CLI e AWS SDKs.

**O que costuma ser cobrado:**
- Fases do SDLC
- AWS CloudShell herda credenciais do console
- Amazon Q Developer é um assistente de codificação com IA generativa
- APIs de recursos fornecem abstração de nível mais alto que APIs de clientes de serviço
- Região é definida ao instanciar o cliente de serviço no SDK
- Código de resposta HTTP 400 series = erro do cliente

---

### 1.2 Amazon S3 — Armazenamento (Módulo 3)

**Conceito:** Serviço de armazenamento de objetos escalável com durabilidade de 11 noves.

**Definição:** Bucket organiza o namespace no nível mais alto. Nomes são globalmente únicos.

**O que costuma ser cobrado:**
- Bucket = container lógico; Objeto = arquivo armazenado
- Versionamento: uma vez ativado, NÃO pode ser desativado (apenas suspenso)
- Maior objeto em um único PUT: 5 GB
- URL virtual-hosted-style: `https://bucket.s3-website-region.amazonaws.com`
- Proteção contra exclusão acidental: habilitar versionamento
- URL pré-assinada: acesso temporário sem credenciais AWS
- Criptografia em trânsito: SSL/TLS
- CORS necessário para acessar objetos de outro bucket em site estático
- Política IAM (recomendação AWS) para conceder permissões ao bucket

---

### 1.3 IAM — Segurança (Módulo 4)

**Conceito:** Serviço que controla autenticação e autorização de acesso aos recursos AWS.

**Definição:** Modelo de Responsabilidade Compartilhada — AWS cuida da segurança DA nuvem; cliente cuida da segurança NA nuvem.

**O que costuma ser cobrado:**
- Cliente é responsável por: configuração de Security Group e dados do lado do cliente
- IAM Policy = documento JSON que concede/nega permissões
- Autenticação = verificação de identidade; Autorização = verificação de permissões
- Credenciais para console: username + password; para API: Access Key + Secret Key
- Recomendação para EC2: criar IAM Role e associar à instância (NÃO usar Access Key)
- Formato de policies: JSON
- Policy anexada a grupo = Identity-based (baseada em identidade)
- Princípio do menor privilégio
- Deny explícito SEMPRE sobrepõe Allow
- Por padrão, todas as requisições são negadas

---

### 1.4 DynamoDB — NoSQL (Módulo 5)

**Conceito:** Banco de dados chave-valor e documento que escala horizontalmente.

**Definição:** Tabela composta por Items (linhas) com Attributes (colunas). Partition Key obrigatória, Sort Key opcional.

**O que costuma ser cobrado:**
- Partition Key = define partição física do dado
- Sort Key = ordena itens dentro da mesma partição
- Índice Secundário Global (GSI): para consultar por atributos diferentes da PK
- Transações DynamoDB: operações "tudo ou nada"
- DynamoDB Streams: captura mudanças na tabela (pode acionar Lambda)
- Global Tables: replicação automática multi-região
- Point-in-time recovery: restauração dos últimos 35 dias
- API Control Operations: criar e gerenciar tabelas

---

### 1.5 API Gateway — REST APIs (Módulo 6)

**Conceito:** Serviço gerenciado para criar, publicar, manter, monitorar e proteger APIs.

**Definição:** Atua como "porta de entrada" para backends (Lambda, HTTP, serviços AWS).

**O que costuma ser cobrado:**
- RESTful API = segue princípios do Representational State Transfer
- WebSocket APIs: para aplicações real-time (chat)
- HTTP APIs: proxy simples para Lambda
- HTTP proxy integration: direciona rota para recurso na internet
- Mapping templates: transformam request antes de enviar ao backend
- URI base gerada contém: Region e Stage name
- Stage variables: conectam stages diferentes a backends diferentes
- Proteção contra SQL injection/XSS: usar AWS WAF com API Gateway
- Métrica Integration Latency: mede responsividade do backend
- Ambientes dev/prod: usar stage variables com aliases do Lambda

---

### 1.6 AWS Lambda — Serverless (Módulo 7)

**Conceito:** Computação serverless orientada a eventos. Executa código sem gerenciar servidores.

**Definição:** Lambda roda código SOMENTE quando ativado por evento e usa apenas os recursos necessários.

**O que costuma ser cobrado:**
- Burst quota: restrição que NÃO pode ser modificada
- API Gateway invoca Lambda de forma SÍNCRONA
- Execution Role: define permissões que a função Lambda tem (ex: escrever no DynamoDB)
- Function handler: ponto de entrada que Lambda chama para executar
- Provisioned concurrency: resolve problema de cold start
- Destinations e Async invocations: gerenciam erros em invocações assíncronas
- Deploy package > 50MB: fazer upload para S3 e referenciar
- ARN com alias (ex: :PROD): invoca a versão associada ao alias
- AWS X-Ray: usar service map para localizar erros visualmente
- Timeout máximo: 15 minutos

---

### 1.7 Containers (Módulo 8)

**Conceito:** Containers empacotam aplicação + dependências em unidade portátil e isolada.

**Definição:** Container é uma instância executável de uma imagem. Cada instrução no Dockerfile cria uma camada read-only.

**O que costuma ser cobrado:**
- Benefício de containers: abstração do que está sendo "enviado" aumenta agilidade
- Componentes de container: Runtime engine + Application code
- `docker run --name my_app_1 node_app`: cria container nomeado
- Cada instrução no Dockerfile cria uma camada read-only
- Razão para containers em microsserviços: cada container pode usar linguagem/tecnologia ideal
- Container orchestration: agendar starts/stops e determinar onde colocar containers
- Amazon ECS: serviço de orquestração altamente escalável que suporta Docker
- Elastic Beanstalk: simplifica deploy de containers (Application = coleção lógica)
- Canary testing no Beanstalk: usar Traffic Splitting
- Elastic Beanstalk usa CloudFormation por baixo

---

### 1.8 Caching — ElastiCache e CloudFront (Módulo 9)

**Conceito:** Caching armazena dados frequentemente acessados em camada mais rápida para reduzir latência.

**Definição:** ElastiCache = cache in-memory (Redis/Memcached). CloudFront = CDN com edge locations.

**O que costuma ser cobrado:**
- Considerar tolerância a dados desatualizados ao decidir onde cachear
- ElastiCache for Redis: suporta read replicas, key-value in-memory
- Responsabilidade do dev: escrever código que busca no cache e, se não encontrar, busca na origem
- Conexão ao ElastiCache: via endpoint único
- CloudFront: serve conteúdo estático de edge locations próximas ao usuário
- Cache hit ratio: incluir apenas valores mínimos necessários na cache key
- Expiração de arquivo: após expirar, CloudFront encaminha request ao origin server
- CloudFront Functions: redirecionamentos e custom response headers
- Lazy loading: evita encher cache com dados não requisitados
- Caching em múltiplas camadas melhora frontend e backend

---

### 1.9 Mensageria — SQS e SNS (Módulo 10)

**Conceito:** Serviços de desacoplamento que permitem comunicação assíncrona entre componentes.

**Definição:** SQS = fila de mensagens (consumers fazem poll). SNS = pub/sub (mensagens são pushed para subscribers).

**O que costuma ser cobrado:**
- Message queue: consumers fazem POLL na fila
- Pub/sub (SNS): nova mensagem é PUSHED para todos os subscribers
- SQS ReceiveMessage com MaxNumberOfMessages: recupera até N mensagens por vez
- Mensagens processadas mais de uma vez: AUMENTAR visibility timeout
- Dead-letter queue com maxReceiveCount baixo: reduz impacto de mensagens com falha
- Short polling: SQS amostra subconjunto de servidores
- SNS Topic: ponto de acesso lógico (canal de comunicação)
- Filter policy: filtra mensagens para subscriber específico (reduz custos)
- Kinesis Producer Library (KPL): para colocar registros em data stream
- Kinesis Data Streams: registros distribuídos em shards
- FIFO SQS queue: garante processamento em ordem (não standard queue)

---

### 1.10 Step Functions — Orquestração (Módulo 11)

**Conceito:** Serviço de coordenação de tarefas que permite construir workflows visuais com estados.

**Definição:** Orquestra múltiplas funções Lambda dependentes entre si em fluxos de trabalho.

**O que costuma ser cobrado:**
- Caso de uso: funções Lambda dependentes entre si
- Benefício: construir workflows visuais
- Task state: executa uma unidade de trabalho
- Choice state: lógica condicional (if/else)
- Map state: executa mesma função para cada item de uma lista
- Parallel state: executa verificações independentes em paralelo
- Succeed e Fail states: NÃO incluem campo Next
- Task Token: retornado por GetActivityTask, usado em SendTaskSuccess
- Express workflows: alta taxa de eventos (IoT)
- Integração com API Gateway para expor workflows como APIs

---

### 1.11 Segurança de Aplicações — Cognito e STS (Módulo 12)

**Conceito:** Serviços para autenticação de usuários, gerenciamento de sessões e proteção de aplicações.

**Definição:** Cognito = sign-up/sign-in para apps. STS = credenciais temporárias. ACM = gerencia certificados.

**O que costuma ser cobrado:**
- SSL e TLS: ambos criptografam comunicações de rede
- Certificate Authority (CA): responsável por emitir certificados
- ACM: gerencia renovação de certificados públicos E privados
- Best practice: usar IAM Roles para obter credenciais temporárias
- STS com federated users: primeira autenticação contra IdP externo
- STS com IAM users: primeira autenticação contra IAM
- CloudTrail: investigar quem deletou objetos do S3
- Cognito User Pool: sign-up e sign-in
- Compromised credentials check: reduz risco de senhas reutilizadas
- Cognito Identity Pool: credenciais temporárias limitadas para acessar serviços AWS
- Cognito + API Gateway: user pool retorna JWTs para o app
- Post-authentication event: invocar Lambda (não API Gateway) para log de eventos

---

### 1.12 CI/CD — Deploy Automatizado (Módulo 13)

**Conceito:** DevOps remove barreiras entre desenvolvimento e operações para otimizar produtividade.

**Definição:** CI/CD automatiza build, teste e deploy de aplicações.

**O que costuma ser cobrado:**
- DevOps: remover barreiras entre dev e ops
- CI: merge de código + testes automatizados obrigatórios
- CodePipeline: automatiza steps de release baseado em modelo definido
- CloudFormation template: seção Resources define recursos AWS
- Conditions section: controla criação condicional de recursos (test vs prod)
- CloudFormation stack: unidade de deployment
- Serverless deploy: não pode replicar ambiente de produção localmente
- SAM template vs CloudFormation: SAM tem seção Globals exclusiva
- `AWS::Serverless::SimpleTable` no SAM = cria tabela DynamoDB

---
---

## 2. REVISÃO COMPLETA

### 2.1 Desenvolvimento na AWS e SDKs

**O que é:** Conjunto de ferramentas e práticas para desenvolver aplicações que interagem com serviços AWS.

**Para que serve:** Criar, testar e implantar aplicações na nuvem AWS de forma programática.

**Principais características:**
- SDLC: Planejar → Definir → Projetar → Desenvolver → Implantar → Manter
- 3 formas de interação: Console, CLI, SDKs
- AWS CloudShell: terminal no browser que herda credenciais do console
- Amazon Q Developer: assistente de codificação com IA generativa
- SDKs disponíveis: Python (Boto3), Java, .NET, JavaScript, Go, etc.
- APIs de recursos: abstração de alto nível sobre APIs de clientes de serviço

**Vantagens:** Automação, reprodutibilidade, integração com CI/CD

**Limitações:** Curva de aprendizado dos SDKs, necessidade de gerenciar credenciais

**Serviços relacionados:** CloudShell, Cloud9, CodeCommit, CodeBuild, CodePipeline

**Exemplo prático:**
```python
import boto3
s3 = boto3.client('s3', region_name='us-east-1')
response = s3.list_objects_v2(Bucket='meu-bucket')
```

---

### 2.2 Amazon S3 (Simple Storage Service)

**O que é:** Serviço de armazenamento de objetos com escalabilidade praticamente ilimitada.

**Para que serve:** Data lakes, backups, hospedagem de sites estáticos, armazenamento de mídia.

**Principais características:**
- Bucket: container lógico (nome globalmente único)
- Objeto: arquivo + metadados (até 5 TB, PUT único até 5 GB)
- 8 classes de armazenamento (Standard, IA, Glacier, etc.)
- Versionamento: protege contra exclusão acidental (não pode ser desativado após ativado)
- URL pré-assinada: acesso temporário sem credenciais
- Criptografia em trânsito (SSL/TLS) e em repouso (SSE-S3, SSE-KMS)
- CORS: necessário para acesso cross-origin
- URI de objeto: `https://nome-bucket.s3.amazonaws.com/nome-objeto`

**Vantagens:** Durabilidade 11 noves, escalabilidade ilimitada, integração nativa

**Limitações:** Não é filesystem, latência maior que EBS, nomes globalmente únicos

**Serviços relacionados:** CloudFront, IAM, Lambda, Athena, Glacier

**Exemplo prático (do curso):**
```bash
aws s3 ls s3://nome-do-bucket
aws s3 cp arquivo.txt s3://nome-do-bucket/
```
```python
import boto3
s3 = boto3.client('s3')
response = s3.list_objects_v2(Bucket='nome-do-bucket')
for obj in response['Contents']:
    print(obj['Key'])
```

---

### 2.3 IAM (Identity and Access Management)

**O que é:** Serviço que gerencia identidades e permissões de acesso aos recursos AWS.

**Para que serve:** Controlar quem (autenticação) pode fazer o quê (autorização) nos recursos.

**Principais características:**
- Users: identidades com credenciais permanentes (console: user+pass; API: access key)
- Groups: coleção de users com policies compartilhadas
- Roles: identidades temporárias assumíveis por serviços/users
- Policies: documentos JSON (Effect, Action, Resource)
- Instance Profile: permite EC2 assumir Role
- Lógica de avaliação: Deny explícito > Allow > Deny implícito (padrão)

**Vantagens:** Controle granular, sem custo, MFA, federação

**Limitações:** Complexidade em ambientes grandes, limite de 5.000 users/conta

**Serviços relacionados:** Todos (IAM é transversal), STS, Cognito, Organizations

**Modelo de Responsabilidade Compartilhada:**
| AWS é responsável por | Cliente é responsável por |
|----------------------|--------------------------|
| Hardware, rede, data centers | Dados do cliente |
| Infraestrutura global | Configuração de Security Groups |
| Serviços gerenciados | IAM (users, groups, roles, policies) |
| Patches do hypervisor | Patches do SO (em EC2) |

---

### 2.4 Amazon DynamoDB

**O que é:** Banco de dados NoSQL totalmente gerenciado, chave-valor e documento.

**Para que serve:** Aplicações de alta escala com acesso por chave (gaming, IoT, sessões, catálogos).

**Principais características:**
- Partition Key (PK): obrigatória, define partição física
- Sort Key (SK): opcional, ordena dentro da partição
- Global Secondary Index (GSI): consulta por atributos diferentes da PK/SK
- Local Secondary Index (LSI): mesma PK, SK diferente
- Transações: operações atômicas "tudo ou nada"
- DynamoDB Streams: captura mudanças (Keys only, New image, Old image, New+Old)
- Global Tables: replicação multi-região automática
- Point-in-time recovery: últimos 35 dias
- TTL: expiração automática de itens

**Vantagens:** Latência single-digit ms, escala automática, totalmente gerenciado

**Limitações:** Sem JOINs, item máximo 400 KB, modelagem orientada a acesso

**Serviços relacionados:** Lambda, API Gateway, Streams, S3, Kinesis

---

### 2.5 Amazon API Gateway

**O que é:** Serviço gerenciado para criar, publicar e proteger APIs REST, HTTP e WebSocket.

**Para que serve:** Expor backends (Lambda, HTTP, serviços AWS) como APIs para clientes.

**Principais características:**
- REST API: completa, com validação, transformação, cache
- HTTP API: mais simples e barata, proxy para Lambda
- WebSocket API: comunicação bidirecional real-time
- Stages: ambientes (dev, staging, prod) com URLs diferentes
- Stage variables: parametrizam integração por stage
- Mapping templates: transformam request/response
- Integrations: Lambda proxy, HTTP proxy, AWS service
- Throttling: proteção contra excesso de requisições
- Timeout: máximo 29 segundos

**Vantagens:** Totalmente gerenciado, escala automática, monitoramento CloudWatch

**Limitações:** Timeout 29s, payload 10 MB, custo por requisição

**Serviços relacionados:** Lambda, IAM, Cognito, WAF, CloudWatch, X-Ray

---

### 2.6 AWS Lambda

**O que é:** Computação serverless que executa código em resposta a eventos.

**Para que serve:** APIs, processamento de eventos, ETL, automação, backends mobile.

**Principais características:**
- Event-driven: executa SOMENTE quando ativado
- Invocação síncrona (API Gateway) e assíncrona (S3, SNS)
- Execution Role: permissões que a função tem para acessar outros serviços
- Function handler: ponto de entrada da execução
- Aliases e versões: gerenciam deploys (ex: PROD, DEV)
- Provisioned concurrency: elimina cold start
- Destinations: roteamento de resultados (sucesso/falha)
- Layers: bibliotecas compartilhadas entre funções
- Timeout: máximo 15 minutos
- Memória: 128 MB a 10.240 MB
- Deploy package: até 50 MB (zip) ou via S3 para pacotes maiores

**Vantagens:** Zero gerenciamento, escala de 0 a milhares, paga por uso

**Limitações:** Cold start, timeout 15 min, stateless, burst quota não modificável

**Serviços relacionados:** API Gateway, DynamoDB, S3, SQS, SNS, EventBridge, X-Ray

---

### 2.7 Containers e Serviços de Container

**O que é:** Tecnologia que empacota aplicação + dependências em unidade portátil e isolada.

**Para que serve:** Microsserviços, portabilidade, deploy consistente, isolamento de processos.

**Principais características:**
- Container = instância executável de uma imagem
- Imagem = template imutável com camadas read-only
- Dockerfile: cada instrução cria uma camada
- Docker CLI: `docker build`, `docker run`, `docker ps`
- Amazon ECS: orquestração de containers (Task Definition, Cluster, Service)
- Amazon ECR: registry privado de imagens Docker
- AWS Fargate: execução serverless de containers (sem gerenciar EC2)
- Elastic Beanstalk: deploy simplificado (Application > Environment)

**Vantagens:** Portabilidade, isolamento, inicialização rápida, microsserviços

**Limitações:** Persistência requer volumes, kernel compartilhado, complexidade de orquestração

**Serviços relacionados:** ECS, EKS, ECR, Fargate, Elastic Beanstalk, EC2

**Deploy no Beanstalk:**
| Política | Descrição |
|----------|-----------|
| All at once | Atualiza tudo de uma vez (downtime) |
| Rolling | Atualiza em lotes |
| Immutable | Cria novas instâncias |
| Traffic Splitting | Canary testing |

---

### 2.8 Caching — ElastiCache e CloudFront

**O que é:** Estratégia de armazenar dados frequentemente acessados em camada mais rápida.

**Para que serve:** Reduzir latência, aliviar pressão no banco de dados, melhorar performance.

**Principais características:**

**Amazon ElastiCache:**
- In-memory key-value store (Redis ou Memcached)
- Redis: suporta read replicas, persistência, pub/sub
- Memcached: mais simples, multi-threaded
- Conexão via endpoint único
- Responsabilidade do dev: lógica de cache-aside (buscar no cache → se miss → buscar na origem)

**Amazon CloudFront:**
- CDN (Content Delivery Network) global
- Edge locations próximas ao usuário
- Cache de conteúdo estático e dinâmico
- Cache key: incluir apenas valores mínimos necessários
- Expiração: após expirar, CloudFront consulta origin server
- CloudFront Functions: lógica leve no edge (redirects, headers)
- Lambda@Edge: lógica mais complexa no edge

**Estratégias de caching:**
- Lazy loading: carrega no cache apenas quando requisitado (evita dados desnecessários)
- Write-through: escreve no cache ao escrever na origem (dados sempre atualizados)
- TTL (Time to Live): define expiração dos dados em cache

---

### 2.9 Mensageria — SQS e SNS

**O que é:** Serviços de comunicação assíncrona para desacoplar componentes de aplicações.

**Para que serve:** Desacoplamento, resiliência, processamento assíncrono, fan-out.

**Amazon SQS (Simple Queue Service):**
- Fila de mensagens: consumers fazem POLL
- Standard queue: entrega at-least-once, sem ordem garantida
- FIFO queue: entrega exactly-once, ordem garantida
- Visibility timeout: tempo que mensagem fica invisível após ser lida
- Dead-letter queue (DLQ): mensagens que falharam N vezes (maxReceiveCount)
- Long polling vs Short polling: long polling reduz custos (espera mensagens)
- Short polling: amostra subconjunto de servidores

**Amazon SNS (Simple Notification Service):**
- Pub/sub: mensagens pushed para todos os subscribers
- Topic: ponto de acesso lógico (canal de comunicação)
- Subscribers: Lambda, SQS, HTTP, email, SMS
- Filter policy: filtra mensagens por atributos para subscribers específicos

**Amazon Kinesis:**
- Data Streams: ingestão de dados em tempo real
- Dados distribuídos em shards
- Kinesis Producer Library (KPL): para produzir registros
- Mantém ordem dentro de um shard

---

### 2.10 AWS Step Functions

**O que é:** Serviço de orquestração serverless que coordena múltiplos serviços AWS em workflows visuais.

**Para que serve:** Coordenar funções Lambda dependentes, processos de aprovação, pipelines de dados.

**Principais características:**
- State Machine: define o workflow completo
- Estados (States):
  - **Task**: executa unidade de trabalho (Lambda, ECS, etc.)
  - **Choice**: lógica condicional (if/else)
  - **Parallel**: executa branches em paralelo
  - **Map**: itera sobre lista de itens
  - **Wait**: pausa por tempo definido
  - **Succeed**: encerra com sucesso (sem Next)
  - **Fail**: encerra com falha (sem Next)
- Standard workflows: longa duração (até 1 ano), exactly-once
- Express workflows: alta taxa de eventos, curta duração (até 5 min)
- Task Token: para aprovações manuais (callback pattern)
- Integração com API Gateway para expor como API

**Vantagens:** Visual, auditável, retry automático, error handling

**Limitações:** Custo por transição de estado, complexidade para workflows simples

**Serviços relacionados:** Lambda, API Gateway, DynamoDB, SQS, SNS, ECS

---

### 2.11 Segurança de Aplicações (Cognito, STS, ACM)

**O que é:** Conjunto de serviços para autenticação de usuários finais, gerenciamento de certificados e credenciais temporárias.

**Para que serve:** Sign-up/sign-in de usuários, proteção de APIs, comunicação segura.

**Amazon Cognito:**
- User Pool: diretório de usuários (sign-up, sign-in, MFA)
- Identity Pool: credenciais temporárias AWS para usuários autenticados
- Compromised credentials check: detecta senhas vazadas
- Integração com API Gateway: retorna JWTs
- Post-authentication trigger: invocar Lambda após login

**AWS STS (Security Token Service):**
- Emite credenciais temporárias (access key + secret key + session token)
- Federated users: autenticação inicial contra IdP externo
- IAM users: autenticação inicial contra IAM
- AssumeRole: permite assumir roles cross-account

**AWS Certificate Manager (ACM):**
- Gerencia certificados SSL/TLS
- Renovação automática de certificados públicos e privados
- SSL e TLS: ambos criptografam comunicações de rede

**AWS CloudTrail:**
- Registra todas as chamadas de API na conta
- Investigar quem deletou objetos, quem acessou recursos

---

### 2.12 CI/CD e Deploy (CloudFormation, SAM, CodePipeline)

**O que é:** Práticas e ferramentas para automatizar build, teste e deploy de aplicações.

**Para que serve:** Entregas frequentes, confiáveis e reproduzíveis.

**DevOps:**
- Filosofia: remover barreiras entre desenvolvimento e operações
- CI: merge frequente + testes automatizados obrigatórios
- CD: deploy automatizado após testes passarem

**AWS CodePipeline:**
- Orquestra pipeline CI/CD completo
- Source → Build → Test → Deploy
- Integra com CodeCommit, CodeBuild, CodeDeploy

**AWS CloudFormation:**
- Infraestrutura como Código (IaC)
- Template YAML/JSON com seções: Resources, Parameters, Conditions, Outputs
- Stack: unidade de deployment (cria/atualiza/deleta recursos juntos)
- Conditions: criação condicional de recursos (test vs prod)

**AWS SAM:**
- Extensão do CloudFormation para serverless
- Seção Globals: exclusiva do SAM (configurações compartilhadas)
- `AWS::Serverless::Function` = Lambda
- `AWS::Serverless::SimpleTable` = DynamoDB
- `AWS::Serverless::Api` = API Gateway
- Comandos: `sam init`, `sam build`, `sam local invoke`, `sam deploy`
- Não pode replicar ambiente de produção localmente (diferença de server-based)

---

### 2.13 EC2 e Docker (Projetos Práticos)

**O que é:** EC2 fornece servidores virtuais; Docker permite rodar containers neles.

**Para que serve:** Hospedar aplicações containerizadas acessíveis pela internet.

**Fluxo prático:**
1. Criar instância EC2 Amazon Linux
2. Instalar Docker: `sudo yum install docker`
3. Iniciar serviço: `sudo systemctl start docker`
4. Habilitar no boot: `sudo systemctl enable docker`
5. Adicionar user ao grupo: `sudo usermod -aG docker $USER`
6. Construir imagem: `docker build -t app .`
7. Rodar container: `docker run -p 80:80 app`
8. Liberar porta 80 no Security Group (Inbound Rules)

**Dockerfile exemplo:**
```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package.json .
COPY server.js .
EXPOSE 80
CMD ["npm","start"]
```

---

### 2.14 VPC (Virtual Private Cloud) — Projeto Prático

**O que é:** Rede virtual isolada na AWS com controle total sobre endereçamento IP.

**Para que serve:** Isolar recursos, controlar tráfego, definir topologia de rede.

**Componentes:**
- VPC: bloco CIDR (ex: 10.0.0.0/16)
- Subnet: subdivisão (pública ou privada)
- Internet Gateway: acesso bidirecional à internet
- NAT Gateway: acesso de saída para sub-redes privadas
- Route Table: direciona tráfego
- Security Group: firewall stateful (nível instância)
- Network ACL: firewall stateless (nível sub-rede)

**Tabela CIDR:**
| Prefixo | Máscara | Hosts |
|---------|---------|-------|
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /29 | 255.255.255.248 | 6 |
| /30 | 255.255.255.252 | 2 |

**Regras importantes:**
- AWS reserva 5 IPs por sub-rede
- Subnet pública: tem rota para Internet Gateway
- Subnet privada: usa NAT Gateway (que fica na subnet pública)
- Toda subnet precisa de Route Table (rota local + gateway)
- Bucket S3 NÃO fica dentro de VPC
- IPv4: parte de rede + parte de host
- VPC Only: cria apenas a VPC sem sub-redes/IGW/routes (configuração manual)

---

### 2.15 IoT, Grafana e Node-RED (Projetos Práticos)

**O que é:** Stack para coleta, armazenamento e visualização de dados IoT.

**Para que serve:** Monitorar sensores, criar dashboards em tempo real.

**Componentes:**
- AWS IoT Core: conecta dispositivos via MQTT
- InfluxDB: banco de séries temporais (em Docker/EC2)
- Grafana: dashboards de visualização (em Docker/EC2)
- Node-RED: programação visual de fluxos IoT (em Docker/EC2)

**Fluxo:** Sensor → MQTT → IoT Core → Rules Engine → InfluxDB → Grafana

---
---

## 3. TABELAS COMPARATIVAS

### 3.1 EC2 vs Lambda

| Aspecto | EC2 | Lambda |
|---------|-----|--------|
| Tipo | IaaS (servidor virtual) | FaaS (serverless) |
| Gerenciamento | Você gerencia SO | AWS gerencia tudo |
| Escala | Manual/Auto Scaling | Automática (0 a milhares) |
| Cobrança | Por hora/segundo (ligado) | Por requisição + duração |
| Timeout | Ilimitado | Máximo 15 minutos |
| Estado | Stateful | Stateless |
| Cold start | Não | Sim |
| Caso de uso | Apps longas, Docker, DBs | APIs, eventos, processamento curto |

---

### 3.2 RDS vs DynamoDB

| Aspecto | RDS | DynamoDB |
|---------|-----|----------|
| Tipo | Relacional (SQL) | NoSQL (chave-valor/documento) |
| Esquema | Fixo (tabelas, colunas) | Flexível (schema-less) |
| Consultas | SQL completo, JOINs | Queries por chave, Scan |
| Escala | Vertical | Horizontal (automática) |
| Índices | Padrão SQL | GSI e LSI |
| Transações | ACID nativo | DynamoDB Transactions |
| Streams | Não nativo | DynamoDB Streams |
| Caso de uso | Transações complexas, relatórios | Alta escala, IoT, gaming |

---

### 3.3 S3 vs EBS vs EFS

| Aspecto | S3 | EBS | EFS |
|---------|----|----|-----|
| Tipo | Objetos | Bloco | Filesystem (NFS) |
| Acesso | HTTP/API | Uma EC2 | Múltiplas EC2 |
| Escalabilidade | Ilimitado | Fixo (redimensionável) | Automática |
| Durabilidade | 11 noves | 99.999% | 11 noves |
| Caso de uso | Backups, data lake | SO, bancos | Diretórios compartilhados |

---

### 3.4 SQS vs SNS vs Kinesis

| Aspecto | SQS | SNS | Kinesis |
|---------|-----|-----|---------|
| Modelo | Queue (pull) | Pub/Sub (push) | Stream (pull) |
| Consumers | Um por mensagem | Múltiplos subscribers | Múltiplos consumers |
| Ordem | FIFO (opcional) | Não garantida | Garantida por shard |
| Retenção | Até 14 dias | Sem retenção | Até 365 dias |
| Caso de uso | Desacoplamento | Notificações, fan-out | Ingestão real-time |
| Replay | Não | Não | Sim |

---

### 3.5 Standard SQS vs FIFO SQS

| Aspecto | Standard | FIFO |
|---------|----------|------|
| Ordem | Best-effort | Garantida |
| Entrega | At-least-once | Exactly-once |
| Throughput | Ilimitado | 300 msg/s (sem batching) |
| Caso de uso | Alta escala, tolerante a duplicatas | Transações financeiras, ordem crítica |

---

### 3.6 CloudFront vs ElastiCache

| Aspecto | CloudFront | ElastiCache |
|---------|-----------|-------------|
| Tipo | CDN (edge) | In-memory cache |
| Localização | Edge locations globais | Dentro da VPC |
| Dados | Conteúdo estático/dinâmico | Resultados de queries, sessões |
| Protocolo | HTTP/HTTPS | Redis/Memcached protocol |
| Caso de uso | Sites, APIs, streaming | DB cache, session store |

---

### 3.7 Redis vs Memcached (ElastiCache)

| Aspecto | Redis | Memcached |
|---------|-------|-----------|
| Persistência | Sim | Não |
| Read replicas | Sim | Não |
| Pub/Sub | Sim | Não |
| Estruturas de dados | Strings, lists, sets, hashes | Strings simples |
| Multi-threaded | Não | Sim |
| Caso de uso | Cache complexo, pub/sub | Cache simples, alta concorrência |

---

### 3.8 Security Group vs Network ACL

| Aspecto | Security Group | Network ACL |
|---------|---------------|-------------|
| Nível | Instância (ENI) | Sub-rede |
| Estado | Stateful | Stateless |
| Regras | Somente ALLOW | ALLOW e DENY |
| Avaliação | Todas as regras | Ordem numérica |
| Padrão | Nega tudo (inbound) | Permite tudo |

---

### 3.9 Cognito User Pool vs Identity Pool

| Aspecto | User Pool | Identity Pool |
|---------|-----------|---------------|
| Função | Autenticação (sign-up/sign-in) | Autorização (credenciais AWS) |
| Retorna | Tokens (JWT) | Credenciais temporárias AWS |
| Caso de uso | Login de usuários | Acesso a S3, DynamoDB pelo app |
| Integração | API Gateway, ALB | Serviços AWS diretamente |

---

### 3.10 CloudFormation vs SAM

| Aspecto | CloudFormation | SAM |
|---------|---------------|-----|
| Escopo | Qualquer recurso AWS | Serverless (Lambda, API GW, DynamoDB) |
| Sintaxe | Verbosa | Simplificada |
| Seção Globals | Não | Sim |
| Teste local | Não | Sim (sam local invoke) |
| Tipos | AWS::* | AWS::Serverless::* |

---
---

## 4. DECORE ANTES DA PROVA

### 4.1 Conceitos Essenciais

- **SDLC** → 6 fases: Planejar, Definir, Projetar, Desenvolver, Implantar, Manter
- **AWS CloudShell** → Herda credenciais do console de gerenciamento
- **Amazon Q Developer** → Assistente de codificação com IA generativa
- **S3** → Armazenamento de objetos. Bucket (nome global único) + Objetos.
- **S3 Versionamento** → Uma vez ativado, NÃO pode ser desativado (apenas suspenso)
- **S3 PUT máximo** → 5 GB em uma única operação
- **URL pré-assinada** → Acesso temporário a objeto S3 sem credenciais AWS
- **CORS** → Necessário para acessar objetos de outro bucket em site estático
- **IAM** → Gerencia identidades e permissões. Policies em JSON.
- **IAM Role** → Credenciais temporárias. Recomendado para EC2 (não Access Key).
- **Deny explícito** → SEMPRE sobrepõe Allow no IAM
- **Princípio do menor privilégio** → Conceder apenas permissões necessárias
- **DynamoDB** → NoSQL chave-valor. Partition Key + Sort Key (opcional).
- **GSI** → Global Secondary Index. Consulta por atributos diferentes da PK.
- **DynamoDB Streams** → Captura mudanças. Pode acionar Lambda.
- **DynamoDB Transactions** → Operações atômicas "tudo ou nada"
- **Point-in-time recovery** → Restaura últimos 35 dias
- **API Gateway** → Front-door para APIs. Stages + Stage Variables.
- **API Gateway timeout** → Máximo 29 segundos
- **Mapping template** → Transforma request antes de enviar ao backend
- **AWS WAF** → Protege API Gateway contra SQL injection e XSS
- **Lambda** → Serverless. Executa SOMENTE quando ativado por evento.
- **Lambda timeout** → Máximo 15 minutos
- **Burst quota** → Restrição que NÃO pode ser modificada
- **Execution Role** → Permissões que Lambda tem para acessar outros serviços
- **Provisioned concurrency** → Resolve cold start
- **Lambda alias** → ARN com :PROD invoca versão associada ao alias PROD
- **X-Ray** → Service map para localizar erros visualmente
- **Docker** → Container = instância de imagem. Dockerfile = receita.
- **ECS** → Orquestração de containers Docker na AWS
- **Fargate** → Execução serverless de containers (sem gerenciar EC2)
- **Elastic Beanstalk** → Deploy simplificado. Traffic Splitting = canary testing.
- **ElastiCache Redis** → In-memory, suporta read replicas
- **CloudFront** → CDN. Edge locations. Cache key mínima = melhor hit ratio.
- **Lazy loading** → Evita encher cache com dados não requisitados
- **SQS** → Fila. Consumers fazem POLL. Visibility timeout.
- **FIFO SQS** → Ordem garantida + exactly-once delivery
- **Dead-letter queue** → Mensagens que falharam N vezes (maxReceiveCount)
- **SNS** → Pub/sub. Topic = canal. Mensagens pushed para subscribers.
- **Filter policy** → Filtra mensagens para subscriber específico
- **Kinesis** → Streaming real-time. Dados em shards. KPL para produzir.
- **Step Functions** → Orquestração visual. Task, Choice, Map, Parallel.
- **Choice state** → Lógica condicional (if/else)
- **Map state** → Itera sobre lista
- **Parallel state** → Executa branches em paralelo
- **Express workflows** → Alta taxa de eventos (IoT)
- **Cognito User Pool** → Sign-up/sign-in. Retorna JWTs.
- **Cognito Identity Pool** → Credenciais temporárias AWS para apps
- **STS** → Credenciais temporárias. Federated = IdP externo.
- **ACM** → Gerencia certificados SSL/TLS. Renovação automática.
- **CloudTrail** → Auditoria. Quem fez o quê na conta AWS.
- **CodePipeline** → Automatiza pipeline CI/CD
- **CloudFormation** → IaC. Stack = unidade de deployment.
- **SAM** → Serverless IaC. Seção Globals exclusiva. `sam deploy`.
- **VPC** → Rede isolada. CIDR. Subnet pública/privada.
- **Internet Gateway** → Acesso bidirecional à internet (subnet pública)
- **NAT Gateway** → Saída para internet (subnet privada). Fica na subnet pública.
- **Security Group** → Stateful. Só ALLOW. Nível instância.
- **NACL** → Stateless. ALLOW e DENY. Nível sub-rede.

---

### 4.2 Pegadinhas Comuns (baseadas nas perguntas do curso)

1. **S3 versionamento** → Protege contra exclusão acidental. Resposta correta para "durable storage + protect against deletion".
2. **IAM Role para EC2** → Sempre a resposta correta quando perguntam "more secure solution" para EC2 acessar DynamoDB/S3.
3. **Stage variables no API Gateway** → Resposta para "LEAST configuration" ao manter ambientes dev/prod com Lambda aliases.
4. **DynamoDB Streams** → Resposta para "enviar mudanças da tabela para Lambda".
5. **FIFO SQS** → Resposta para "processamento em ordem" (não standard queue, não Kinesis para transações individuais).
6. **Visibility timeout** → Aumentar quando mensagens são processadas mais de uma vez.
7. **Dead-letter queue** → Resposta para "reduzir impacto de mensagens com falha".
8. **Choice state** → Resposta para "diferentes passos dependendo de condição" no Step Functions.
9. **Map state** → Resposta para "executar mesma função para cada item de uma lista".
10. **Cognito User Pool** → Resposta para "sign-up and sign-in". Identity Pool é para credenciais AWS.
11. **Lambda post-authentication** → Invocar Lambda (não API Gateway) para log de eventos após login.
12. **CloudTrail** → Resposta para "investigar quem deletou objetos do S3".
13. **Burst quota** → Única restrição do Lambda que NÃO pode ser modificada.
14. **Provisioned concurrency** → Resposta para "slow response for first users each day" (cold start).
15. **Upload > 50MB** → Fazer upload para S3 e referenciar no Lambda.
16. **X-Ray service map** → Primeiro passo para troubleshooting de erros em app serverless.
17. **Traffic Splitting** → Canary testing no Elastic Beanstalk.
18. **Conditions section** → Resposta para "mesmo template para test e prod" no CloudFormation.
19. **AWS::Serverless::SimpleTable** → Cria tabela DynamoDB no SAM.
20. **Globals section** → Exclusiva do SAM (não existe no CloudFormation puro).

---

### 4.3 Respostas-Chave das Provas dos Módulos

| Módulo | Pergunta-chave | Resposta |
|--------|---------------|----------|
| 3 | Durable storage + protect against deletion | S3 com versionamento |
| 4 | More secure solution para EC2 acessar DynamoDB | IAM Role associada à EC2 |
| 5 | Enviar mudanças do DynamoDB para Lambda | Habilitar DynamoDB Streams |
| 6 | Dev/prod com LEAST configuration | Stage variables + Lambda aliases |
| 7 | Slow response for first users (cold start) | Provisioned concurrency |
| 8 | Canary testing no Beanstalk | Traffic Splitting |
| 9 | Melhorar performance para users distantes | CloudFront distribution |
| 10 | Processamento em ordem de transações | FIFO SQS queue |
| 11 | Lógica condicional no Step Functions | Choice state |
| 12 | Sign-up/sign-in + log de eventos | Cognito + Lambda (post-auth) |
| 13 | Mesmo template para test/prod | Conditions section |

---

### 4.4 Formas de Cobrança AWS

- Usar dados armazenados (storage)
- Usar processamento (compute)
- Dados que SAEM da AWS (data transfer out)

---

### 4.5 Códigos HTTP Importantes

| Código | Significado |
|--------|-------------|
| 200 | OK (sucesso) |
| 201 | Created |
| 400 | Bad Request (erro do cliente) |
| 401 | Unauthorized (não autenticado) |
| 403 | Forbidden (não autorizado) |
| 404 | Not Found |
| 429 | Too Many Requests (throttling) |
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |

---

*Fim do guia de revisão. Boa prova! 🚀*
