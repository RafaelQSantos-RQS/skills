---
name: conventional-commits
description: Auxilia o agente a analisar diffs de código no git e redigir mensagens de commit padronizadas e objetivas seguindo a especificação Conventional Commits (v1.0.0). Use quando o usuário pedir para commitar, gerar mensagem de commit ou sugerir commits para alterações no git.
---

# Conventional Commits Helper

Esta skill instrui o agente a inspecionar alterações pendentes no repositório Git e elaborar mensagens de commit precisas, atômicas e padronizadas no formato **Conventional Commits 1.0.0**.

## Quando Usar

- Quando o usuário pedir: *"faça o commit das alterações"*, *"gere uma mensagem de commit"*, *"como commitar isso?"*, *"escreva um commit convencional"*.
- Ao preparar pull requests ou submeter alterações de código.

## Formato do Commit

```text
<tipo>[escopo opcional]: <descrição concisa no imperativo>

[corpo opcional explicando o motivo da mudança e contexto]

[rodapé opcional com referências a issues ou BREAKING CHANGE]
```

### Tipos Permitidos:
- **`feat`**: Introdução de nova funcionalidade ou recurso para o usuário.
- **`fix`**: Correção de bug ou comportamento inadequado.
- **`refactor`**: Refatoração de código que não altera comportamento nem corrige bug.
- **`perf`**: Melhoria de desempenho ou otimização de código.
- **`docs`**: Alterações em documentação (README, docstrings, manuais).
- **`test`**: Adição ou correção de testes automatizados.
- **`build`**: Mudanças no sistema de build ou dependências externas (ex: npm, pip, gradle).
- **`ci`**: Alterações em pipelines de integração contínua (ex: GitHub Actions, workflows).
- **`chore`**: Tarefas de manutenção rotineiras que não alteram código de produção.
- **`style`**: Ajustes de formatação, lint, ponto e vírgula sem alteração lógica.

### Breaking Changes:
- Indique com um ponto de exclamação antes dos dois pontos:
  `feat(api)!: alteração de contrato na rota /users`
  ou no rodapé com:
  `BREAKING CHANGE: payload agora exige o campo id`

## Diretrizes de Redação

1. **Inspecione o diff primeiro:** Sempre execute `git status` e `git diff --cached` (ou `git diff`) para entender exatamente o que mudou.
2. **Atomicidade:** Se houver mudanças não correlatas, sugira separar em commits distintos em vez de agrupar tudo em um único commit monolítico.
3. **Modo Imperativo:** Escreva a descrição no imperativo e em minúsculas (ex: `adiciona suporte a...` ou `add support for...`, sem ponto final no título).
4. **Responda em Português ou Inglês conforme a preferência do usuário ou histórico do repositório.**
