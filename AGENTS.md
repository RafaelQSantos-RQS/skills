# AGENTS.md — Guia Operacional para Agentes de IA

Este documento define as diretrizes, padrões de arquitetura e fluxos operacionais que qualquer agente de inteligência artificial (Antigravity, Claude Code, Cursor, Codex, GitHub Copilot, etc.) **deve seguir obrigatoriamente** ao interagir com este repositório.

---

## 1. Visão Geral do Repositório

- **Propósito:** Catálogo pessoal e centralizado de **Skills** de IA do desenvolvedor Rafael Queiroz Santos (`RafaelQSantos-RQS/skills`).
- **Ecossistema:** Distribuído primariamente através do gerenciador de pacotes [`skills.sh`](https://skills.sh) via comando:
  ```bash
  npx skills add RafaelQSantos-RQS/skills
  ```
- **Compatibilidade:** As skills são universais e consumidas por múltiplos agentes. Todo conteúdo deve ser agnóstico de ambiente (sem caminhos locais absolutos do sistema operacional do autor).

---

## 2. Invariantes e Regras Rígidas (Anti-Padrões a Evitar)

Qualquer agente trabalhando neste repositório deve respeitar as seguintes regras:

1. ❌ **NUNCA crie um arquivo `SKILL.md` na raiz do repositório:**
   - O CLI `npx skills` interpreta um `SKILL.md` na raiz como indicador de que o repositório inteiro é uma única skill isolada, ocultando todas as subpastas.
2. 📁 **Localização Padrão das Skills:**
   - Todas as skills devem residir exclusivamente dentro do diretório `skills/`:
     ```text
     skills/<nome-da-skill>/SKILL.md
     ```
3. 🏷️ **Nomenclatura Obrigatória:**
   - Pastas de skills devem usar estritamente `kebab-case` (ex: `conventional-commits`, `docker-compose-validator`, `sql-optimizer`).
   - O arquivo principal deve se chamar exatamente `SKILL.md` (em letras maiúsculas).
4. 📝 **Frontmatter YAML Obrigatório:**
   - Todo `SKILL.md` deve iniciar com cabeçalho YAML contendo `name` e `description`:
     ```markdown
     ---
     name: nome-da-skill
     description: Explicação clara de quando e por que ativar esta skill.
     ---
     ```
5. 🎯 **Qualidade da `description` (Gatilhos de Ativação):**
   - Os agentes decidem se carregam ou não uma skill avaliando a `description`. Portanto, ela **deve** incluir palavras-chave e frases de gatilho explícitas (ex: *"Use quando o usuário pedir para commitar..."*, *"Use ao refatorar componentes..."*).
6. 🔄 **Sincronização Obrigatória do `README.md`:**
   - Sempre que uma skill for adicionada, renomeada ou removida, a tabela do catálogo no [`README.md`](./README.md) **deve ser atualizada imediatamente**.
7. 🧪 **Verificação Prévia Obrigatória:**
   - Antes de considerar qualquer tarefa concluída, o agente deve rodar `npx skills add . --list` para garantir que o CLI consegue descobrir e analisar as skills sem erros.

---

## 3. Fluxos Operacionais para Agentes

### Fluxo A: Criar uma Nova Skill do Zero

Quando o usuário solicitar a criação de uma nova skill:

1. **Definir o nome e escopo:** Escolha um identificador em `kebab-case`.
2. **Criar a estrutura da pasta:**
   ```bash
   mkdir -p skills/<nome-da-skill>
   ```
   *(Pode-se duplicar o conteúdo de `skills/_template/` como ponto de partida).*
3. **Redigir o `SKILL.md`:**
   - Inclua o frontmatter YAML com `name` e `description`.
   - Estruture em seções: `# Título`, `## Quando Usar`, `## Instruções`, `## Exemplos/Saída Esperada`.
4. **Adicionar recursos auxiliares (se aplicável):**
   - Scripts determinísticos vão em `skills/<nome-da-skill>/scripts/` (bash ou node `.mjs`).
   - Documentações extensas, tabelas ou cheatsheets vão em `skills/<nome-da-skill>/references/`.
5. **Atualizar o catálogo no `README.md`:**
   - Adicione uma nova linha na tabela de skills com o nome, descrição concisa e o comando de instalação.
6. **Validar:**
   ```bash
   npx skills add . --list
   ```

---

### Fluxo B: Importar / Adicionar uma Skill Externa

Quando o usuário fornecer um link de GitHub, Notion ou texto de uma skill encontrada na internet:

1. **Auditoria de Segurança:**
   - Verifique se a skill não contém comandos perigosos (ex: exclusão não supervisionada, comandos `rm -rf`, execução de binários desconhecidos ou vazamento de variáveis de ambiente).
2. **Higienização e Adaptação:**
   - Converta o nome para `kebab-case`.
   - Garanta que não existam caminhos absolutos hardcoded (ex: `/home/usuario/...` ou `C:\Users\...`).
   - Se a skill pertencia a um repositório monotemático com `SKILL.md` na raiz, adapte-a para a estrutura `skills/<nome-da-skill>/SKILL.md`.
3. **Metadados e Créditos:**
   - Preserve os créditos de autoria original no frontmatter utilizando o campo `metadata`:
     ```yaml
     ---
     name: nome-da-skill
     description: ...
     metadata:
       author: autor-original
       source: https://github.com/...
     ---
     ```
4. **Registrar no `README.md` e testar com `npx skills add . --list`.**

---

### Fluxo C: Atualizar uma Skill Existente

Ao refinar instruções, corrigir regras ou atualizar dependências de uma skill:

1. **Preservar Retrocompatibilidade:**
   - Evite alterar o campo `name` no frontmatter a menos que explicitamente solicitado pelo usuário, para não quebrar instalações existentes.
2. **Refinar a `description` se novas capacidades forem adicionadas:**
   - Garanta que novas palavras-chave ou casos de uso fiquem refletidos na descrição.
3. **Se houver scripts associados:**
   - Teste a execução do script com parâmetros padrão e casos de borda.
4. **Atualizar a descrição no `README.md` se o propósito tiver mudado.**
5. **Validar com `npx skills add . --list`.**

---

### Fluxo D: Remover ou Descontinuar uma Skill

1. Remova a pasta correspondente: `rm -rf skills/<nome-da-skill>`.
2. Remova a linha correspondente na tabela do [`README.md`](./README.md).
3. Execute `npx skills add . --list` para confirmar que a skill não aparece mais.

---

## 4. Eficiência de Contexto e Boas Práticas

Agentes de IA consomem tokens ao ler arquivos. Para maximizar a eficiência e a clareza:

- **Divisão Progressiva de Informação (Progressive Disclosure):**
  - O arquivo `SKILL.md` principal deve ser direto e focado no fluxo operacional (idealmente menos de 400 linhas).
  - Use a pasta `references/` para armazenar manuais detalhados, especificações OpenAPI ou tabelas extensas, instruindo o agente no `SKILL.md` a ler o arquivo de referência somente quando necessário.
- **Scripts Determinísticos:**
  - Prefira criar scripts em `scripts/` para automações lógicas (ex: scripts bash com `set -e` ou Node.js em `.mjs`) em vez de pedir para o agente adivinhar transformações complexas de arquivos ou dados.
  - Scripts devem enviar logs/status para `stderr` e dados úteis para `stdout`.

---

## 5. Protocolo de Verificação e Git

1. **Validação Local Obrigatória:**
   ```bash
   npx skills add . --list
   ```
2. **Padrão de Mensagens de Commit (Conventional Commits):**
   - `feat(skills): adiciona skill <nome>`
   - `fix(skills): corrige regras da skill <nome>`
   - `docs(skills): atualiza documentação da skill <nome> ou README`
   - `chore(skills): remove skill descontinuada <nome>`
