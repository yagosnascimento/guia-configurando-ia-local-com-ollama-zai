---

# Guia Definitivo: Configurando sua IA Local com Ollama, Z.ai (GLM) e VS Code

Este guia fornece instruções detalhadas, passo a passo, para configurar um ambiente de desenvolvimento assistido por Inteligência Artificial rodando 100% localmente. Isso garante privacidade total dos dados, latência reduzida e isenção de custos de assinatura.

---

## Sumário
1. [Pré-requisitos de Hardware](#1-pré-requisitos-de-hardware)
2. [Passo 1: Instalando o Ollama](#2-passo-1-instalando-o-ollama)
3. [Passo 2: Baixando e Executando o Modelo Z.ai (GLM)](#3-passo-2-baixando-e-executando-o-modelo-zai-glm)
4. [Passo 3: Configurando o VS Code para Contexto de Código](#4-passo-3-configurando-o-vs-code-para-contexto-de-código)
5. [Passo 4: Indexando seu Repositório](#5-passo-4-indexando-seu-repositório)
6. [Dicas de Performance e Otimização](#6-dicas-de-performance-e-otimização)
7. [Solução de Problemas Comuns](#7-solução-de-problemas-comuns)

---

## 1. Pré-requisitos de Hardware

Rodar modelos de IA localmente exige recursos específicos. Verifique se seu sistema atende aos requisitos mínimos para o modelo **GLM-5.1**:

* **GPU (Recomendado):** NVIDIA com pelo menos 8GB de VRAM (série RTX 3060 ou superior). Em dispositivos Mac, processadores Apple Silicon (M1, M2, M3) com 16GB de RAM unificada apresentam excelente desempenho.
* **RAM:** Mínimo de 16GB. Caso não possua GPU dedicada, o Ollama utilizará a memória RAM; nesse cenário, 32GB é o ideal para modelos maiores.
* **Armazenamento:** Mínimo de 10GB de espaço livre em SSD. O uso de HDs convencionais impacta severamente a velocidade de resposta.
* **Sistema Operacional:** Windows 10/11, macOS ou distribuições Linux modernas.

---

## 2. Passo 1: Instalando o Ollama

O Ollama é o motor que permite gerenciar e rodar modelos de linguagem de forma simplificada.

1.  Acesse o site oficial: [ollama.com](https://ollama.com).
2.  Clique em **Download** e selecione sua plataforma (Windows, macOS ou Linux).
3.  Execute o instalador e siga as instruções na tela.
4.  Certifique-se de que o ícone do Ollama esteja visível na barra de tarefas, indicando que o servidor está ativo.
5.  Para validar a instalação, abra o terminal e execute:
    ```bash
    ollama --version
    ```

---

## 3. Passo 2: Baixando e Executando o Modelo Z.ai (GLM)

A Z.ai (Zhipu AI) desenvolve a família GLM, otimizada para raciocínio lógico e programação.

1.  Abra o terminal.
2.  Execute o comando para baixar e iniciar o modelo:
    ```bash
    ollama run glm-5.1:cloud
    ```
    > **Nota:** O modelo possui alguns gigabytes de tamanho. O tempo de conclusão dependerá da sua conexão de rede.
3.  Após o download, você poderá interagir com a IA diretamente no terminal. Digite `/exit` para encerrar a sessão.

---

## 4. Passo 3: Configurando o VS Code para Contexto de Código

Utilizaremos a extensão **Continue.dev** para integrar o VS Code ao Ollama.

1.  No **VS Code**, acesse a aba de **Extensões** (`Ctrl+Shift+X`).
2.  Pesquise por **"Continue"** e instale a versão oficial da `continue.dev`.
3.  Clique no ícone do Continue na barra lateral esquerda.
4.  Clique no ícone de engrenagem no painel da extensão e depois local config para abrir o arquivo `config.json`.
5.  Adicione a configuração do modelo na seção `models`:
    ```json
    {
      "models": [
        {
          "title": "Z.ai GLM 5.1",
          "provider": "ollama",
          "model": "glm-5.1:cloud"
        }
      ]
    }
    ```

---

## 5. Passo 4: Indexando seu Repositório

Esta etapa permite que a IA compreenda a estrutura e a lógica do seu projeto específico.

1.  Com o projeto aberto no VS Code, abra o painel do **Continue**.
2.  Localize a opção de indexação de codebase ou o ícone de pasta no campo de chat.
3.  Aguarde a criação do índice local (processo realizado uma única vez por projeto).
4.  **Comandos principais:**
    * **Contexto global:** Digite `@codebase` seguido da sua pergunta (ex: `@codebase Como funciona o fluxo de login?`).
    * **Contexto local:** Use `Ctrl + L` para adicionar trechos selecionados ao chat.
    * **Edição direta:** Use `Ctrl + I` para solicitar geração de código diretamente no arquivo ativo.

---

## 6. Dicas de Performance e Otimização

* **Quantização:** Se o tempo de resposta estiver alto, utilize versões quantizadas menores, como `glm-4:9b`.
* **Atualizações:** Mantenha o motor atualizado para garantir melhorias de performance executando `ollama update` quando disponível.
* **Gestão de Recursos:** Feche aplicações que consomem muita memória RAM (como navegadores com muitas abas) para priorizar o processamento dos tokens da IA.

---

## 7. Solução de Problemas Comuns

| Problema | Causa Provável | Solução |
| :--- | :--- | :--- |
| **"Ollama not found"** | Servidor não iniciado | Certifique-se de que o aplicativo Ollama está rodando na barra de tarefas. |
| **Respostas lentas** | Uso de CPU em vez de GPU | Verifique no Gerenciador de Tarefas se a carga está na GPU (Memória de Vídeo Dedicada). |
| **Erro de Conexão** | Configuração de porta incorreta | Garanta que a URL no `config.json` do Continue seja `http://localhost:11434`. |

---
*Yago Siqueira Nascimento - Este documento visa auxiliar na configuração de ambientes de desenvolvimento privados e eficientes.*
