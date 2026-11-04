# 🚀 Servidor Vector Store - Chroma DB

Este repositório contém as configurações para execução local do servidor de banco de dados vetorial **Chroma DB**, utilizado na integração com a API Spring Boot.

---

## 🛠️ Pré-requisitos

* **Python 3.10+** instalado
* **Git** instalado

---

## 📦 Como Baixar e Executar do Zero

Siga o passo a passo no terminal para clonar o repositório, preparar o ambiente virtual e iniciar o servidor.

### 1. Clonar o Repositório
```powershell
git clone https://github.com/nayanpereira/chroma.git
cd chroma
```

### 2. Criar o Ambiente Virtual (`venv`)
No terminal (PowerShell ou CMD), crie o ambiente virtual responsável por isolar as dependências do projeto:

```powershell
python -m venv venv
```

> 💡 **Nota (PowerShell):** Se a execução de scripts estiver desabilitada no seu PowerShell, libere a sessão atual executando:
> ```powershell
> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
> ```

### 3. Instalar as Dependências
Instale o **Chroma DB** e demais dependências a partir do arquivo de requisitos:

```powershell
.\venv\Scripts\pip install -r requirements.txt
```

*(Caso ainda não possua o arquivo `requirements.txt`, instale diretamente executando: `.\venv\Scripts\pip install chromadb`)*

---

## ⚡ Executando o Servidor Chroma DB

Execute o comando abaixo para iniciar o servidor escutando apenas em **localhost (`127.0.0.1`)**, garantindo segurança e isolamento da sua rede local:

```powershell
.\venv\Scripts\chroma run --path .\dados --host 127.0.0.1 --port 8000
```

> **Atenção:** A pasta `.\dados` será criada automaticamente pelo Chroma DB assim que a primeira coleção for gerada.

---

## 🔍 Teste de Conexão

Com o servidor em execução, confirme se o serviço está ativo acessando o endpoint de heartbeat:

* **URL base:** `http://127.0.0.1:8000`
* **Heartbeat API:** `http://127.0.0.1:8000/api/v2/heartbeat`

### Teste via PowerShell:
```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/api/v2/heartbeat"
```

---

## ⚙️ Configuração na API Spring Boot (`application.properties`)

Para conectar a aplicação Java / Spring Boot a este servidor Chroma local, insira no arquivo `src/main/resources/application.properties`:

```properties
spring.ai.vectorstore.chroma.client.host=http://127.0.0.1
spring.ai.vectorstore.chroma.client.port=8000
```