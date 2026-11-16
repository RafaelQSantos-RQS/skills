# Comandos por host

Descubra o host com `git remote get-url origin` e use a seção correspondente. Os comandos assumem que você está no diretório do repositório, na branch da MR.

## GitLab (`glab`)

Self-hosted: exporte `GITLAB_HOST=gitlab.suaempresa.com` ou passe `--hostname` em cada comando, inclusive no `glab auth login`.

```bash
glab auth status

glab mr create --title "..." --description "..." --target-branch main --draft
glab mr create --title "..." --description "..." --target-branch main \
  --squash-before-merge --remove-source-branch --yes

glab mr view --web
glab mr update <id> --draft=false        # marcar pronta para review
glab mr note <id> -m "ajustei em abc1234"
glab ci status --branch "$(git branch --show-current)"
```

`--fill` reaproveita as mensagens de commit como corpo. Só use se os commits já estiverem bem escritos; caso contrário, escreva o corpo.

Sem `glab`, mas com servidor compatível, push options criam a MR no próprio push:

```bash
git push -o merge_request.create -o merge_request.target=main \
  -o merge_request.title="..." -o merge_request.description="..."
```

## GitHub (`gh`)

```bash
gh auth status

gh pr create --title "..." --body "..." --base main --draft
gh pr view --web
gh pr edit <id> --title "..." --body "..."
gh pr ready <id>
gh pr comment <id> --body "..."
gh pr checks <id>
```

`--fill` tem o mesmo problema do `glab mr create --fill`: promove mensagens de commit a corpo.

## Sem CLI

Se `glab` e `gh` não estão instalados e o push option não é suportado, não invente chamada de API nem URL de MR. Deixe o texto pronto e peça para o usuário colar:

```bash
printf '%s\n\n%s\n' "Título da MR" "Corpo da MR" > /tmp/mr.md
```

E diga com clareza: "não abri a MR; cole o conteúdo em `<host>/<projeto>/-/merge_requests/new`".

## Limites

- Nunca rode `glab mr merge` ou `gh pr merge` sem o usuário pedir.
- Nunca faça push sem o usuário saber: esta skill escreve a MR, não decide o envio.
- Nunca publique token, URL interna ou nome de cliente no corpo da MR sem o usuário confirmar.
