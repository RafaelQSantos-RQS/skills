---
name: merge-request
description: Orienta a abrir, atualizar e responder revisões de Merge Requests (GitLab) ou Pull Requests (GitHub e outros) com título e corpo enxutos e sem ruído. Use quando o usuário pedir para abrir MR/PR, criar pull request, escrever ou revisar a descrição de uma MR, revisar o próprio diff antes de submeter, responder comentários de review, ou transformar commits pendentes em uma MR pronta para revisão.
---

# Merge Request

Uma MR boa responde a três perguntas do revisor: **por que isso existe**, **o que muda**, **onde olhar**. Seções, listas, emoji e adjetivos são ruído quando empurram essas três para longe.

## Quando Usar

- Abrir, atualizar ou marcar como pronta uma MR/PR.
- Escrever ou revisar o título e o corpo de uma MR existente.
- Fazer o self-review do próprio diff antes de pedir revisão.
- Responder comentários de review depois de ajustar o código.

## 1. Ler o repositório antes de escrever

Convenção de MR é do repositório, não sua. Impor o seu formato gera atrito e o revisor pede para refazer.

```bash
git log --oneline -20
ls .gitlab/merge_request_templates/ .github/ 2>/dev/null
git remote get-url origin
```

| O que olhar | O que decidir |
|---|---|
| `git log` | idioma dos títulos, prefixo (`feat(api):`, `[PROJ-123]`, nada), se o commit é imperativo |
| `.gitlab/merge_request_templates/` ou `.github/pull_request_template.md` | existe template → ele manda. Preencha as seções dele; não acrescente outras |
| `CONTRIBUTING.md`, `docs/` | regra de aprovação, squash, branch base |
| `git remote get-url origin` | host real (self-hosted não é `gitlab.com`); comandos em `references/hosts.md` |
| `git branch -r` + `git log` | branch base: `main`, `master` ou `develop` |

Sem template, use a estrutura da seção 4. Com template, ele vence a estrutura — mas as regras de conteúdo (verificar de verdade, não inventar) valem sempre.

## 2. Self-review antes de abrir

Leia o diff inteiro, não só os arquivos de que você lembra:

```bash
git diff <base>...HEAD
```

Procure o que não deveria entrar: `console.log`/`print`/`dd()` de debug, código comentado, `TODO` recém-criado, arquivo de IDE ou de build, `.env`, lockfile alterado sem motivo. **Segredo ou token no diff: pare e avise o usuário antes de qualquer push.**

Dois assuntos no título ("corrige o cache e adiciona filtro") são duas MRs. Como sinal de tamanho, ~400 linhas alteradas ou ~10 arquivos costuma ser o ponto em que o revisor para de ler com atenção — não é lei, é aviso.

## 3. Título

- Imperativo, dizendo o que a MR faz: `Corrige expiração de sessão no refresh`, não `Correção de sessão`.
- Até 72 caracteres, sem ponto final, sem emoji.
- Sem prefixo convencional, comece com maiúscula. Título de MR é lido por humano; histórico de commits em minúsculas não obriga a MR a ser minúscula. Com prefixo, siga o que o repo faz depois dos dois-pontos (normalmente minúsculo).
- Prefixo convencional só se o histórico do repo usa.
- ID do ticket só se o repo ou o template pede.
- MR incompleta: use o draft do host, não "WIP" no título.

## 4. Corpo: proporcional ao diff

O tamanho do texto acompanha o tamanho da mudança. Descrição maior que o diff é sinal de enchimento.

- **Diff pequeno** (até ~50 linhas): uma a quatro linhas de prosa, sem heading.
- **Diff médio**: problema em um parágrafo, decisão em outro, e o que verificar.
- **Diff grande**: quatro blocos, nesta ordem — **Problema** (o comportamento errado ou a necessidade), **Abordagem** (a decisão e o tradeoff), **Onde olhar** (o trecho que merece atenção ou a ordem de leitura), **Como verifiquei** (o que rodou e o que não).

O porquê vem antes do quê: o revisor precisa do contexto para julgar o diff, não do diff recontado.

Vale escrever: decisão e alternativa descartada, o que ficou de fora de propósito, migração ou rollback, risco em produção, edge case que o código não cobre.
Não vale: lista de arquivos alterados, "melhoria de performance" sem número, screenshot que você não tirou, log de terminal colado inteiro.

Em "Como verifiquei", diga o que realmente rodou — teste novo cobrindo o bug, lint, build, verificação manual. Se não rodou, diga que não rodou. "Testado" sem teste é o comentário que mais destrói confiança.

## 5. Anti-slop

Vícios comuns de texto gerado por IA, com a correção:

| Vício | Antes | Depois |
|---|---|---|
| Emoji decorativo | `## ✨ Resumo`, `🚀 Adiciona cache` | `## Resumo`, `Adiciona cache de sessão` |
| Auto-narração | "Este MR introduz uma solução robusta que..." | "O login falhava quando o token expirava no meio do request." |
| Recontar o diff | lista dos 12 arquivos alterados | só a decisão e o tradeoff |
| Adjetivo inflado | robusto, completo, poderoso, elegante, seamless, production-ready | o fato ou número que justifica |
| Teatro de seções | Summary/Changes/Testing/Benefits num fix de 3 linhas | 3 linhas de prosa |
| Checklist inventado | `- [x] Li as diretrizes de contribuição` | o template do repo, ou nada |
| Heading por frase | um `##` a cada parágrafo | prosa corrida |
| Atribuição de IA | "Generated with ...", co-autor de modelo | nada, salvo política explícita do repo |
| Hedge | "talvez valha considerar potencialmente" | afirma, ou corta a frase |
| Promessa vazia | "totalmente testado e production-ready" | "testei o caminho de erro; o feliz já era coberto" |
| Travessão decorativo | vírgula — em — toda frase | vírgula, dois-pontos, parêntese |
| Simetria artificial | "mais rápido, mais seguro e mais simples" | o benefício que dá para medir |

Três testes antes de publicar:

1. Tire o adjetivo. Se a frase continua verdadeira, o adjetivo era ruído.
2. Tire o heading. Se a linha abaixo já dizia aquilo, o heading era ruído.
3. Compare o corpo com o diff. Se o corpo ganha, corte pela metade.

## 6. Responder review

- Leia todas as threads antes de responder a primeira: comentários se repetem e a resposta pode ser uma só.
- Diga o que mudou e onde: "ajustei em `abc1234` — o cache agora é invalidado antes do redirect". "Feito" sozinho não permite conferir.
- Discordar é legítimo: explique com o código ou o requisito e proponha alternativa. Não aceite mudança só para encerrar a thread.
- Marque resolvido só depois do push que contém a correção.
- Não reescreva a descrição inteira a cada ajuste. Se o escopo mudou, acrescente uma linha em "Atualizações"; caso contrário, edite o trecho afetado.
- Avise o revisor quando a pipeline ficar verde — e quando o vermelho não for culpa da MR.

## 7. Antes de pedir revisão

- Base branch errada é o erro mais comum. Confira antes de abrir.
- Não misture reformatação com mudança de comportamento: separe em commit ou MR própria. Mandar o revisor usar `git diff -w` esconde o ruído em vez de resolvê-lo.
- Force-push em branch com review aberto apaga o contexto dos comentários. Só faça se o revisor estiver avisado.
- Abrir cedo como draft é melhor que abrir pronto e grande no fim.

## Referências

- `references/hosts.md`: criar, atualizar e comentar MR no GitLab (`glab`), no GitHub (`gh`) e sem CLI instalado.
