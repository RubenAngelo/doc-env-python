# ⚙️ Desenvolvimento Python com WSL, Docker, Pyenv, Poetry e Git

Guia completo para configurar um ambiente de desenvolvimento Python usando **WSL (Ubuntu)**, **Docker**, **Pyenv**, **Poetry**, e **Git**. Inclui instruções para configurar o ambiente e comandos Git essenciais para o dia a dia.

---

## 📦 Tecnologias

- WSL 2 (Ubuntu)
- Docker & Docker Compose
- Pyenv
- Poetry
- Git
- Python 3.x
- Visual Studio Code (opcional)

---

## 📖 Índice

- [⚙️ Desenvolvimento Python com WSL, Docker, Pyenv, Poetry e Git](#️-desenvolvimento-python-com-wsl-docker-pyenv-poetry-e-git)
  - [📦 Tecnologias](#-tecnologias)
  - [📖 Índice](#-índice)
  - [🔧 Configuração do WSL](#-configuração-do-wsl)
  - [🐳 Configuração do Docker](#-configuração-do-docker)
  - [🐍 Configuração do Pyenv](#-configuração-do-pyenv)
    - [Dependências](#dependências)
    - [Instalação](#instalação)
    - [Configuração no Shell](#configuração-no-shell)
    - [Verificação](#verificação)
  - [📦 Configuração do Poetry](#-configuração-do-poetry)
    - [Dependências](#dependências-1)
    - [Instalação](#instalação-1)
    - [Configuração](#configuração)
    - [Verificação](#verificação-1)
  - [📂 Configuração do Git](#-configuração-do-git)
    - [Instalação](#instalação-2)
    - [Configuração Inicial](#configuração-inicial)
    - [Comandos Git Essenciais](#comandos-git-essenciais)
  - [🧠 Integração com VSCode](#-integração-com-vscode)
  - [🛠️ Configurando o Projeto](#️-configurando-o-projeto)
  - [🚧 Criando Projeto com Poetry](#-criando-projeto-com-poetry)
  - [📚 Gerenciando Dependências](#-gerenciando-dependências)
    - [Ativar Ambiente Virtual](#ativar-ambiente-virtual)
    - [Adicionar Dependências](#adicionar-dependências)
    - [Instalar Dependências](#instalar-dependências)
    - [Atualizar `poetry.lock`](#atualizar-poetrylock)
  - [▶️ Executando o Projeto](#️-executando-o-projeto)
  - [🐳 Docker Compose Exemplo](#-docker-compose-exemplo)
  - [✅ Verificação Rápida](#-verificação-rápida)
  - [🧠 Extras](#-extras)

---

## 🔧 Configuração do WSL

1. No Prompt de Comando (não precisa ser administrador):
   ```bash
   wsl --install
   ```

2. Acesse o Ubuntu:
   ```bash
   wsl -d Ubuntu
   ```

3. Crie usuário e senha quando solicitado.

4. Atualize pacotes:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

## 🐳 Configuração do Docker

1. Instale Docker e Docker Compose:
   ```bash
   sudo apt install -y docker.io docker-compose-plugin
   sudo usermod -aG docker $USER
   newgrp docker
   ```

2. Reinicie o WSL (No prompt do windows fora do WSL):
   ```bash
   wsl --shutdown
   wsl -d Ubuntu
   ```

3. Start e Teste:
   ```bash
   sudo service docker start
   docker run hello-world
   ```

---

## 🐍 Configuração do Pyenv

### Dependências
```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
libffi-dev liblzma-dev git
```

### Instalação
```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

### Configuração no Shell
1. Edite `~/.bashrc`:
   ```bash
   nano ~/.bashrc
   ```

2. Adicione ao final:
   ```bash
   export PYENV_ROOT="$HOME/.pyenv"
   export PATH="$PYENV_ROOT/bin:$PATH"
   eval "$(pyenv init --path)"
   eval "$(pyenv init -)"
   ```

3. Salve: `Ctrl+O`, `Enter`, `Ctrl+X`.

4. Atualize o shell:
   ```bash
   source ~/.bashrc
   ```

### Verificação
```bash
pyenv --version
```

---

## 📦 Configuração do Poetry

### Dependências
```bash
sudo apt install -y curl python3-pip
```

### Instalação
```bash
curl -sSL https://install.python-poetry.org | python3 -
```

### Configuração
```bash
export PATH="$HOME/.local/bin:$PATH"
source ~/.bashrc
```

### Verificação
```bash
poetry --version
```

---

## 📂 Configuração do Git

### Instalação
Git já está incluído nas dependências do Pyenv. Verifique:
```bash
git --version
```

### Configuração Inicial
1. Configure nome e e-mail:
   ```bash
   git config --global user.name "Seu Nome"
   git config --global user.email "seu.email@exemplo.com"
   ```

2. Configure o editor padrão (exemplo: nano):
   ```bash
   git config --global core.editor nano
   ```

### Comandos Git Essenciais
- **Iniciar um repositório**:
  ```bash
  git init
  git add .
  git commit -m "Initial commit"
  ```

- **Clonar um repositório**:
  ```bash
  git clone https://github.com/usuario/repositorio.git
  ```

- **Adicionar e confirmar alterações**:
  ```bash
  git add .              # Adiciona todas as alterações
  git commit -m "Descrição da alteração"
  ```

- **Verificar status**:
  ```bash
  git status
  ```

- **Ver histórico de commits**:
  ```bash
  git log --oneline
  ```

- **Criar e mudar para uma branch**:
  ```bash
  git checkout -b nome-da-branch
  ```

- **Enviar alterações para o repositório remoto**:
  ```bash
  git push origin nome-da-branch
  ```

- **Atualizar repositório local**:
  ```bash
  git pull origin main
  ```

- **Mesclar branch**:
  ```bash
  git checkout main
  git merge nome-da-branch
  ```

- **Resolver conflitos** (edite os arquivos conflitantes, depois):
  ```bash
  git add .
  git commit
  ```

- **Revertendo commits**:
  ```bash
  git revert id-do-commit
  ```

- **Resetando commits**:
  ```bash
  git reset --hard id-do-commit-anterior
  ```

- **Alterando commits**:
  ```bash
  git commit --amend -m "Descrição da alteração"
  ```


---

## 🧠 Integração com VSCode

1. Abra o projeto no VSCode.
2. Abra o terminal integrado: `Ctrl+J`.
3. Selecione **Ubuntu (WSL)** no menu do terminal.

---

## 🛠️ Configurando o Projeto

1. Liste versões do Python disponíveis:
   ```bash
   pyenv install --list
   ```

2. Instale uma versão (exemplo: 3.9.0):
   ```bash
   pyenv install 3.9.0
   ```

3. Verifique:
   ```bash
   pyenv versions
   ```

4. Defina a versão local:
   ```bash
   pyenv local 3.9.0
   ```

---

## 🚧 Criando Projeto com Poetry

```bash
poetry new meu-projeto
cd meu-projeto
```

Edite `pyproject.toml` para configurar o projeto:
```toml
[tool.poetry]
name = "meu-projeto"
version = "0.1.0"
description = "Descrição do projeto"
authors = ["Seu Nome <seu.email@exemplo.com>"]

[tool.poetry.dependencies]
python = "^3.9"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

---

## 📚 Gerenciando Dependências

### Ativar Ambiente Virtual
```bash
poetry shell
```

### Adicionar Dependências
```bash
poetry add requests
```

### Instalar Dependências
```bash
poetry install
```

### Atualizar `poetry.lock`
```bash
poetry lock
```

---

## ▶️ Executando o Projeto

```bash
poetry run python main.py
```

---

## 🐳 Docker Compose Exemplo

1. Crie `docker-compose.yml`:
   ```yaml
   version: '3.9'
   services:
     app:
       build:
         context: .
         dockerfile: Dockerfile
       container_name: meu-projeto
       ports:
         - "8000:8000"
       volumes:
         - .:/app
       command: poetry run python main.py
       restart: unless-stopped
   ```

2. Crie `Dockerfile`:
   ```dockerfile
   FROM python:3.9-slim
   WORKDIR /app
   COPY pyproject.toml poetry.lock ./
   RUN pip install poetry && poetry install --no-dev
   COPY . .
   EXPOSE 8000
   CMD ["poetry", "run", "python", "main.py"]
   ```

3. Execute:
   ```bash
   docker compose up --build
   ```

---

## ✅ Verificação Rápida

- Docker: `docker run hello-world`
- Pyenv: `pyenv --version`
- Poetry: `poetry --version`
- Git: `git --version`
- Python local: Verifique `.python-version`
- Ambiente virtual: `poetry env info`

---

## 🧠 Extras

- [Pyenv](https://github.com/pyenv/pyenv)
- [Poetry](https://python-poetry.org/docs/)
- [WSL](https://learn.microsoft.com/pt-br/windows/wsl/)
- [Git](https://git-scm.com/doc)
- Testado no Ubuntu via WSL 2 🎉

---

Feito com 💻 e ☕ por Ruben Adriel
