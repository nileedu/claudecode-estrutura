# Análise do Vazamento do Claude Code

**Descrição:** Uma análise sobre o vazamento de código do Claude Code via source maps, o que foi exposto e o possível impacto para o ecossistema de agentes de IA.

**Nota do autor:** Uma análise detalhada sobre o incidente de 31 de março de 2026, quando o Claude Code vazou acidentalmente 512 mil linhas de código-fonte via npm source maps, incluindo referências ao modelo Capybara, ao "Undercover Mode" e ao impacto potencial para startups de agentes de IA.

Em 31 de março de 2026, uma falha na configuração de build causou um grande vazamento de código-fonte do Claude Code da Anthropic via arquivos de source map do npm, expondo 1.900 arquivos na íntegra. O pesquisador de segurança Chaofan Shou foi o primeiro a descobrir e tornar público o fato; em poucas horas, a comunidade criou vários espelhos no GitHub. Ironicamente, o código continha um subsistema chamado "Undercover Mode" — projetado especificamente para evitar vazamentos de informações internas — mas o sistema inteiro acabou sendo exposto.

Este artigo analisa o conteúdo crítico desse vazamento, o impacto para startups de agentes de IA e por que esse "open source acidental" pode impulsionar o desenvolvimento do setor.

**Valor central:** Entender o design da arquitetura interna, as funcionalidades ocultas e as práticas de engenharia do Claude Code, avaliando o impacto desse vazamento para a indústria de agentes de IA.

## Fatos principais do incidente

| Item | Detalhes |
|---|---|
| Data do vazamento | 31 de março de 2026 |
| Descobridor | Pesquisador de segurança Chaofan Shou |
| Método de vazamento | Pacote npm v2.1.88 contendo 57 MB de arquivos `.map` |
| Escala do vazamento | 1.906 arquivos, 512.000+ linhas de código TypeScript |
| Causa do vazamento | `.npmignore` não excluiu arquivos `.map` + Bun gerando source maps por padrão |
| É a primeira vez? | Não — um incidente semelhante ocorreu em fevereiro de 2025 |
| Reação da Anthropic | Lançou imediatamente uma nova versão removendo os arquivos `.map` e deletou a versão antiga do npm |
| Reação da comunidade | 3+ repositórios espelho no GitHub, 1.100+ estrelas |

## O que foi vazado: 3 descobertas principais

### 1. A misteriosa família de modelos Capybara

O código revelou um codinome de modelo nunca antes divulgado — **Capybara**, dividido em três níveis:

| Codinome do modelo | Posicionamento especulado |
|---|---|
| `capybara` | Versão padrão (possivelmente o próximo Claude) |
| `capybara-fast` | Versão rápida |
| `capybara-fast[1m]` | Versão rápida com janela de contexto de 1M |

A comunidade especula que Capybara possa ser o codinome interno da série Claude 5, mas a Anthropic não se pronunciou.

### 2. Undercover Mode (Modo Disfarçado)

Esta é a descoberta mais controversa. O código contém um subsistema completo de **"Undercover Mode"**, cujo comando de sistema declara explicitamente que o assistente deve operar sem revelar informações internas da Anthropic.

Em outras palavras, a ferramenta aparenta incluir um modo voltado a contribuições anônimas em projetos de código aberto, sem expor a origem interna da empresa.

Isso gerou debate na comunidade open source: empresas de IA enviarem anonimamente código gerado por IA para projetos abertos pode ser interpretado como uma forma de ocultação indevida?

### 3. `/buddy`, o pet virtual estilo Tamagotchi

O código esconde um sistema de pet virtual funcional — o comando `/buddy` pode invocar um pet de IA, com espécies, raridade, atributos, acessórios e efeitos de animação. Isso sugere uma cultura interna de engenharia que mistura experimentação e humor mesmo em uma ferramenta séria de codificação.

## A arquitetura de engenharia vazada

Deixando o lado mais curioso de lado, a parte mais valiosa do vazamento é a arquitetura do Claude Code — uma das raras exposições amplas de um agente de IA em nível de produção.

### Destaques da arquitetura central

| Componente de Arquitetura | Detalhes da implementação vazada | Valor para a indústria |
|---|---|---|
| Sistema de execução de ferramentas | Implementação completa de Bash / IO de arquivos / Computer Use | Como um agente executa comandos do sistema com segurança |
| Permissões e fluxo de aprovação | Mecanismos de bypass multinível e aprovação | Design de fronteiras de segurança para agentes de produção |
| Telemetria e monitoramento | Pipeline completo de coleta e análise de dados | Como monitorar comportamento e desempenho do agente |
| Compressão de contexto | Lógica de Context Compaction | Estratégias de gerenciamento de contexto para diálogos longos |
| Comando do sistema | Comandos relacionados à segurança | Como restringir o comportamento do agente |
| Comunicação IPC | Protocolo de comunicação entre processos | Coordenação de múltiplos agentes |
| Feature Flags | Lista completa de 44 chaves de funcionalidade | Indícios do roteiro de produto |
| Mecanismo de Sandbox | Implementação de isolamento para execução de código | Melhores práticas para execução segura |

## Por que esse "open source acidental" pode impulsionar o setor

### O que é possível aprender com as práticas vazadas

Antes desse vazamento, não havia uma referência pública robusta sobre como um agente de IA de nível de produção deveria ser construído. O Claude Code, muito bem posicionado em rankings técnicos, oferece aqui uma visão rara de práticas de engenharia em larga escala.

| Prática de Engenharia | Abordagem do Claude Code | Inspiração para a indústria |
|---|---|---|
| Execução segura de ferramentas | Sandbox multinível + aprovação de permissão + lista de permissões de comandos | A execução de comandos deve ter fronteiras de segurança |
| Gerenciamento de contexto | Compressão automática via Context Compaction | Sessões longas exigem estratégias proativas |
| Feature Flag | 44 chaves de funcionalidade, lançamento gradual | Produtos em escala precisam de controle refinado |
| Design de telemetria | Pipeline de coleta e análise de comportamento | Observabilidade é crucial |
| Coordenação de múltiplos agentes | Comunicação IPC + mensagens estruturadas | Padrões de comunicação multiagente |
| Engenharia de comando do sistema | Comandos em camadas + restrições de função | Padrões de design para produção |

## Impacto específico nas startups de AI Agent

### 1. Redução da barreira técnica

Antes, criar um agente de IA de nível de produção exigia resolver do zero questões como fronteiras de segurança, permissões e gerenciamento de contexto. Com uma implementação de referência tão completa exposta, equipes menores podem estudar padrões arquiteturais já validados.

### 2. Mudança no foco da concorrência

Se a arquitetura deixa de ser um segredo, a diferenciação entre agentes tende a migrar de **"como construir"** para **"qual modelo usar"** e **"quão boa é a experiência do usuário"**.

### 3. Aceleração do ecossistema open source

O código vazado já passou a ser usado pela comunidade em várias frentes:

- O projeto **claw-code** está reescrevendo a lógica central do Claude Code em Rust.
- Repositórios no GitHub estão criando análises de arquitetura e documentação de aprendizado.
- Pesquisadores de segurança estão examinando bypasses de permissão e vulnerabilidades potenciais.

### 4. Estabelecimento de padrões de segurança

O sistema de permissões, o mecanismo de sandbox e o design de comandos de segurança do Claude Code podem influenciar padrões práticos de segurança para agentes de IA, justamente por representarem uma implementação ampla e concreta.

## Lições para desenvolvedores

### Lições sobre segurança de configuração

A causa técnica do vazamento foi simples: o arquivo `.npmignore` não excluiu os arquivos `.map`. Isso serve como alerta para qualquer equipe que publique pacotes npm.

```txt
# Deve ser incluído no .npmignore
*.map
*.js.map
*.d.ts.map
```

Uma opção ainda mais segura é declarar explicitamente apenas os arquivos necessários no campo `files` do `package.json`, em vez de depender apenas de exclusões.

### Se você é um empreendedor de AI Agent

| O que fazer | Motivo |
|---|---|
| Estudar o sistema de permissões do Claude Code | É uma referência madura de segurança para agentes |
| Aprender sobre Context Compaction | Solução de produção para gerenciamento de contexto |
| Referenciar o design de Feature Flags | Exemplo de lançamento gradual com 44 chaves |
| Não copiar código diretamente | O código vazado possui direitos autorais; o aprendizado deve focar em padrões |
| Acompanhar o modelo Capybara | Pode indicar a direção da próxima geração do Claude |

### Se você é um usuário do Claude Code

Este vazamento não altera necessariamente a experiência principal de uso, já que as capacidades centrais dependem do backend e da infraestrutura da Anthropic. Ainda assim, vale acompanhar:

- Atualizações para a versão mais recente.
- Possíveis anúncios sobre o modelo Capybara.
- Novas funcionalidades sugeridas pelas 44 feature flags expostas.

## Perguntas frequentes

### Q1: Este vazamento afeta a segurança do Claude Code?

O vazamento do código do cliente não significa, por si só, que o servidor tenha sido invadido. A parte mais sensível da operação — como inferência de modelo, autenticação de API e criptografia de transmissão — permanece do lado do servidor. Ainda assim, a exposição da lógica local de permissões e dos comandos de segurança pode aumentar a superfície de análise para pesquisadores e atacantes.

### Q2: Capybara é o Claude 5?

A comunidade especula que sim, mas a Anthropic não confirmou. Os codinomes `capybara`, `capybara-fast` e `capybara-fast[1m]` sugerem uma família estruturada de modelos, mas qualquer conclusão definitiva depende de anúncio oficial.

## Resumo

Pontos principais sobre o vazamento do código-fonte do Claude Code:

- Em **31/03/2026**, 512 mil linhas de código TypeScript foram expostas acidentalmente via source maps do npm.
- A causa foi a falha em excluir arquivos `.map` no `.npmignore`.
- Entre as descobertas, destacam-se a família de modelos **Capybara**, o **Undercover Mode** e o sistema de mascote virtual **`/buddy`**.
- O impacto é potencialmente negativo para a Anthropic no curto prazo, mas pode beneficiar o setor no longo prazo ao expor práticas reais de engenharia de agentes de IA.

## Referências

- **VentureBeat** — relatório sobre o vazamento do código-fonte do Claude Code e a resposta da Anthropic.
- **Repositório espelho no GitHub** — backup comunitário e análises do código vazado.
- **DEV Community** — interpretações técnicas e discussões sobre o conteúdo exposto.
