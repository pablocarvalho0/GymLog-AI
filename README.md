# 🏋️‍♂️ GymLog AI 🤖

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)
![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-green)

Um chatbot para Telegram que utiliza Inteligência Artificial para registrar e analisar treinos de academia a partir de mensagens em linguagem natural.

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [✨ Funcionalidades](#-funcionalidades)
- [🛠️ Tecnologias Utilizadas](#️-tecnologias-utilizadas)
- [🚀 Começando](#-começando)
  - [Pré-requisitos](#pré-requisitos)
  - [Instalação](#instalação)
- [⚙️ Configuração](#️-configuração)
- [▶️ Uso](#️-uso)
- [🗺️ Roteiro de Desenvolvimento](#️-roteiro-de-desenvolvimento)
- [🤝 Contribuição](#-contribuição)
- [📄 Licença](#-licença)
- [📧 Contato](#-contato)

## 📖 Sobre o Projeto

O **GymLog AI** nasceu da necessidade pessoal de transformar anotações de treino, antes feitas de forma desorganizada em grupos de WhatsApp, em dados estruturados e acionáveis. A dificuldade em consultar o histórico, medir o progresso de cargas e analisar a frequência dos treinos era um obstáculo para um acompanhamento de performance eficaz.

Este projeto resolve esse problema através de um assistente virtual no Telegram. O usuário simplesmente descreve seu treino em uma mensagem, e o bot, com o auxílio da API da OpenAI, interpreta, estrutura e armazena essas informações em um banco de dados, pronto para futuras consultas e análises visuais.

### Diagrama da Arquitetura
```
Usuário --> Telegram --> Bot (Python) --> OpenAI API (para estruturar)
   ^                                             |
   |                                             V
Relatório <-- Imagem (Matplotlib) <-- API (FastAPI) <-- Banco de Dados (SQLite)
```

## ✨ Funcionalidades

- **✍️ Registro via Linguagem Natural:** Envie uma mensagem como se estivesse anotando para si mesmo.
- **🧠 Extração de Dados com IA:** A API da OpenAI interpreta os detalhes do seu treino (exercícios, séries, pesos, repetições).
- **🗄️ Armazenamento Estruturado:** Os dados são salvos de forma organizada em um banco de dados SQLite.
- **📊 Geração de Relatórios:** Solicite relatórios de progresso e receba gráficos visuais da sua evolução.

## 🛠️ Tecnologias Utilizadas

Este projeto foi construído utilizando as seguintes tecnologias:

- **Back-end & Lógica do Bot:**
  - [Python 3.9+](https://www.python.org/)
  - [FastAPI](https://fastapi.tiangolo.com/)
  - [SQLAlchemy](https://www.sqlalchemy.org/)
  - [python-telegram-bot](https://python-telegram-bot.org/)
- **Inteligência Artificial:**
  - [OpenAI API](https://openai.com/api/)
- **Banco de Dados:**
  - [SQLite](https://www.sqlite.org/index.html)
- **Análise e Visualização:**
  - [Pandas](https://pandas.pydata.org/)
  - [Matplotlib](https://matplotlib.org/)
- **Desenvolvimento:**
  - [Uvicorn](https://www.uvicorn.org/)
  - [Ngrok](https://ngrok.com/) (para desenvolvimento local)

## 🚀 Começando

Para obter uma cópia local do projeto e colocá-la em funcionamento, siga estes passos.

### Pré-requisitos

Você precisará ter o seguinte software instalado em sua máquina:
- Python 3.9 ou superior
- Pip (gerenciador de pacotes do Python)
- Git (sistema de controle de versão)
- Uma conta na [OpenAI](https://platform.openai.com/) para obter uma chave de API.
- Uma conta no [Telegram](https://telegram.org/) e um token de bot gerado pelo [BotFather](https://t.me/botfather).
- O [Ngrok](https://ngrok.com/download) para expor seu servidor local à internet.

### Instalação

1. **Clone o repositório:**
   ```sh
   git clone [https://github.com/seu-usuario/gymlog-ai.git](https://github.com/seu-usuario/gymlog-ai.git)
   cd gymlog-ai
   ```

2. **Crie e ative um ambiente virtual (Recomendado):**
   ```sh
   # Para Linux/macOS
   python3 -m venv venv
   source venv/bin/activate

   # Para Windows
   python -m venv venv
   .\venv\Scripts\activate
   ```

3. **Instale as dependências:**
   Crie um arquivo `requirements.txt` com as bibliotecas necessárias e execute:
   ```sh
   pip install -r requirements.txt
   ```
   *Conteúdo do `requirements.txt`:*
   ```txt
   fastapi
   uvicorn[standard]
   sqlalchemy
   python-telegram-bot
   openai
   requests
   pandas
   matplotlib
   python-dotenv
   ```

## ⚙️ Configuração

As chaves de API e tokens são informações sensíveis e não devem ser enviadas para o Git.

1. **Crie um arquivo `.env`** na raiz do projeto, copiando o exemplo abaixo:
   ```sh
   cp .env.example .env
   ```
   *Se não tiver um `.env.example`, crie o `.env` manualmente.*

2. **Adicione suas credenciais** ao arquivo `.env`:
   ```env
   TELEGRAM_TOKEN="SEU_TOKEN_AQUI_DO_BOTFATHER"
   OPENAI_API_KEY="SUA_CHAVE_DE_API_AQUI_DA_OPENAI"
   ```

## ▶️ Uso

Para rodar o projeto, você precisará de 3 terminais abertos.

1. **Terminal 1: Inicie o Ngrok**
   Para expor sua API local na porta 8000 (porta padrão do FastAPI).
   ```sh
   ngrok http 8000
   ```
   *Copie a URL "Forwarding" que termina com `ngrok-free.app`. Você pode precisar dela para configurar webhooks no futuro.*

2. **Terminal 2: Inicie o Servidor FastAPI**
   Na raiz do projeto, execute:
   ```sh
   uvicorn main:app --reload
   ```
   *O `main` se refere ao arquivo `main.py` e `app` ao objeto FastAPI instanciado nele.*

3. **Terminal 3: Inicie o Bot do Telegram**
   Na raiz do projeto, execute:
   ```sh
   python bot.py
   ```
   *O `bot.py` é o arquivo que contém a lógica do seu bot.*

Agora, abra o Telegram, encontre seu bot e comece a enviar mensagens!

**Exemplo de Registro:**
> Fui na SmartFit hoje. Treino de peito.
> Supino reto 40kg 12 reps, 45kg 10 reps, 50kg 8 reps.
> Voador 30kg 15 reps, 35kg 12 reps.

**Exemplo de Solicitação de Relatório:**
> /relatorio evolução supino reto

## 🗺️ Roteiro de Desenvolvimento

- [ ] **MVP Básico:** Funcionalidades de registro e relatório de evolução por exercício.
- [ ] **Geração de Treinos:** Usar a IA para sugerir treinos com base no histórico.
- [ ] **Dashboard Web:** Criar uma interface web com React para visualizações mais ricas.
- [ ] **Deploy na Nuvem:** Mover o back-end para um serviço como Render ou Heroku.

Veja o [arquivo de projeto](./PROJETO_GYMLOG_AI.md) para mais detalhes.

## 🤝 Contribuição

Contribuições são o que tornam a comunidade de código aberto um lugar incrível para aprender, inspirar e criar. Qualquer contribuição que você fizer será **muito bem-vinda**.

Se você tiver uma sugestão para melhorar este projeto, por favor, faça um fork do repositório e crie uma pull request. Você também pode simplesmente abrir uma issue com a tag "enhancement". Não se esqueça de dar uma estrela ao projeto! Obrigado novamente!

1. Faça um Fork do projeto
2. Crie sua Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Faça o Commit de suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Faça o Push para a Branch (`git push origin feature/AmazingFeature`)
5. Abra uma Pull Request

## 📄 Licença

Distribuído sob a Licença MIT. Veja `LICENSE.txt` para mais informações.

## 📧 Contato

| Plataforma | Contato                                                                  |
| :--------- | :----------------------------------------------------------------------- |
| 👤 **Nome** | Pablo Carvalho do Nascimento dos Santos                                  |
| 📧 **Email** | `pablocnsantos2@gmail.com`                                               |
| 💼 **LinkedIn** | [Pablo Carvalho](https://www.linkedin.com/in/pablo-carvalho-pcns8896/)              |
| 💻 **Projeto** | [Repositório no GitHub](https://github.com/pablocarvalho0/gymlog-ai)       |
