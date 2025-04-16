
# ⚙️ Ambiente de Desenvolvimento com WSL, Docker, Pyenv e Poetry

Este repositório contém um guia completo e passo a passo para configurar um ambiente de desenvolvimento Python usando **WSL (Ubuntu)**, **Docker**, **pyenv** e **Poetry**.

---

## 📦 Tecnologias Utilizadas

- WSL 2 (Ubuntu)
- Docker & Docker Compose
- Pyenv
- Poetry
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
  - [🚧 Criando um Projeto com Poetry](#-criando-um-projeto-com-poetry)
  - [📚 Gerenciando Dependências](#-gerenciando-dependências)
    - [Criando e ativando ambiente virtual:](#criando-e-ativando-ambiente-virtual)
    - [Adicionando dependências:](#adicionando-dependências)
    - [Instalando todas as dependências do projeto:](#instalando-todas-as-dependências-do-projeto)
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
sudo apt install docker.io -y
sudo service docker start
sudo usermod -aG docker $USER
```

Reinicie o WSL:

```bash
wsl --shutdown
wsl -d Ubuntu
```

Instale o Docker Compose:

```bash
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.24.6/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
```

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

```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
source ~/.bashrc
```

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

## 🚧 Criando um Projeto com Poetry

```bash
poetry new project-test
cd project-test
mv ../.python-version .
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

```bash
poetry env use python
poetry env activate
```

### Adicionando dependências:

```bash
poetry add "requests<2.28"
```

### Instalando todas as dependências do projeto:

```bash
poetry install
```

---

## ▶️ Executando o Projeto

```bash
poetry run python meu_codigo.py
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