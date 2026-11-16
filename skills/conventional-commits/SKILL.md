---
name: conventional-commits
description: Ajuda a inspecionar mudanças no Git, separar commits atômicos, escrever mensagens e validá-las contra a convenção do repositório. Use quando o usuário pedir para commitar, gerar ou revisar uma mensagem de commit, sugerir commits para alterações, configurar ou executar commitlint, ou preparar commits para uma MR/PR.
---

# Conventional Commits

Inspecione o repositório antes de escolher a mensagem. A especificação Conventional Commits é um padrão útil, mas a configuração e as convenções locais têm prioridade.

## 1. Descobrir o contrato do repositório

Antes de redigir ou validar:

```bash
git status --short
git diff --cached
git diff
git log --oneline -20
```

Procure, sem alterar nada:

- `commitlint.config.js`, `.mjs`, `.cjs`, `.ts` ou `.json`;
- `package.json` e os lockfiles do gerenciador usado;
- `.commitlintrc`, `.commitlintrc.json`, `.commitlintrc.yml`, `.commitlintrc.yaml` ou `.commitlintrc.js`;
- `CONTRIBUTING.md`, `README.md`, hooks de commit e documentação de release.

Se houver configuração do commitlint, ela é a autoridade. Por exemplo:

```js
export default { extends: ['@commitlint/config-conventional'] };
```

Isso normalmente exige tipo em minúsculas, tipo permitido, assunto não vazio, sem ponto final e limite de 100 caracteres no cabeçalho — mas **não adivinhe regras a partir do exemplo**: leia a configuração e valide com o commitlint.

Se não houver configuração, use o histórico para descobrir idioma, prefixos, escopo, limite aproximado e formato do time. Não invente um escopo só porque ele parece organizado.

## 2. Escolher o tipo e dividir o trabalho

Use o tipo que descreve a intenção observável da mudança:

| Tipo | Quando usar |
|---|---|
| `feat` | recurso novo para o usuário |
| `fix` | correção de comportamento incorreto |
| `refactor` | reorganização sem mudança de comportamento |
| `perf` | melhoria de desempenho |
| `docs` | documentação |
| `test` | teste sem mudança de produção |
| `build` | dependências ou sistema de build |
| `ci` | pipeline e automação de CI |
| `chore` | manutenção que não se encaixa melhor em outro tipo |
| `style` | formatação sem alteração de lógica |
| `revert` | reversão de um commit anterior, se permitido pela configuração |

Se o diff contém assuntos não relacionados, proponha commits separados antes de escrever uma mensagem única. Não use `chore` para esconder uma feature ou um bug.

## 3. Escrever a mensagem

Formato:

```text
<tipo>[escopo opcional]: <descrição curta>

[corpo opcional: motivo, decisão ou impacto]

[rodapé opcional: issue ou BREAKING CHANGE]
```

- Escreva a descrição no imperativo e sem ponto final, respeitando o idioma do repositório.
- Siga a capitalização exigida pelo commitlint local. No `config-conventional` padrão, o assunto deve ser minúsculo: `fix(auth): impede refresh expirado`.
- Use escopo apenas quando o histórico ou a configuração o justificar.
- Explique no corpo o motivo, tradeoff, impacto ou migração; não reescreva a lista de arquivos.
- Marque mudança incompatível com `!` (`feat(api)!:`) ou com `BREAKING CHANGE:` no rodapé, conforme a convenção local.
- Não coloque emoji decorativo, auto-narração, adjetivo inflado, promessa de teste não executado ou atribuição a uma IA.

## 4. Validar a mensagem

Valide a mensagem final, não um exemplo diferente. Substitua `MSG` por um arquivo temporário que contenha exatamente a mensagem candidata e remova o arquivo ao terminar.

### Prioridade das configurações

1. Se o repositório tiver configuração do commitlint, use-a.
2. Se não tiver configuração, use `@commitlint/config-conventional` como padrão explícito.
3. Se a configuração local estender regras próprias, **não** passe `--extends @commitlint/config-conventional` junto: isso pode validar contra regras diferentes das do projeto.

### Caminho A: Node disponível

Escolha o primeiro caminho disponível nesta ordem, verificando antes com `command -v node`, `command -v npx` e `command -v docker`. Ter Node instalado não significa que o projeto tenha `commitlint` instalado; por isso há um fallback para `npx`.

Prefira uma instalação local já existente:

```bash
./node_modules/.bin/commitlint --edit MSG
```

Se não houver binário local, use `npx`. Com configuração local, o CLI deve descobri-la no diretório do projeto:

```bash
npx --yes commitlint --edit MSG
```

Sem configuração local, peça explicitamente o preset convencional:

```bash
npx --yes -p @commitlint/cli -p @commitlint/config-conventional commitlint --extends @commitlint/config-conventional --edit MSG
```

Se o projeto já declara `@commitlint/cli` e o preset no `package.json`, prefira a versão do projeto e não baixe outra versão sem necessidade.

### Caminho B: Node indisponível, Docker disponível

Monte somente o diretório do repositório e use a imagem oficial:

```bash
docker run --rm -i -v "$PWD:/work:ro" -w /work commitlint/commitlint --edit MSG
```

Esse caminho respeita a configuração encontrada no diretório montado. Sem configuração local, a imagem oficial usa a configuração convencional padrão. Se o repositório exigir plugins ou presets que não estejam na imagem, informe que a validação não foi reproduzida; não instale dependências no projeto automaticamente.

### Caminho C: nenhum Node nem Docker

Faça uma checagem manual limitada contra o contrato descoberto: cabeçalho, tipo, escopo, assunto, pontuação, comprimento e breaking change. Diga explicitamente que foi uma **validação manual**, não uma execução de commitlint. Não declare que a mensagem passou no commitlint.

Se nenhuma ferramenta estiver disponível e a mensagem falhar numa regra que não dá para confirmar, peça confirmação ao usuário ou mostre a mensagem como candidata, sem criar o commit automaticamente.

### Resultado da validação

- Exit code zero: informe que o comando executado passou e cite o comando usado.
- Exit code diferente de zero: mostre as regras que falharam e proponha uma correção; não mascare o erro.
- Comando ausente, dependência não resolvida, imagem indisponível ou configuração incompatível: informe a limitação e classifique o resultado como não validado.

## 5. Criar o commit

Só crie o commit quando o usuário pedir ou autorizar claramente. Antes:

1. confirme `git status` e o diff staged;
2. verifique que a mensagem corresponde ao diff e não inclui arquivo acidental;
3. rode a validação disponível;
4. se houver falha, corrija a mensagem ou pergunte antes de prosseguir.

Use arquivo para preservar corpo e rodapés:

```bash
git commit -F MSG
```

Não faça `git add -A`, push, amend ou rebase como efeito colateral. Se houver mudanças não staged, deixe claro quais ficaram fora.
