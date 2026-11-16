# 🧠 Skills Repository

Repositório pessoal de **Skills** para Agentes de Inteligência Artificial (compatível com **Antigravity**, **Claude Code**, **Cursor**, **Codex**, **GitHub Copilot**, etc.).

Este repositório reúne e centraliza instruções especializadas, fluxos de trabalho e padrões que podem ser instalados diretamente em qualquer projeto ou no ambiente global da sua máquina utilizando o comando oficial **`npx skills add`**.

---

## 🚀 Instalação Rápida

O utilitário oficial [`skills`](https://skills.sh) (desenvolvido pela Vercel Labs) aceita tanto o atalho do GitHub (`owner/repo`) quanto a URL completa.

### 1. Listar as skills disponíveis neste repositório
Antes de instalar, você pode visualizar todas as skills públicas disponíveis:
```bash
npx skills add RafaelQSantos-RQS/skills --list
```

### 2. Instalar uma skill específica
Para instalar apenas a skill desejada no projeto atual:
```bash
npx skills add RafaelQSantos-RQS/skills --skill conventional-commits
```

### 3. Instalar globalmente (para uso em qualquer projeto)
Se quiser que as skills fiquem disponíveis para o seu agente em todos os seus projetos sem precisar reinstalar:
```bash
npx skills add RafaelQSantos-RQS/skills --skill conventional-commits -g
```

### 4. Instalar todas as skills de uma vez
```bash
npx skills add RafaelQSantos-RQS/skills --all
# Ou globalmente:
npx skills add RafaelQSantos-RQS/skills --all -g
```

---

## 📦 Catálogo de Skills

| Skill | Descrição | Comando de Instalação |
| :--- | :--- | :--- |
| **`conventional-commits`** | Inspeciona diffs, sugere commits atômicos e valida mensagens com a configuração local do commitlint, usando Node, Docker ou fallback manual. | `npx skills add RafaelQSantos-RQS/skills --skill conventional-commits` |
| **`merge-request`** | Abrir, atualizar e responder review de Merge Requests (GitLab) ou Pull Requests (GitHub): título e corpo proporcionais ao diff, self-review e limpeza de ruído típico de texto gerado por IA. | `npx skills add RafaelQSantos-RQS/skills --skill merge-request` |
| **`skill-template`** | Boilerplate e guia de referência para criação de novas skills. | `npx skills add RafaelQSantos-RQS/skills --skill skill-template` |
| **`ux-laws`** | Base de conhecimento com 30 leis de UX (Fitts, Hick, Miller, Jakob, Gestalt, carga cognitiva, hierarquia visual) para revisar UI e tomar decisões de frontend. | `npx skills add RafaelQSantos-RQS/skills --skill ux-laws` |
| **`rust-best-practices`** | Padrões idiomáticos de Rust (borrow vs clone, clippy, thiserror/anyhow, type state, Send/Sync) derivados do handbook da Apollo GraphQL. | `npx skills add RafaelQSantos-RQS/skills --skill rust-best-practices` |
| **`angular-developer`** | Skill oficial do time Angular: geração de código e orientação em signals, forms, DI, routing, SSR, ARIA, animações, testes e CLI. | `npx skills add RafaelQSantos-RQS/skills --skill angular-developer` |
| **`angular-new-app`** | Skill oficial do time Angular para criar um app novo: detecção do CLI, flags do `ng new`, `--ai-config` e pinagem de versão. | `npx skills add RafaelQSantos-RQS/skills --skill angular-new-app` |
| **`optimus-ui`** | Documentação offline do Optimus UI (fork MIT do PrimeNG para Angular): API, props, eventos, templates, theming e migração dos 80+ componentes. | `npx skills add RafaelQSantos-RQS/skills --skill optimus-ui` |

---

## 🛠️ Como Adicionar Novas Skills a Este Repositório

O repositório foi arquitetado para permitir que você adicione quantas skills quiser sem quebrar a descoberta automática do `npx skills add`.

### Estrutura de Pastas
Cada skill reside em sua própria pasta dentro do diretório `skills/`:

```text
skills/
├── README.md
├── .gitignore
└── skills/
    ├── _template/              # Boilerplate para novas skills
    │   └── SKILL.md
    │
    ├── conventional-commits/   # Exemplo de skill
    │   ├── SKILL.md            # Obrigatório
    │   ├── scripts/            # (Opcional) scripts bash / python / node
    │   └── references/         # (Opcional) documentos de apoio / tabelas
    │
    └── sua-nova-skill/
        └── SKILL.md
```

> **Atenção:** Nunca coloque um arquivo `SKILL.md` diretamente na raiz do repositório. O CLI do `skills` entende que uma raiz com `SKILL.md` é uma skill única e isolada, ocultando as subpastas.

### Passo a Passo para Criar uma Skill

1. **Crie a pasta da sua skill:**
   ```bash
   mkdir -p skills/minha-skill
   ```
   *(Ou copie a pasta `skills/_template`)*

2. **Crie o arquivo `SKILL.md`:**
   Todo arquivo `SKILL.md` **precisa** começar com o cabeçalho YAML frontmatter contendo `name` e `description`:

   ```markdown
   ---
   name: minha-skill
   description: Descreva exatamente quando o agente deve carregar esta skill (ex: "Use quando o usuário pedir para analisar desempenho de banco de dados...")
   ---

   # Minha Skill

   ## Quando Usar
   - Descreva os cenários de ativação...

   ## Instruções
   1. Passo 1 para o agente...
   2. Passo 2 para o agente...
   ```

   > 💡 **Dica sobre a `description`:** O campo `description` é lido diretamente pelos agentes (Claude Code, Antigravity, Cursor, etc.) para decidir autonomamente quando acionar a skill. Seja claro e inclua palavras-chave de intenção.

3. **Valide a skill localmente antes de subir:**
   No diretório do repositório, rode:
   ```bash
   npx skills add . --list
   ```
   Se a sua nova skill aparecer na lista com a descrição correta, ela está pronta!

4. **Faça o commit e envie para o GitHub:**
   ```bash
   git add .
   git commit -m "feat(skills): adiciona skill minha-skill"
   git push origin main
   ```

---

## 🧰 Comandos Úteis do `npx skills`

- **Ver skills instaladas no projeto atual:**
  ```bash
  npx skills list
  ```
- **Ver skills instaladas globalmente no seu computador:**
  ```bash
  npx skills ls -g
  ```
- **Atualizar skills instaladas para a versão mais recente:**
  ```bash
  npx skills update
  # ou globalmente:
  npx skills update -g
  ```
- **Remover uma skill instalada:**
  ```bash
  npx skills remove minha-skill
  ```

---

## 📄 Licença
Distribuído sob licença livre para uso pessoal e colaborativo.
