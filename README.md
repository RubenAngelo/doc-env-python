
# ⚙️ Ambiente de Desenvolvimento com WSL, Docker, Pyenv e Poetry

Este repositório contém um guia completo e passo a passo para configurar um ambiente de desenvolvimento Python usando **WSL (Ubuntu)**, **Docker**, **pyenv** e **Poetry**.

---

## 📦 Tecnologias Utilizadas

- WSL 2 (Ubuntu)
- Docker & Docker Compose
- Pyenv
- Poetry
- Git
- Python 3.x
- Visual Studio Code (opcional)

---

## 📖 Índice

- [⚙️ Ambiente de Desenvolvimento com WSL, Docker, Pyenv e Poetry](#️-ambiente-de-desenvolvimento-com-wsl-docker-pyenv-e-poetry)
  - [📦 Tecnologias Utilizadas](#-tecnologias-utilizadas)
  - [📖 Índice](#-índice)
  - [🔧 Instalação do WSL](#-instalação-do-wsl)
  - [🐳 Instalação do Docker](#-instalação-do-docker)
  - [🐍 Instalação do Pyenv](#-instalação-do-pyenv)
    - [Dependências:](#dependências)
    - [Instalação:](#instalação)
    - [Configuração no shell:](#configuração-no-shell)
    - [Verificação:](#verificação)
  - [📦 Instalação do Poetry](#-instalação-do-poetry)
    - [Dependências:](#dependências-1)
    - [Instalação:](#instalação-1)
    - [Configuração:](#configuração)
    - [Verificação:](#verificação-1)
  - [🧠 Integração com IDE (VSCode)](#-integração-com-ide-vscode)
  - [🛠️ Configurando o Pyenv no Projeto](#️-configurando-o-pyenv-no-projeto)
  - [🚧 Criando um Projeto com Poetry](#-criando-um-projeto-com-poetry)
  - [📚 Gerenciando Dependências](#-gerenciando-dependências)
    - [Criando e ativando ambiente virtual:](#criando-e-ativando-ambiente-virtual)
    - [Adicionando dependências:](#adicionando-dependências)
    - [Instalando todas as dependências do projeto:](#instalando-todas-as-dependências-do-projeto)
    - [Reescreva o arquivo poetry.lock:](#reescreva-o-arquivo-poetrylock)
  - [▶️ Executando o Projeto](#️-executando-o-projeto)
  - [✅ Verificação rápida](#-verificação-rápida)
  - [🧠 Extras](#-extras)

---

## 🔧 Instalação do WSL

1. Abra o **Prompt de Comando** (não precisa ser como administrador):

   ```bash
   wsl --install
   ```

2. Entre no Ubuntu:

   ```bash
   wsl -d Ubuntu
   ```

3. Crie um usuário e senha quando solicitado.

4. Atualize os pacotes:

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

## 🐳 Instalação do Docker

```bash
sudo apt install docker.io docker-compose-plugin
sudo usermod -aG docker $USER
newgrp docker
```

Reinicie o WSL:

```bash
wsl --shutdown
wsl -d Ubuntu
```

Instale o Docker Compose:

Teste com:

```bash
docker run hello-world
```

---

## 🐍 Instalação do Pyenv

### Dependências:

```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
libffi-dev liblzma-dev git
```

### Instalação:

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

### Configuração no shell:

1. Abra o arquivo de configuração do shell:

    ````bash
    nano ~/.bashrc
    ````

2. Adicione os comandos do pyenv ao arquivo: No final do arquivo, adicione as seguintes linhas:

    ```bash
    export PYENV_ROOT="$HOME/.pyenv"
    export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init --path)"
    eval "$(pyenv init -)"
    ```

3. Salve o aruivo apertando:

    - `CTRL + O`
    - `Enter`
    - `CTRL + X`

### Verificação:

```bash
pyenv --version
```

---

## 📦 Instalação do Poetry

### Dependências:

```bash
sudo apt install curl python3-pip -y
```

### Instalação:

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

### Configuração:

```bash
export PATH="$HOME/.local/bin:$PATH"
source ~/.bashrc
```

### Verificação:

```bash
poetry --version
```

---

## 🧠 Integração com IDE (VSCode)

1. Crie o projeto e abra com o **VSCode**.
2. Use `Ctrl + J` para abrir o terminal integrado.
3. Clique na setinha do terminal e selecione **Ubuntu (WSL)**.

---

## 🛠️ Configurando o Pyenv no Projeto

Com o terminal já aberto no VSCode e o ambiente WSL ativo:

1. Liste todas as versões disponíveis do Python:
    ```bash
    pyenv install --list
    ```

2. Escolha uma versão e instale, por exemplo:
    ```bash
    pyenv install 3.7.0
    ```

3. Verifique se a instalação foi concluída com sucesso:
    ```bash
    pyenv versions
    ```

4. Configure o Python local para o projeto atual:
    ```bash
    pyenv local 3.7.0
    ```

    Isso criará um arquivo `.python-version` no diretório atual, indicando que o projeto está usando essa versão do Python.

---

## 🚧 Criando um Projeto com Poetry

```bash
poetry new project-test
```

Edite o `pyproject.toml` com as informações do seu projeto e pacote principal.

Exemplos:

```toml
# Estrutura: src/project_test
packages = [{ include = "project_test", from = "src" }]

# Estrutura: app/project_test
packages = [{ include = "project_test", from = "app" }]

# Estrutura direta: app
packages = [{ include = "app" }]
```

---

## 📚 Gerenciando Dependências

### Criando e ativando ambiente virtual:
1. Baixe o poetry shell:

    ```bash
    poetry self add poetry-plugin-shell
    ```

1. Ative o ambiente virtual:

    ```bash
    poetry shell
    ```

### Adicionando dependências:

```bash
poetry add "requests<2.28"
```

### Instalando todas as dependências do projeto:

```bash
poetry install
```

### Reescreva o arquivo poetry.lock:

```bash
poetry lock
```

---

## ▶️ Executando o Projeto

```bash
poetry run python meu_codigo.py
```
---

### Exemplo de docker-compose:

1. No diretorio crie um arquivo `docker-compose.yml` e adicione algo semelhante ao abaixo dentro dele:
  ```yml
  version: '3.9'

  services:
    api:
      build:
        context: .
        dockerfile: Dockerfile
      container_name: project-test # Aqui coloque o nome que deseja dar ao container
      ports:
        - "5000:5000" # Aqui coloque a porta que deseja mapear, se for a 8000, use 8000:8000
      env_file:
        - .env # Aqui coloque o caminho para o arquivo .env se tiver
      volumes:
        - .:/app # Aqui coloque o caminho para o projeto
      command: python run.py
      restart: unless-stopped
  ```

2. Crie um arquivo `Dockerfile` e adicione algo semelhante ao abaixo dentro dele:
  ```
  # Escolha a versão do Python que desejar
  FROM python:3.7-slim-buster 
  
  # Instala as dependências do sistema
  RUN apt-get update && \
      apt-get install -y \
      build-essential gcc libffi-dev libssl-dev && \
      rm -rf /var/lib/apt/lists/*
  
  RUN apt-get update && apt-get install -y gcc g++ libffi-dev libssl-dev
  
  # Cria o diretório de trabalho
  
  WORKDIR /app
  
  # Copia o arquivo requirements.txt e instala as dependências
  
  COPY requirements.txt .
  RUN python -m pip install --upgrade pip
  RUN pip install --no-cache-dir -r requirements.txt
  
  # Copia o restante do projeto
  
  COPY . .
  
  # Expose a porta 5000
  
  EXPOSE 5000
  
  # Comando para executar o projeto
  
  CMD ["python", "run.py"]
  ```

3. Rode o comando para subir o conteiner. Se não precisar reconstruir a imagem então não precisa do `--build`:
   ```bash
   docker compose up --build
   ```

---

## ✅ Verificação rápida

- `docker run hello-world` → Docker OK
- `pyenv --version` → Pyenv OK
- `poetry --version` → Poetry OK
- `.python-version` criado → Python local OK
- `poetry env info` mostra Python certo? → Virtualenv OK

---

## 🧠 Extras

- Repositório oficial do [Pyenv](https://github.com/pyenv/pyenv)
- Documentação do [Poetry](https://python-poetry.org/docs/)
- Página do [WSL](https://learn.microsoft.com/pt-br/windows/wsl/)
- Testado no Ubuntu via WSL 2 com sucesso 🎉

---

Feito com 💻 e café por Ruben Adriel
