# AcademicAgent-Redes-II-IA

## 👥 Integrantes
- Artur Mesquita Jeager (188354)
     - Plataforma: Linux → Ubuntu 24.04.2 LTS
- Octávio Francisco Petry Bortoluzzi (188380)
     - Plataforma: Windows 11 Home

--- 
## Descrição do Problema 

"Um aluno se depara com um prova de redes II com prazo próximo, sem muito tempo, ele precisa estudar todo o conteúdo da matéria de uma forma rápida e eficiente."

Neste contexto, entra o AcademicAgent como um auxiliador de estudos, neste contexto abrangendo a matéria de redes, que ajudará os usuários a revisar o conteudo com a finalidade de se preparar para prova, corrigindo e criando questões de estudo, respondendo à perguntas.

---

## ⚙️ Especificações do Projeto:
- LangChain: Framework para aplicações com LLMs
- LangGraph: Orquestração de agentes
- Ollama: Execução local de modelos LLaMA
- ChromaDB: Banco de dados vetorial
- Sentence Transformers: Geração de embeddings
- Python 3.10+: Linguagem de programação
  
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

7. Execute a Ingestão para Fomentar a Base de conhecimento
No terminal, com o ambiente ainda ativado, rode:

---

## Especificações dos Agente IA

- Agente 1 (Pesquisador): Ele recebe a dúvida do aluno, vai até a biblioteca (ChromaDB), lê os PDFs de Redes, extrai apenas os dados mais densos e técnicos e cria um "Resumo Técnico" (um dossiê).
- Agente 2 (Professor): Ele não acessa os PDFs. Ele recebe o "Dossiê Técnico" do Pesquisador e tem a função exclusiva de traduzir aquele jargão técnico para uma explicação didática, fluida e com exemplos para o aluno.
- Agente 3 (Revisor): Mantemos o nosso avaliador de qualidade no final.

---

## 🎯 Exemplos de Execução

```
==================================================

Qual a sua dúvida de Redes?
> Se o servidor DNS parar, o que acontece com a empresa?

[Agente Recuperador] Buscando materiais na base de Redes II...
[Agente Redator] Escrevendo a explicação...
[Agente Revisor] Avaliando a qualidade da resposta...

==================================================
RESPOSTA FINAL:
Excelente pergunta!

Se o servidor DNS parar, a empresa pode enfrentar graves problemas para manter sua infraestrutura online. Aqui estão algumas consequências:

1. **Impossibilidade de acesso**: Sem um servidor DNS funcionando corretamente, os usuários não poderão mais acessar os sites da empresa ou seus serviços online.
2. **Desenvolvimento de erros**: Os aplicativos e sistemas que dependem do DNS para resolver nomes de domínios começarão a apresentar erros e falhas, o que pode levar à perda de dados e tempo de inatividade.
3. **Problemas de comunicação**: A impossibilidade de resolução de nomes de domínios impede a comunicação entre os servidores da empresa e seus clientes, levando a problemas de entrega de emails, mensagens instantâneas e outros serviços online.
4. **Perda de reputação**: Uma falha prolongada no servidor DNS pode levar à perda de confiança dos clientes e parceiros, o que pode afetar negativamente a imagem da empresa.

Para minimizar esses riscos, é fundamental implementar estratégias de backup e recuperação para garantir a continuidade do serviço DNS. Isso pode incluir a manutenção de servidores DNS redundantes, a configuração de caching e a realização de backups regulares dos dados do servidor DNS. Além disso, é importante ter um plano de contingência em caso de falha para minimizar os danos e garantir a recuperação rápida do serviço.
==================================================
```
```python ingestao.py```

