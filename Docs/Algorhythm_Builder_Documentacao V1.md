# 🧠 Algorhythm Builder – Documentação Técnica Inicial

## 📌 Visão Geral

**Algorhythm Builder** é uma plataforma de desenvolvimento assistido por IA, onde o usuário descreve em texto (ou imagem) o que deseja construir e a aplicação:

- Interpreta o pedido com um agente de IA
- Planeja e gera código automaticamente
- Apresenta os resultados de forma organizada e iterável

## 🧱 Arquitetura do Projeto

```txt
Algorhythm Builder (Next.js App)
├── Frontend (React + TailwindCSS + shadcn/ui)
│   ├── PromptInput.tsx      → Entrada de comandos do usuário
│   ├── OutputPanel.tsx      → Exibição dos códigos gerados
│   ├── ImageUpload.tsx      → Upload de imagens (Figma/layouts)
│   ├── Sidebar.tsx          → Navegação geral do app
│   └── Projects.tsx         → (futuro) histórico de projetos
│
├── Backend (API Routes Next.js)
│   ├── /api/generate        → Conecta com Mistral (texto → código)
│   ├── /api/image           → Conecta com OpenAI GPT-4o (imagem → descrição)
│   └── /api/agent (futuro)  → Conecta com agentes autônomos da Mistral
│
├── lib/
│   └── ai.ts                → Funções utilitárias de IA (Mistral / OpenAI)
```

---

## 🔄 Fluxo de Funcionamento

### 1. Texto → Código

- Usuário digita um comando como:
  > “Crie uma landing page com cabeçalho, texto e botão.”
- API chama `Mistral` usando chat/completions
- A IA responde com:
  - Explicação do layout
  - Código React + Tailwind
- Resultado é exibido no `OutputPanel`

### 2. Imagem → Descrição (→ Código)

- Usuário envia uma imagem (Figma, print etc.)
- A imagem é convertida para URL
- Enviada ao `GPT-4o` via endpoint multimodal
- A IA responde com:
  - Descrição textual da interface (ex: "tela com cabeçalho e botão azul")
- Essa descrição pode ser reutilizada para gerar código com Mistral

---

## 🧠 Integração com IA

### ✨ Mistral API (via Groq ou direta)

- Modelo: `mistral-small` ou `mixtral-8x7b`
- Função: geração de código, respostas explicativas, estruturação

### 🖼️ OpenAI GPT-4o

- Usado apenas para análise de imagem
- Input: imagem por URL
- Output: descrição textual do layout (usada como prompt)

### (Futuro) Agentes Mistral

- Planejamento autônomo com memória
- Criação de componentes coordenados (ex: Header + Footer + Logic)

---

## 🔐 Segurança

- Tokens de API ficam **protegidos** em `.env` (não expostos no client)
- Toda comunicação com IA passa por **API Routes do Next.js**
- Possibilidade de rate limit e log de uso

---

## 💡 Componentes por função

| Componente    | Responsabilidade                               |
| ------------- | ---------------------------------------------- |
| `Sidebar`     | Menu lateral com abas e navegação geral        |
| `PromptInput` | Campo de input tipo ChatGPT com botão de envio |
| `OutputPanel` | Exibição do código/explicação retornado        |
| `ImageUpload` | Upload de imagem + preview + envio             |
| `Projects`    | (Futuro) Listagem de projetos gerados          |

---

## 🚀 Próximas Etapas Técnicas

1. Criar estrutura base do projeto Next.js com Tailwind + shadcn
2. Configurar as API Routes `/api/generate` e `/api/image`
3. Conectar com Mistral e OpenAI via lib `ai.ts`
4. Implementar componente `PromptInput` com envio de texto
5. Mostrar resultado formatado em `OutputPanel`
6. Implementar `ImageUpload` com integração GPT-4o (via URL)
7. Criar pasta "Projetos" para histórico (persistência futura)

---

> Essa documentação servirá como base viva para o desenvolvimento do Algorhythm Builder. Vamos construir com clareza, eficiência e visão de longo prazo. 💡
