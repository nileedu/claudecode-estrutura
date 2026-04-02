# Plano: 3 Novas Trilhas — Agentes de IA (T4, T5, T6)

## Contexto

O curso "Por Dentro do Claude Code" tem 3 trilhas (T1-T3) que explicam a arquitetura do Claude Code. O usuário quer **3 trilhas práticas adicionais** que ensinem a CONSTRUIR agentes de IA, usando os padrões do Claude Code como referência e culminando na criação de um agente local com Qwen + Ollama.

## Estrutura

### Trilha 4 — Fundamentos de Agentes (Amber)
**Para quem está começando. O que é um agente, como funciona, primeiros passos.**

| Módulo | Título | Tópicos (6 cada) |
|---|---|---|
| 4.1 | 🤖 O Que É um Agente de IA | Chatbot vs Agente, O loop fundamental, Ferramentas como superpoderes, Estado e memória, Autonomia e limites, Anatomia de um agente |
| 4.2 | 🔄 O Loop do Agente | Input → LLM → Tools → Results → Response, Por que o loop é infinito, Quando o agente para, Streaming vs batch, Tratamento de erros no loop, Seu primeiro loop em pseudocódigo |
| 4.3 | 🧰 Ferramentas (Tools) | O que é uma ferramenta, Anatomia: nome/descrição/parâmetros/execução, Tool calling: como o LLM escolhe, Validação de entrada, Permissões e segurança, Ferramentas essenciais (read/write/shell/search) |
| 4.4 | 🧠 Memória e Contexto | Janela de contexto explicada, Contexto = memória de trabalho, Memória persistente vs sessão, Compressão de contexto, System prompt como DNA do agente, CLAUDE.md e configuração |

### Trilha 5 — Construindo um Agente Completo (Teal)
**Planejando e executando passo a passo com MUITOS exemplos de código Python.**

| Módulo | Título | Tópicos (6 cada) |
|---|---|---|
| 5.1 | 📐 Arquitetando Seu Agente | Definindo o escopo, Stack tecnológica (Python + Ollama), Componentes essenciais, Padrão de projeto: Tool Registry, Padrão: Context Manager, Padrão: Permission Controller |
| 5.2 | 🔧 Construindo o Sistema de Ferramentas | Classe base Tool, Implementando read_file/write_file, Implementando run_shell com segurança, Implementando search_in_files (grep), Registro e descoberta de ferramentas, Execução paralela vs sequencial |
| 5.3 | 🧠 Construindo o Sistema de Memória | Memória de sessão (mensagens), Persistência com JSON/SQLite, 4 tipos de memória (usuário/feedback/projeto/referência), Compressão: sliding window, Compressão: resumo com LLM, Consolidação automática (AutoDream simplificado) |
| 5.4 | 🛡️ Segurança e Permissões | Por que segurança é obrigatória, Sandbox com subprocess, Sistema allow/deny/ask, Validação de comandos shell, Limites de recursos (timeout/memória), Auditoria e logging |

### Trilha 6 — Agente Local com Qwen + Ollama (Rose)
**Usando Claude Code como referência para criar um agente que roda com LLMs locais.**

| Módulo | Título | Tópicos (6 cada) |
|---|---|---|
| 6.1 | 🏠 Configurando o Ambiente Local | Instalando Ollama, Modelos Qwen disponíveis (Qwen3, Qwen3-Coder, Qwen3.5), Escolhendo por hardware (8GB/16GB/24GB/40GB+), Context window: o parâmetro mais importante, Python + biblioteca ollama, Primeiro chat com Qwen |
| 6.2 | 🔗 Tool Calling com LLMs Locais | Como funciona tool calling no Ollama, Formato dos schemas (OpenAI-compatible), O fluxo: request → tool_calls → execution → tool result, Thinking mode vs Non-thinking mode (Qwen3), Streaming com ferramentas, Limitações vs modelos de API |
| 6.3 | 🏗️ Montando o Agente Completo | O agent loop com Ollama (~30 linhas), Integrando as ferramentas da T5, Sistema de memória com persistência, Gerenciamento de contexto para janelas menores, Strip de `<think>` blocks do Qwen3, keep_alive e otimizações |
| 6.4 | 🚀 Do Local ao Produção | LiteLLM: usando Claude Code CLI com modelos locais, Multi-agente local (processos paralelos), Benchmarks: Qwen3-Coder-Next vs Claude (SWE-bench 69.6% vs 72-77%), Quando usar local vs API, Frameworks alternativos (smolagents, LangGraph, Qwen-Agent), O futuro: agentes híbridos |

## Arquivos a Criar

```
curso/
├── trilha4/                    # Amber
│   ├── index.html
│   ├── modulo-4-1.html
│   ├── modulo-4-2.html
│   ├── modulo-4-3.html
│   └── modulo-4-4.html
├── trilha5/                    # Teal
│   ├── index.html
│   ├── modulo-5-1.html
│   ├── modulo-5-2.html
│   ├── modulo-5-3.html
│   └── modulo-5-4.html
└── trilha6/                    # Rose
    ├── index.html
    ├── modulo-6-1.html
    ├── modulo-6-2.html
    ├── modulo-6-3.html
    └── modulo-6-4.html
```

**+ Atualizar:** `index.html` (landing page) para incluir as 6 trilhas

## Cores

| Trilha | Cor | Classes |
|---|---|---|
| T4 | Amber | text-amber-400, bg-amber-500/20, border-amber-500/30, from-amber-900/30 |
| T5 | Teal | text-teal-400, bg-teal-500/20, border-teal-500/30, from-teal-900/30 |
| T6 | Rose | text-rose-400, bg-rose-500/20, border-rose-500/30, from-rose-900/30 |

Light mode (mais escuro para contraste):
- Amber: #92400e (amber-800)
- Teal: #0d9488 (teal-600)
- Rose: #9f1239 (rose-800)

## Conteúdo-Chave por Trilha

### T4 — Foco: Conceitos fundamentais com analogias ao Claude Code
- Cada conceito é explicado primeiro em teoria, depois mostrado como o Claude Code implementa
- Diagramas existentes reutilizados (diagrama_conversa, diagrama_ferramentas, diagrama_memoria, diagrama_seguranca)
- Pseudocódigo e fluxogramas — ainda não é código real

### T5 — Foco: Código Python real, passo a passo
- Cada módulo constrói uma parte do agente com código completo
- Exemplos copiar-colar que funcionam
- Padrões extraídos do Claude Code adaptados para Python:
  - Tool Registry (inspirado no padrão universal de ferramentas)
  - MemoryManager (inspirado nos 4 tipos de memória)
  - PermissionController (inspirado nas 5 camadas de segurança)
  - ContextCompressor (inspirado no pipeline de 4 estágios)

### T6 — Foco: Integração prática com Ollama + Qwen
- Setup real com comandos para instalar e configurar
- Modelos recomendados por hardware:
  - 8GB VRAM: qwen3:8b ou qwen2.5-coder:7b
  - 16GB: qwen3:14b ou qwen3-coder:30b-a3b (MoE)
  - 24GB: qwen3:32b
  - 40GB+: qwen3-coder-next (Q4) — SWE-bench 69.6%
- Código do agente completo com ~120 linhas
- LiteLLM proxy para usar Claude Code CLI com modelos locais
- Benchmarks reais

## Imagens Reutilizáveis

| Imagem | Módulo(s) |
|---|---|
| diagrama_conversa_pt.png | 4.2 (o loop) |
| diagrama_ferramentas_pt.png | 4.3, 5.2 (ferramentas) |
| diagrama_memoria_pt.png | 4.4, 5.3 (memória) |
| diagrama_seguranca_pt.png | 5.4 (segurança) |
| diagrama_compactacao_pt.png | 5.3 (compressão) |
| diagrama_agentes_pt.png | 6.4 (multi-agente) |
| diagrama_query_loop_pt.png | 4.2, 6.3 (loop) |
| diagrama_subsistemas_pt.png | 5.1 (arquitetura) |

## Atualização da Landing Page

O hero da index.html precisa ser atualizado:
- Stats: 6 Trilhas, 24 Módulos, 144 Tópicos, ~12h
- Grid de trilhas: de 3 colunas para 2x3 ou 3x2
- Adicionar T4, T5, T6 com suas cores e descrições
- Nav: adicionar links para as 3 novas trilhas

## Execução

1. Criar diretórios trilha4/, trilha5/, trilha6/
2. Para cada trilha: criar index + 4 módulos (5 agentes em paralelo)
3. Commit + push por trilha
4. Atualizar index.html com as 6 trilhas
5. Push final

## Verificação

- Abrir cada página no browser
- Testar dark/light mode
- Verificar links entre trilhas
- Confirmar que todas as imagens carregam
- Verificar responsividade mobile
