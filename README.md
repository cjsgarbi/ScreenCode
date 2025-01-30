# screenshot-to-code
Uma ferramenta simples para converter capturas de tela, mockups e designs Figma em código limpo e funcional usando IA. **Agora com suporte para Claude Sonnet 3.5 e Gemini 2.0 Flash!**

https://github.com/abi/screenshot-to-code/assets/23818/6cebadae-2fe3-4986-ac6a-8fb9db030045

Pilhas suportadas:

- HTML + Tailwind
- HTML + CSS
- React + Tailwind
- Vue + Tailwind
- Bootstrap
- Ionic + Tailwind
- SVG

Modelos de IA suportados:

- Claude Sonnet 3.5 - Melhor modelo!
- GPT-4o - também recomendado!
- DALL-E 3 ou Flux Schnell (usando Replicate) para geração de imagens

Veja a seção [Exemplos](#-examples) abaixo para mais demonstrações.

Também adicionamos suporte experimental para fazer uma gravação de vídeo/tela de um site em ação e transformá-lo em um protótipo funcional.

![google in app quick 3](https://github.com/abi/screenshot-to-code/assets/23818/8758ffa4-9483-4b9b-bb66-abd6d1594c33)

[Saiba mais sobre vídeo aqui](https://github.com/abi/screenshot-to-code/wiki/Screen-Recording-to-Code).

[Siga-me no Twitter para atualizações](https://twitter.com/_abi_).## 🌍  Hosted Version

[Try it live on the hosted version (paid)](https://screenshottocode.com). If you're a large or medium enterprise (50+ employees), [book a meeting to explore custom enterprise plans](https://cal.com/abi-raja-wy2pfh/30min).

## 🛠 Primeiros passos

O aplicativo tem um frontend React/Vite e um backend FastAPI.

Chaves necessárias:

- [Chave de API OpenAI com acesso ao GPT-4](https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md) ou chave Anthropic (opcional)
- Ambas são recomendadas para que você possa comparar os resultados do Claude e do GPT4o

Se você quiser executar o aplicativo com modelos de código aberto Ollama (não recomendado devido aos resultados de baixa qualidade), [siga este comentário](https://github.com/abi/screenshot-to-code/issues/354#issuecomment-2435479853).

** Informações uteis:

O backend não carrega junto com o frontend. Eles são projetos separados e precisam ser iniciados separadamente. O frontend é iniciado usando vite e o backend é iniciado usando uvicorn.

Instale no venv o yam caso não tenha instalado:
```bash
python -m venv venv
```
```bash
venv\Scripts\activate
```
```bash
yarn --version
```
```bash
npm install -g yarn
```
kenExecute detro do backend depois que entrar em cd backend(eu uso Poetry para gerenciamento de pacotes - `pip install poetry` se você não tiver) , as apiS podem ser adcionadas depois :
Siga estas etapas para configurar o projeto e executar a aplicação:

Navegue até o diretório backend:
```bash
cd backend
```
Ative o ambiente virtual:
```bash
venv\Scripts\activate
```
Limpe o cache do pip (recomendado para evitar erros de instalação):
```bash
pip cache purge
```
Crie um arquivo .env e adicione suas chaves de API:
```bash
echo "OPENAI_API_KEY=sk-your-key" > .env
echo "ANTHROPIC_API_KEY=your-key" > .env
```
IMPORTANTE: Substitua sk-your-key pela sua chave da API do OpenAI e your-key pela sua chave da API do Anthropic.

Edite o arquivo pyproject.toml:

Abra o arquivo backend/pyproject.toml e adicione a seguinte linha dentro da seção [tool.poetry], caso não exita :
```bash
packages = [{include = "backend"}]
```
Isso instrui o poetry a incluir o diretório backend como um pacote.

Instale as dependências:
```bash
poetry install
```
Este comando instala todas as dependências necessárias, incluindo o projeto backend.

Execute a aplicação:
```bash
poetry run uvicorn main:app --reload --port 7860
```
Este comando inicia o servidor Uvicorn, executando a aplicação FastAPI. O parâmetro --reload ativa o recarregamento automático para desenvolvimento, e --port 7860 define a porta na qual a aplicação será executada.


Instale no venv o yam caso não tenha instalado:
```bash
python -m venv venv
```
```bash
venv\Scripts\activate
```
```bash
yarn --version
```
```bash
npm install -g yarn
```
Com essas etapas, você terá configurado o projeto com sucesso e estará com a aplicação em execução!
```bash
npm install -g yarn
cd backend
pip cache purge
echo "OPENAI_API_KEY=sk-your-key" > .env
echo "ANTHROPIC_API_KEY=your-key" > .env

del poetry.lock
pip install poetry
poetry install
poetry run

poetry shell
poetry run uvicorn main:app --reload --port 7001

```
Você também pode configurar as chaves usando a caixa de diálogo de configurações no frontend (clique no ícone de engrenagem após carregar o frontend).

Execute o frontend:

```bash
cd frontend
yarn
yarn dev
```

Abra http://localhost:5173 para usar o aplicativo.

Se você preferir executar o backend em uma porta diferente, atualize VITE_WS_BACKEND_URL em `frontend/.env.local`

Para fins de depuração, se você não quiser desperdiçar créditos do GPT4-Vision, você pode executar o backend no modo simulado (que transmite uma resposta pré-gravada):

```bash
MOCK=true poetry run uvicorn main:app --reload --port 7001
```

## Docker

Se você tiver o Docker instalado no seu sistema, no diretório raiz, execute:

```bash
echo "OPENAI_API_KEY=sk-your-key" > .env
docker-compose up -d --build

```

O aplicativo estará instalado e funcionando em http://localhost:5173. Observe que você não pode desenvolver o aplicativo com esta configuração, pois as alterações no arquivo não acionarão uma reconstrução.

## 🙋‍♂️ Perguntas frequentes

- **Estou encontrando um erro ao configurar o backend. Como posso consertar?** [Tente isto](https://github.com/abi/screenshot-to-code/issues/3#issuecomment-1814777959). Se isso ainda não funcionar, abra um problema.

- **Como obtenho uma chave de API OpenAI?** Veja https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md

- **Como posso configurar um proxy OpenAI?** - Se você não conseguir acessar a API OpenAI diretamente (devido a restrições de país, por exemplo), você pode tentar uma VPN ou pode configurar a URL base OpenAI para usar um proxy: Defina OPENAI_BASE_URL em `backend/.env` ou diretamente na IU na caixa de diálogo de configurações. Certifique-se de que a URL tenha "v1" no caminho para que fique assim: `https://xxx.xxxxx.xxx/v1`

- **Como posso atualizar o host de backend ao qual meu front-end se conecta?** - Configure VITE_HTTP_BACKEND_URL e VITE_WS_BACKEND_URL em front/.env.local Por exemplo, defina VITE_HTTP_BACKEND_URL=http://124.10.20.1:7001

- **Está vendo erros UTF-8 ao executar o backend?** - No Windows, abra o arquivo .env com o notepad++, vá para Codificação e selecione UTF-8.

- **Como posso fornecer feedback?** Para feedback, solicitações de recursos e relatórios de bugs, abra um problema ou me envie um ping no [Twitter](https://twitter.com/_abi_).

## 📚 Exemplos

**NYTimes**

| Original | Réplica                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img width="1238" alt="Captura de tela 2023-11-20 às 12 54 03 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/3b644dfa-9ca6-4148-84a7-3405b6671922"> | <img width="1414" alt="Captura de tela 2023-11-20 às 12 59 56 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/26201c9f-1a28-4f35-a3b1-1f04e2b8ce2a"> |

**Página do Instagram (sem fotos de Taylor Swift)**

https://github.com/abi/screenshot-to-code/assets/23818/503eb86a-356e-4dfc-926a-dabdb1ac7ba1

**Hacker News** mas ele erra as cores no começo, então nós o cutucamos

https://github.com/abi/screenshot-to-code/assets/23818/3fec0f77-44e8-4fb3-a769-ac7410315e5d#   S c r e e n C o d e 
 
 