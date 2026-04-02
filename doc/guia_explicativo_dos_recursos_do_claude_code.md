# Guia Explicativo dos Recursos do Claude Code

## 1. Visão Geral

O Claude Code não é apenas um chatbot executado no terminal. Ele é descrito como um sistema completo de agentes (agent runtime), com múltiplos componentes integrados que permitem automatizar tarefas, gerenciar contexto, executar ações e interagir com diferentes ferramentas.

Seu valor principal não está apenas em escrever bons prompts, mas em saber configurar e utilizar seu ecossistema: comandos, memória, permissões e integrações.

---

## 2. Comandos Principais

Os comandos são atalhos que estruturam o uso do sistema e aumentam muito a eficiência.

### Principais comandos:

- **/init**  
  Inicializa o projeto e gera contexto inicial (como um arquivo base de operação).

- **/plan**  
  Coloca o sistema em modo de planejamento antes de executar ações.

- **/compact**  
  Resume o histórico da conversa para economizar tokens e reduzir custo.

- **/review** e **/security review**  
  Executam revisões estruturadas de código.

- **/context**  
  Controla quais arquivos estão no contexto ativo.

- **/cost**  
  Mostra o custo acumulado da sessão.

- **/summary**  
  Resume o estado atual do trabalho.

- **/resume**  
  Retoma uma sessão anterior sem precisar explicar tudo novamente.

👉 Ideia central: quem domina comandos trabalha muito mais rápido do que quem usa só prompts.

---

## 3. Sistema de Memória

O Claude Code possui um sistema de memória persistente.

### Arquivo principal:

- **CLAUDE.md**

Esse arquivo funciona como um manual operacional do projeto.

### O que deve conter:

- Regras do projeto
- Padrões de código
- Decisões técnicas
- Restrições importantes

### O que NÃO deve conter:

- Textos longos
- Documentação histórica
- Explicações genéricas

👉 Ideia: ele atua como onboarding automático para o sistema.

---

## 4. Sistema de Permissões

O sistema possui controle detalhado sobre ações como:

- editar arquivos
- rodar comandos
- acessar recursos

### Problema comum:

O sistema pede confirmação o tempo todo.

### Solução:

Configurar permissões automáticas (wildcards), por exemplo:

- permitir todos comandos git
- permitir edições em determinada pasta

### Arquivos de configuração:

- settings.json
- settings.local.json

👉 Resultado: menos interrupção e mais automação.

---

## 5. Arquitetura Multiagente

O sistema foi projetado para dividir tarefas em partes menores.

### Em vez de:

Um único prompt grande e complexo

### Melhor abordagem:

- etapa 1: análise
- etapa 2: planejamento
- etapa 3: execução
- etapa 4: verificação

Também existem sinais de:

- execução paralela
- tarefas em background
- coordenação entre agentes

👉 Ideia: decompor tarefas aumenta qualidade e eficiência.

---

## 6. Extensibilidade (MCP, Plugins e Skills)

O sistema pode ser expandido através de integrações.

### MCP (Model Context Protocol)

Permite conectar o Claude Code a:

- APIs
- bancos de dados
- ferramentas externas

### Plugins e Skills

Permitem criar:

- automações repetíveis
- fluxos personalizados
- capacidades específicas por domínio

👉 Ideia: o poder vem do que você conecta ao sistema.

---

## 7. Recursos Avançados e Internos

O código indica a existência de funcionalidades ainda não totalmente públicas.

### Exemplos mencionados:

- Voice Mode
- Daemon Mode
- Coordinator Mode
- Sistema chamado Kairos (ou similar)

Também existem:

- feature flags (recursos ativados por usuário)
- diferentes experiências dependendo da configuração

👉 Ideia: o sistema está em evolução contínua.

---

## 8. Configuração Avançada

O sistema possui diversas opções de configuração:

- roteamento de modelos
- escolha de backend (AWS Bedrock, Google Vertex)
- comportamento do shell
- controles de privacidade
- modelos diferentes para subagentes

👉 Ideia: pode ser ajustado como infraestrutura, não só como ferramenta.

---

## 9. Boas Práticas (Resumo)

Usuários avançados seguem alguns princípios:

1. Manter o CLAUDE.md curto e objetivo
2. Usar comandos em vez de depender só de prompts
3. Configurar permissões para evitar interrupções
4. Dividir tarefas complexas em etapas
5. Gerenciar contexto para reduzir custo
6. Usar /compact regularmente
7. Conectar ferramentas externas

---

## 10. Conclusão

O Claude Code deve ser tratado como um sistema operacional de automação com IA, e não apenas como um chatbot.

O ganho real vem da combinação de:

- estrutura (comandos)
- memória (CLAUDE.md)
- automação (permissões)
- organização (decomposição de tarefas)
- integração (MCP, plugins, skills)

Quem entende esses elementos consegue extrair muito mais valor da ferramenta.

