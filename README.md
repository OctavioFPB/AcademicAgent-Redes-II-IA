# AcademicAgent-Redes-II-IA

## 👥 Integrantes
- Artur Mesquita Jeager (188354)
     - Plataforma: Linux → Ubuntu 24.04.2 LTS
- Octávio Francisco Petry Bortoluzzi (188380)
     - Plataforma: Windows 11 Home

--- 
## 📐 Descrição do Problema & Objetivo da Solução

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
## 📜 Papel de cada agente

AcademicAgent possui 3 agentes:

* 1.Pesquisador: responsável por realizar a pesquisa, relativa a pergunata, no banco de dados que repassa o conteúdo ao professor;
* 2.Professor: responsável por transformar o conteudo do pesquisador em uma explicação;
* 3.Revisor: responsável por revisar o conteudo do professor para conseratar imprecições e garantir a qualidadee acuricidade da explicação.

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

## Especificações dos Agente IA

- Agente 1 (Pesquisador): Ele recebe a dúvida do aluno, vai até a biblioteca (ChromaDB), lê os PDFs de Redes, extrai apenas os dados mais densos e técnicos e cria um "Resumo Técnico" (um dossiê).
- Agente 2 (Professor): Ele não acessa os PDFs. Ele recebe o "Dossiê Técnico" do Pesquisador e tem a função exclusiva de traduzir aquele jargão técnico para uma explicação didática, fluida e com exemplos para o aluno.
- Agente 3 (Revisor): Mantemos o nosso avaliador de qualidade no final.

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

