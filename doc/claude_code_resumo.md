# Dentro do Claude Code – Arquitetura (Resumo Traduzido)

## O que é o Claude Code
O Claude Code é um CLI da Anthropic que funciona como um verdadeiro sistema operacional para desenvolvimento com IA. Possui mais de 1.900 arquivos e 500 mil linhas de código.

### Principais componentes:
- Query Engine (motor de conversa)
- Tools (40+ ferramentas)
- Agents (subagentes paralelos)
- Bridge (conexão com browser/IDE)
- Memory (memória persistente)
- Security (camadas de proteção)
- Context Manager (compressão de contexto)
- Skills & Plugins (extensibilidade)

---

## Como funciona uma conversa
Fluxo básico:
1. Você digita
2. Sistema injeta contexto + skills
3. Chamada para API
4. Execução de tools
5. Retorno dos resultados
6. Resposta final

Esse processo roda em loop até terminar.

---

## Ferramentas (Tools)
Cada ferramenta segue um padrão:
- call(): executa ação
- validação de entrada
- permissões (allow/deny/ask)
- execução paralela segura
- controle de interrupção

---

## Agentes (Sub-agents)
3 modos:
- Standard: independente, sem contexto
- Fork: herda contexto e compartilha cache
- Teammate: processos separados coordenados

---

## Segurança
5 camadas:
- Sandbox
- Sistema de permissões
- Proteções de comandos
- Análise de comandos
- Proteção do código

---

## Compressão de contexto
4 etapas:
- Microcompact: remove outputs antigos
- History Snip: corta histórico antigo
- Autocompact: resume automaticamente
- Session Memory: preserva info importante

---

## Memória
4 tipos:
- Usuário (preferências)
- Feedback (erros/acertos)
- Projeto (contexto ativo)
- Referência (links externos)

Sistema AutoDream consolida memórias automaticamente.

---

## Multi-agentes (Army Mode)
- Um líder coordena vários agentes
- Cada um executa tarefas específicas
- Comunicação via mensagens internas

---

## UltraPlan
Permite enviar tarefas para a nuvem:
- Cria plano remoto
- Usuário aprova
- Execução volta localmente

---

## Bridge
Conecta terminal com browser/IDE:
- Comunicação bidirecional
- WebSocket + HTTP
- Sessões simultâneas

---

## Recursos ocultos (Background)
- Sugestão de prompts
- Extração de memória
- MagicDocs (docs auto-atualizadas)
- Resumo de agentes
- Memória de sessão

---

## Buddy System
Sistema gamificado com “pets”:
- 18 espécies
- 5 raridades
- Stats tipo RPG
- Gerado a partir do usuário

---

## Insight principal
O Claude Code é muito mais que um CLI: é uma plataforma completa de orquestração de IA com agentes, memória, segurança e execução distribuída.
