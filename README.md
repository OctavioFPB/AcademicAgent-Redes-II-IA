# Multi-Agentes IA Acadêmico - Especialistas em Redes 

## 👥 Integrantes
- Artur Mesquita Jeager (188354)
     - Plataforma: Linux → Mint 22.3 Zena
- Octávio Francisco Petry Bortoluzzi (188380)
     - Plataforma: Windows 11 Home Single Language (25H2)
     - Terminal: PowerShell

--- 
## 📐 Descrição do Problema & Objetivo da Solução

"Um aluno se depara com um prova de redes II com prazo próximo, sem muito tempo, ele precisa estudar todo o conteúdo da matéria de uma forma rápida e eficiente."

Neste contexto, entra o AcademicAgent como um auxiliador de estudos, neste contexto abrangendo a matéria de redes, que ajudará os usuários a revisar o conteudo com a finalidade de se preparar para prova, corrigindo e criando questões de estudo, respondendo à perguntas.

---

## ⚙️ Especificações Técnicas do Projeto e Arquitetura:
- LangChain: Framework para aplicações com LLMs
- LangGraph: Orquestração de agentes
- Ollama: Execução local de modelos LLaMA
- ChromaDB: Banco de dados vetorial
- Sentence Transformers: Geração de embeddings
- Python 3.10+: Linguagem de programação

- Tools Disponíveis:
     - O sistema conta com uma ferramenta principal chamada buscar_documentos_redes. Ela é acionada exclusivamente pelo Agente Pesquisador e tem a função de receber uma string de busca (query), consultar o banco de dados vetorial local e retornar os trechos de texto mais relevantes (top-K) que contêm o jargão técnico necessário para responder à dúvida do usuário.

- Explicação de como o MCP foi utilizado:
     - Para padronizar o acesso a recursos externos, implementamos o Model Context Protocol (MCP) através de uma classe adaptadora local (AdaptadorMCP). O Agente Pesquisador não acessa o banco vetorial diretamente; em vez disso, ele envia uma requisição no formato padrão JSON-RPC 2.0 (método tools/call) para o adaptador. O adaptador executa a tool e devolve os dados formatados na árvore de resposta oficial do MCP (result -> content -> text), garantindo desacoplamento e segurança na execução da ferramenta.

- Explicação da estratégia de RAG (Retrieval-Augmented Generation):
     - A estratégia de RAG foi dividida em duas etapas para evitar alucinações. Primeiro, quando o usuário faz uma pergunta, o Agente Pesquisador faz a recuperação (Retrieval) extraindo os dados técnicos brutos do banco vetorial, gerando um "Dossiê Técnico". Em seguida, ocorre a geração aumentada (Augmented Generation), onde o Agente Professor recebe apenas esse dossiê como contexto (sem acesso à base total ou a pesquisas web) e traduz o conteúdo para uma linguagem didática e formatada para o aluno.

- Origem e natureza da base de conhecimento utilizada:
     - A base de conhecimento é composta por materiais didáticos em formato PDF da disciplina de Redes de Computadores II. A natureza dos dados é estritamente acadêmica e técnica, cobrindo tópicos fundamentais da ementa, como: Arquitetura TCP/IP, DNS, Sockets, Protocolos UDP e TCP, Roteamento IP, ICMP e Cálculo de Sub-redes.

- Tecnologia de embeddings e armazenamento vetorial adotados: 
           - Embeddings: Utilizamos a biblioteca Sentence Transformers integrada via HuggingFaceEmbeddings, rodando o modelo leve e eficiente all-MiniLM-L6-v2. Ele converte os trechos de texto dos PDFs em vetores matemáticos com excelente captura de semântica.
           - Armazenamento Vetorial: Adotamos o ChromaDB, executado de forma local e persistente. Ele armazena os embeddings e realiza a busca de contexto em frações de segundo utilizando o cálculo de similaridade de cosseno.

- Dependências do Projeto:
     - Para replicar e rodar o projeto localmente, as seguintes tecnologias e bibliotecas são exigidas:
          - Core: Python (3.10 ou superior) e Ollama (com o modelo llama3 baixado localmente).
          - Bibliotecas Python (Instaláveis via pip):
                - ```langgraph``` (Orquestração de agentes)
                - ```langchain``` e ```langchain-ollama``` (Integração com LLM)
                - ```langchain-chroma``` e ```chromadb``` (Banco vetorial local)
                - ```langchain-huggingface``` e ```sentence-transformers``` (Geração de embeddings locais)
                - ```pypdf``` (Leitura e extração de texto dos PDFs originais)
           
---

## ✔️​ Requisitos
- Hardware: Pelo menos 8GB de RAM (recomendado 16GB para rodar o modelo LLaMA localmente com folga).
- Python: Versão 3.10, 3.11 ou 3.12 instalada (evite a versão 3.13 recém-lançada, pois muitas bibliotecas de IA ainda não são totalmente compatíveis).
- Compilador C++ (Apenas Windows): O ChromaDB e outras bibliotecas matemáticas geralmente exigem o "Microsoft C++ Build Tools" instalado no Windows para compilar dependências.
- Ollama: Instalado no sistema operacional para rodar o modelo local.

---

## 🧪 Instruções de compilação/execução.
### 🦙 1. Instale o Ollama e Baixe o Modelo
Baixe o instalador no site oficial (ollama.com). Após instalar, abra o terminal e faça o download do modelo que será o cérebro dos seus agentes:
```ollama pull llama3```

### 📂 2. Estrutura de Pastas
Baixe a pasta principal do trabalho final anexada no repositório. Abra o terminal dentro dessa nova pasta.

### 👾 3. Crie e Ative o Ambiente Virtual
Isso impede que as bibliotecas do projeto entrem em conflito com o resto do seu computador.
No terminal (dentro da pasta do projeto), rode:
```python -m venv venv```

Para ativar o ambiente (o prefixo (venv) deve aparecer no terminal):
```bash
No Windows: venv\Scripts\activate
No Linux/Mac: source venv/bin/activate
```

### 4. 📖 Instale as Bibliotecas Corretas
Com o ambiente ativado, execute o comando abaixo. Ele instala exatamente as versões que se comunicam bem entre si para a ingestão de dados e orquestração de agentes:

```pip install langchain langchain-community langchain-huggingface langchain-chroma pypdf sentence-transformers chromadb langgraph```

### 7. Execute a Ingestão para Fomentar a Base de conhecimento
No terminal, com o ambiente ainda ativado, rode: ```python ingestao.py```

---

## 🤖 Papéis dos Agentes na Arquitetura
- __Agente 1__ (Pesquisador): Atua como o especialista em recuperação de informações. Ao receber a dúvida do aluno, ele não acessa o banco de dados de forma engessada; em vez disso, utiliza o MCP (Model Context Protocol) para acionar a ferramenta externa de busca na base vetorial (ChromaDB). Com o retorno padronizado, ele lê os trechos dos PDFs da disciplina de Redes de Computadores, extrai apenas os dados mais densos e técnicos, e compila um "Dossiê Técnico".
- __Agente 2__ (Professor): Ele não tem acesso direto aos PDFs nem às ferramentas de busca. Ele recebe exclusivamente o "Dossiê Técnico" formulado pelo Pesquisador e tem a função de traduzir aquele jargão bruto para uma explicação didática, fluida e com exemplos práticos para o aluno.
- __Agente 3__ (Revisor): Atua como o coordenador de qualidade (Quality Assurance) do sistema. Ele recebe a dúvida original do aluno e a resposta elaborada pelo Professor. Sua função é realizar uma avaliação crítica binária: se a resposta estiver clara, correta e livre de alucinações, ele a APROVA para o usuário final. Caso identifique falhas, jargões excessivos ou respostas incompletas, ele REJEITA o texto, forçando o Agente Professor a reescrever a explicação (com um limite de segurança de 3 tentativas para evitar loops infinitos).

## 📜 Justificativa: Por que esta arquitetura é superior a um Agente Único?

A escolha da arquitetura em pipeline com três agentes especializados (Pesquisador $\rightarrow$ Professor $\rightarrow$ Revisor) foi adotada para resolver um dos problemas mais comuns em Modelos de Linguagem: a perda de foco e a alucinação ao lidar com múltiplas instruções complexas simultaneamente.Em uma abordagem de Agente Único, o LLM precisaria, em um mesmo prompt: interpretar a pergunta, acionar as ferramentas de busca em uma base de dados extensa, extrair os fatos técnicos, adequar o tom de voz para ser didático e revisar o próprio texto. Isso frequentemente gera respostas onde a didática sobrepõe a precisão técnica, ou onde o modelo simplesmente inventa informações (alucinação) para preencher lacunas de contexto ruidoso.

Os ganhos diretos da nossa Arquitetura Multiagente incluem:

- Separação de Preocupações (Separation of Concerns): Cada agente possui um system prompt enxuto e hiperfocado. O Pesquisador é estritamente analítico e extrativo. O Professor é estritamente generativo e focado em pedagogia.
- Prevenção de Alucinação (Groundedness): Como o Agente Professor não tem acesso ao mecanismo de busca global e é forçado a basear-se apenas no dossiê filtrado pelo Pesquisador, a chance de inventar conceitos de Redes de Computadores que não estão na ementa da disciplina cai drasticamente.
- Controle de Qualidade em Loop (Self-Reflection): A introdução do Agente Revisor cria um mecanismo de auto-correção. O sistema não entrega a primeira resposta gerada caso ela não atinja o padrão acadêmico exigido, algo impossível de garantir de forma confiável com uma execução de passo único (single-shot) por um único agente.
- Desacoplamento de Ferramentas via MCP: Ao obrigar o Pesquisador a solicitar os dados através do Model Context Protocol, separamos o raciocínio da IA da infraestrutura de banco de dados. Isso traz segurança e modularidade, permitindo escalar o sistema no futuro sem alterar a lógica cognitiva dos agentes.

---

## 🎯 Exemplos de Execução

```
Qual a sua dúvida de Redes?
> Quantas etapas tem um processo de Handshake

[Agente 1: Pesquisador] Vasculhando os PDFs e criando um dossiê técnico...
[Agente 2: Professor] Transformando o dossiê em uma explicação didática...
[Agente 3: Revisor] Avaliando se a aula está boa...

==================================================
RESPOSTA FINAL:
Muito bem! Vamos explorar o processo de Handshake juntos!

De acordo com o dossiê técnico, o processo de Handshake tem 3 etapas:

1. **Sincronização**: O cliente envia um pacote SYN (synchronize) ao servidor.
2. **Resposta do Servidor**: O servidor responde com um pacote SYN-ACK (synchronize-acknowledgment).
3. **Confirmação**: O cliente confirma a conexão com um pacote ACK (acknowledgment).

Essas 3 etapas são essenciais para estabelecer uma conexão segura e eficaz entre o cliente e o servidor. E agora, você tem uma ideia clara sobre como funciona o Handshake!
==================================================
```

