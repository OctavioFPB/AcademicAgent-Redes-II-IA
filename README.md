# AcademicAgent-Redes-II-IA

## 👥 Integrantes
- Artur Mesquita Jeager (188354)
     - Plataforma: Linux → Ubuntu 24.04.2 LTS
- Octávio Francisco Petry Bortoluzzi (188380)
     - Plataforma: Windows 11 Home

---

## ⚙️ Especificações do Projeto:
- Linguagem: C++ (padrão C++17)

  
---

## 🧪 Instruções de compilação/execução.
### ✅ Pré-requisitos
- Sistema: GNU/Linux
- Compilador: `g++` com suporte a __C++17__ (ou superior)
Para instalar o g++, execute (caso ainda não tenha):
```bash
sudo apt update
sudo apt install g++
```

### 🦙 1. Instale o Ollama e Baixe o Modelo
Baixe o instalador no site oficial (ollama.com). Após instalar, abra o terminal e faça o download do modelo que será o cérebro dos seus agentes:
ollama pull llama3

### 📂 2. Crie a Estrutura de Pastas
Crie uma pasta principal para o seu trabalho final (por exemplo, trabalho_redes_ia). Abra o terminal dentro dessa nova pasta.

### 3. Crie e Ative o Ambiente Virtual
Isso impede que as bibliotecas do projeto entrem em conflito com o resto do seu computador.
No terminal (dentro da pasta do projeto), rode:
python -m venv venv

Para ativar o ambiente (o prefixo (venv) deve aparecer no terminal):
```bash
No Windows: venv\Scripts\activate

No Linux/Mac: source venv/bin/activate
```

4. Instale as Bibliotecas Corretas
Com o ambiente ativado, execute o comando abaixo. Ele instala exatamente as versões que se comunicam bem entre si para a ingestão de dados e orquestração de agentes:
pip install langchain langchain-community langchain-huggingface langchain-chroma pypdf sentence-transformers chromadb langgraph

5. Organize os Arquivos do Projeto
Dentro da sua pasta principal, crie uma subpasta chamada dados_redes. Mova os 10 PDFs que você anexou aqui (DNS, Sockets, IP, etc.) para dentro dessa pasta dados_redes.

6. Recrie o Script de Ingestão
Na pasta principal (fora de dados_redes), crie um arquivo chamado ingestao.py e cole o código que passei na mensagem anterior. Salve o arquivo.

7. Execute a Ingestão
No terminal, com o ambiente ainda ativado, rode:
python ingestao.py
