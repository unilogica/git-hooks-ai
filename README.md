Claro\! Um bom `README.md` é essencial para qualquer projeto.

Aqui está uma proposta de `README.md` completa e bem estruturada para um repositório no GitHub que ensina como configurar e usar os scripts que criamos. O texto está em português e formatado em Markdown.

-----

# Mensagens de Commit Automáticas com IA

[](https://opensource.org/licenses/MIT)

Cansado de escrever mensagens de commit? Este projeto utiliza um simples hook do Git para gerar mensagens de commit claras, concisas e padronizadas usando o poder das APIs da **OpenAI** ou do **Google Gemini**.

Ele se integra perfeitamente ao seu fluxo de trabalho, analisando suas alterações (`git diff`) e sugerindo uma mensagem de commit informativa, seguindo o padrão **Conventional Commits**.

*(Exemplo de como o editor abre com a mensagem já preenchida)*

## Principais Funcionalidades

  - **Geração Automática:** Cria mensagens de commit com base nas suas alterações em stage.
  - **Suporte a Múltiplos Provedores:** Escolha entre a API da OpenAI (ex: GPT-4o mini) ou do Google (ex: Gemini 1.5 Flash).
  - **Padrão Profissional:** As mensagens são formatadas seguindo o padrão [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/), melhorando a legibilidade do seu histórico.
  - **Integração Perfeita:** Funciona diretamente com o comando `git commit`. A experiência é ainda melhor com `git commit -v`.
  - **Fácil de Configurar:** Apenas um arquivo e uma variável de ambiente são necessários.

## Pré-requisitos

Antes de começar, garanta que você tenha os seguintes softwares instalados:

1.  **Git:** O sistema de controle de versão.
2.  **cURL:** Ferramenta para fazer requisições web. Geralmente já vem instalada na maioria dos sistemas.
3.  **jq:** Um processador de JSON para a linha de comando. É **essencial** para o funcionamento do script.
      - **No Debian/Ubuntu:** `sudo apt-get install jq`
      - **No macOS (com Homebrew):** `brew install jq`
4.  **Chave de API:** Você precisará de uma chave de API de um dos provedores:
      - **OpenAI:** Obtenha sua chave no [painel da OpenAI](https://platform.openai.com/api-keys).
      - **Google Gemini:** Obtenha sua chave no [Google AI Studio](https://aistudio.google.com/app/apikey).

## Instalação

A configuração é feita dentro do seu repositório Git local.

### 1\. Clone este Repositório (Opcional)

Se você quiser ter os scripts como parte de um projeto, pode clonar este repositório. Caso contrário, apenas copie o conteúdo do script desejado. Para este guia, vamos supor que você clonou o repositório.

```bash
git clone https://github.com/SEU_USUARIO/SEU_REPO.git
cd SEU_REPO
```

### 2\. Escolha e Configure o Hook

Este repositório contém dois scripts:

  - `openai/prepare-commit-msg`
  - `gemini/prepare-commit-msg`

Você precisa criar um link simbólico de um deles para o diretório de hooks do seu projeto. Dentro da pasta do seu projeto, execute:

**Para usar OpenAI:**

```bash
ln -s ../../openai/prepare-commit-msg .git/hooks/prepare-commit-msg
```

**OU**

**Para usar Google Gemini:**

```bash
ln -s ../../gemini/prepare-commit-msg .git/hooks/prepare-commit-msg
```

*Este método com link simbólico é ótimo porque qualquer atualização que você fizer no script (via `git pull`) será refletida automaticamente no hook. Porém se preferir simplesmente copiar / colar fique a vontade.*

### 3\. Dê Permissão de Execução

O Git exige que os arquivos de hook sejam executáveis.

```bash
chmod +x .git/hooks/prepare-commit-msg
```

## Configuração

### 1\. Configure a Chave de API

O script lê a chave de API de uma variável de ambiente. Você deve adicioná-la ao seu arquivo de configuração de shell (como `.bashrc`, `.zshrc`, etc.) para não precisar defini-la toda vez.

**Se você escolheu OpenAI:**

```bash
export OPENAI_API_KEY="sk-SUA-CHAVE-DA-OPENAI-AQUI"
```

**Se você escolheu Google Gemini:**

```bash
export GEMINI_API_KEY="SUA-CHAVE-DO-GEMINI-AQUI"
```

Após adicionar a linha, reinicie seu terminal ou recarregue a configuração com `source ~/.bashrc` (ou o arquivo correspondente).

### 2\. (Opcional) Mude o Modelo da IA

Você pode facilmente alterar o modelo de IA editando o script. Procure a linha que define o modelo e substitua pelo de sua preferência (lembre-se de verificar a compatibilidade com a API).

  - No script da OpenAI, a linha é: `--arg model "gpt-4o-mini"`
  - No script do Gemini, a linha é: `"https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent?key=$GEMINI_API_KEY"`

## Como Usar

O fluxo de trabalho é o mesmo de sempre, mas com um toque de mágica.

1.  Faça suas alterações no código.
2.  Adicione os arquivos ao stage:
    ```bash
    git add .
    ```
3.  Execute o comando de commit. **Recomendamos usar a flag `-v` (verbose)** para ver o diff junto com a mensagem sugerida.
    ```bash
    git commit -v
    ```
    Ou, se quiser adicionar todas as alterações em arquivos já monitorados:
    ```bash
    git commit -av
    ```
4.  Seu editor de texto padrão será aberto, já preenchido com uma mensagem de commit gerada pela IA.
5.  Revise a mensagem. Você pode editá-la como quiser.
6.  Salve e feche o editor para finalizar o commit. Pronto\!

## Solução de Problemas

  - **Nada acontece:**
      - Verifique se o hook tem permissão de execução (`ls -l .git/hooks`).
      - Confirme se o link simbólico foi criado corretamente.
      - Certifique-se de que `jq` está instalado (`command -v jq`).
  - **Recebo um erro sobre a API:**
      - Verifique se a variável de ambiente (`OPENAI_API_KEY` ou `GEMINI_API_KEY`) está definida e exportada corretamente (`echo $SUA_VARIAVEL`).
      - Confirme se a sua chave de API está ativa e se você tem créditos ou um plano de faturamento ativo no provedor.

## Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo [LICENSE](https://www.google.com/search?q=LICENSE) para mais detalhes.
