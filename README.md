# 🚀 Terminal Google Colab + Ollama + Ngrok

[![Licença: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

> Execute modelos LLM localmente no Google Colab com GPU gratuita e exponha via ngrok para usar no VS Code!

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Pré-requisitos](#-pré-requisitos)
- [Como Usar](#-como-usar)
- [Configuração no VS Code](#-configuração-no-vs-code)
- [Performance Esperada](#-performance-esperada)
- [Solução de Problemas](#-solução-de-problemas)
- [Contribuindo](#-contribuindo)
- [Licença](#-licença)

## 🎯 Sobre o Projeto

Este projeto permite rodar o modelo **Qwen2.5-Coder 7B** (ou qualquer outro modelo do Ollama) no **Google Colab** com aceleração por GPU (Tesla T4), e expô-lo publicamente via **ngrok** para ser consumido por ferramentas como:

- **Continue.dev** (VS Code)
- **Cline** (VS Code)
- Qualquer cliente compatível com API do Ollama

### ✨ Características

- ✅ **Totalmente gratuito** (uso do Colab gratuito)
- ✅ **GPU Tesla T4** com 16GB de VRAM
- ✅ **Qwen2.5-Coder 7B** otimizado para programação
- ✅ **Túnel ngrok** para acesso externo
- ✅ **Fácil integração** com VS Code
- ✅ **Código aberto** e extensível

## 📋 Pré-requisitos

Antes de começar, você precisa ter:

- [x] Uma conta **Google** (para acessar o Colab)
- [x] Uma conta **ngrok** (gratuita em [ngrok.com](https://ngrok.com))
- [x] **VS Code** com uma das extensões:
  - [Continue.dev](https://marketplace.visualstudio.com/items?itemName=Continue.continue)
  - [Cline](https://marketplace.visualstudio.com/items?itemName=saoudrizwan.claude-dev)

## 🚀 Como Usar

### Passo 1: No Google Colab

1. Acesse [Google Colab](https://colab.research.google.com/)
2. Crie um **Novo Notebook**
3. Em **Ambiente de execução > Alterar tipo de ambiente de execução**, selecione **GPU (T4)**
4. Copie o conteúdo do arquivo [`terminal_ollama.txt`](terminal_ollama.txt)
5. Cole em uma célula do notebook e execute (`Ctrl+Enter`)
6. Aguarde o download do modelo (cerca de 5-10 minutos)
7. Ao final, **copie a URL gerada** (ex: `https://xxxx.ngrok-free.dev`)

> ⚠️ **Importante**: Mantenha a aba do Colab **ativa e aberta** enquanto estiver usando. Se ficar inativa, a sessão pode ser encerrada.

### Passo 2: Configurar o ngrok (token)

O script usa seu token do ngrok para criar o túnel. Substitua no script a linha:

```python
NGROK_TOKEN = "SEU_TOKEN_AQUI"
```

Pelo seu token que você encontra no [dashboard do ngrok](https://dashboard.ngrok.com/get-started/your-authtoken).

### Passo 3: Configurar no VS Code

#### Com Continue.dev

Edite o arquivo `~/.continue/config.yaml`:

```yaml
models:
  - name: Qwen Coder 7B (Ngrok)
    provider: ollama
    model: qwen2.5-coder:7b
    apiBase: https://SUA_URL_AQUI.ngrok-free.dev
    requestOptions:
      headers:
        ngrok-skip-browser-warning: "true"
    roles:
      - chat
      - edit
    contextLength: 32768
```

#### Com Cline

No Cline, configure:

- **API Provider**: Ollama
- **Base URL**: `https://SUA_URL_AQUI.ngrok-free.dev`
- **API Key**: (deixar em branco)
- **Model**: `qwen2.5-coder:7b`

### Passo 4: Pronto!

Agora você tem um assistente de IA gratuito rodando na nuvem, integrado ao seu VS Code!

## 📊 Performance Esperada

| Característica | Valor |
|:---|:---|
| **GPU** | NVIDIA Tesla T4 (16GB VRAM) |
| **Modelo** | Qwen2.5-Coder 7B (Q4_K_M) |
| **Velocidade** | ~20-30 tokens/segundo |
| **Contexto** | 32.768 tokens |
| **Tempo de download** | ~5-10 minutos |
| **Tempo de sessão** | 5-12 horas (Colab gratuito) |

## 🔧 Solução de Problemas

### Erro: "A URL não responde"

**Solução**: A URL do ngrok muda a cada sessão do Colab. Execute o script novamente e atualize a URL no VS Code.

### Erro: "403 Forbidden" no ngrok

**Solução**: Certifique-se de que o header `ngrok-skip-browser-warning: "true"` está sendo enviado nas requisições.

### Erro: "Session expired" no Colab

**Solução**: Mantenha a aba do Colab ativa. Considere usar o Colab Pro+ se precisar de sessões mais longas.

### O modelo não baixa

**Solução**: Verifique se o token do ngrok está correto e se você está com GPU ativada no Colab.

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um **fork** do projeto
2. Crie uma **branch** para sua feature (`git checkout -b feature/nova-feature`)
3. Faça o **commit** das mudanças (`git commit -m 'Adiciona nova feature'`)
4. Faça o **push** para a branch (`git push origin feature/nova-feature`)
5. Abra um **Pull Request**

### Sugestões de Melhorias

- Adicionar suporte a outros modelos (Llama, Mistral, etc.)
- Criar um script com Tailscale (URL privada)
- Adicionar monitoramento de status do túnel
- Documentar como usar com outras extensões do VS Code

## 📄 Licença

Distribuído sob a licença **MIT**. Veja [LICENSE](LICENSE) para mais informações.

---

## 🌟 Créditos

- [Ollama](https://ollama.com/) - Framework para rodar LLMs localmente
- [Ngrok](https://ngrok.com/) - Túneis públicos seguros
- [Qwen2.5-Coder](https://qwenlm.ai/) - Modelo de código da Alibaba
- [Google Colab](https://colab.research.google.com/) - Ambiente de execução gratuito

---

Feito com ❤️ por [tonychagas](https://github.com/tonychagas)

⭐ Se este projeto te ajudou, considere dar uma estrela no GitHub
