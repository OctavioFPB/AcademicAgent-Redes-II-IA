# AcademicAgent-Redes-II-IA

## 👥 Integrantes
- Artur Mesquita Jeager (188354)
     - Plataforma: Linux → Ubuntu 24.04.2 LTS
- Octávio Francisco Petry Bortoluzzi (188380)
     - Plataforma: Windows 11 Home

---

## ⚙️ Especificações do Projeto:
- LangChain: Framework para aplicações com LLMs
- LangGraph: Orquestração de agentes
- Ollama: Execução local de modelos LLaMA
- ChromaDB: Banco de dados vetorial
- Sentence Transformers: Geração de embeddings
- Python 3.10+: Linguagem de programação
  
---

## 🧪 Instruções de compilação/execução.
### 🦙 1. Instale o Ollama e Baixe o Modelo
Baixe o instalador no site oficial (ollama.com). Após instalar, abra o terminal e faça o download do modelo que será o cérebro dos seus agentes:
```ollama pull llama3```

### 📂 2. Crie a Estrutura de Pastas
Crie/baixe a pasta principal do trabalho final. Abra o terminal dentro dessa nova pasta.

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
pip install langchain langchain-community langchain-huggingface langchain-chroma pypdf sentence-transformers chromadb langgraph

5. Organize os Arquivos do Projeto
Dentro da sua pasta principal, crie uma subpasta chamada dados_redes. Mova os 10 PDFs que você anexou aqui (DNS, Sockets, IP, etc.) para dentro dessa pasta dados_redes.

6. Recrie o Script de Ingestão
Na pasta principal (fora de dados_redes), crie um arquivo chamado ingestao.py e cole o código que passei na mensagem anterior. Salve o arquivo.

7. Execute a Ingestão
No terminal, com o ambiente ainda ativado, rode:
python ingestao.py
