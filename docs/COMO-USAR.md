# Como usar

O ciclo de trabalho, do primeiro material bruto ate o codigo entregue.

---

## O gesto de todo dia

**Nao sabe em que mexer?** Abra a sessao na raiz do vault:

```
cd /caminho/do/vault
claude
/brain
```

Sai o panorama: todos os projetos, em que fase, o que trava, quando foi tocado pela ultima vez.
Voce escolhe.

**Ja sabe?** Abra direto no projeto:

```
cd /caminho/do/vault/repos/backside/meu-projeto
claude
/brain
```

Sai o `STATUS.md`: onde parou, o que trava, proximo passo.

Mesmo comando. O que muda e de onde voce chama.

> **Por que nao se trabalha a partir da raiz.** Os comandos de projeto — `/spec`, `/loop`,
> `/save` — escrevem no repositorio onde a sessao esta aberta. Rodar da raiz gravaria no lugar
> errado. A raiz serve para decidir; o trabalho acontece dentro do projeto.

---

## O ciclo

### Comecar um projeto

```
cd X:/2brains
claude
/new-project
```

Pergunta o nome, a categoria (`backside`, `w3`, `private`) e o **perfil** — o que o projeto gera.
Cria a estrutura completa em `repos/{categoria}/{nome}/`, com `STATUS.md`, `WORKFLOW.md`,
`JOURNAL.md` e `.bks-profile.json`.

Os perfis:

| Perfil | Gera |
|---|---|
| `docs` | escopo, arquitetura, apresentacao — sem codigo |
| `fullstack` | documentacao, design, front, back, banco, infra |
| `frontend` | design, mocks, componentes, integracao |
| `backend` | API, dominio, persistencia, scripts |
| `component` | biblioteca, SDK, pacote |
| `infra` | IaC, pipeline, observabilidade |
| `data` | ETL, modelagem, BI |
| `legacy-docs` | documentar um legado, sem altera-lo |
| `reengineering` | documentar e reescrever um legado |

O perfil determina quais fases se aplicam. Projeto `docs` nunca recebe pergunta sobre banco de
dados.

### Do material bruto ao codigo

Todos os passos abaixo rodam **com a sessao aberta na raiz do projeto**.

**1 · Material entra**

```
/note arquitetura pretendida
```

Escreve em `docs/input/notas/`. Nota viva: cresce ao longo dos dias, com secao
`## Estado em AAAA-MM-DD`. Nunca decisao fechada — decisao vira ADR.

Material de terceiros vai a mao para `docs/input/research/`.

**2 · Consolidar**

```
/canonize
```

Le tudo de `docs/input/` e `docs/design/` e escreve `docs/canonical/CONTEXT.md`. A partir daqui, e
essa a fonte — o material bruto para de ser lido pelos comandos seguintes.

Rode quando as notas pararem de mudar. Consolidar cedo demais congela o que ainda estava se
formando.

**3 · Produto**

```
/prd
```

Do `CONTEXT.md` sai o PRD: o que o produto e, para quem, e o que conta como pronto.

**4 · Especificar**

```
/spec
```

Entrevista por bounded context. Gera `specs/features/FEAT-*.md`. Aprovado, gera
`specs/tests/TEST-*.md`. Aprovado, gera `specs/tasks/TASK-*.md`.

As tres aprovacoes importam. Spec sem teste vira codigo sem criterio de aceite.

**5 · Arquitetura**

```
/arch
```

Gera `outputs/ARCH-{projeto}.md` e atualiza o `README.md`. Diagramas na notacao BKS.

**6 · Implementar**

```
/loop
```

Implementa uma task sob LOOP-4: ate quatro tentativas contra goals verificaveis — build limpo,
testes verdes, cenarios da `TEST` cobertos.

**7 · Revisar**

```
/review
```

Revisao independente, read-only, em invocacao separada de quem implementou.

**8 · Fechar a sessao**

```
/save
```

Roteia o que a sessao produziu: decisoes para `decisions/`, specs para `specs/`, reescreve o
`STATUS.md`, acrescenta o marco no `JOURNAL.md`.

**Sempre feche com `/save`.** E ele que mantem o `STATUS.md` util — e o `STATUS.md` e o que o
`/brain` le da proxima vez.

---

## Retomando depois de semanas

```
cd /caminho/do/vault
claude
/brain
```

O panorama mostra o que estava ativo e o que travou. Escolha, abra a sessao no projeto, e rode
`/brain` de novo — agora ele le o `STATUS.md` daquele projeto.

Se o `STATUS.md` estiver velho em relacao ao `JOURNAL.md` ou ao git, o `/brain` avisa e oferece
atualizar.

---

## Conhecimento

**Do projeto** — o que o produto e vai para `brain/domain/`; como se constroi ali vai para
`brain/engineering/`.

**Transversal** — vale para mais de um projeto, ou para nenhum em particular: vai para
`knowledge/` do vault. Material bruto entra em `knowledge/raw/_inbox/` e o `/ingest` classifica.

A regra: se so faz sentido dentro de um projeto, e do projeto.

---

## O que o kit traz

O vault nao tem comandos nem skills. Vem tudo do plugin `bks-sdd-kit`:

| | |
|---|---|
| Skills | `bks-sdd`, `bks-dotnet-solutions`, `bks-typescript-solutions`, `bks-tests`, `bks-arch`, `bks-standards`, `bks-create-plan-tasks` |
| Comandos | `/brain` `/new-project` `/note` `/canonize` `/prd` `/spec` `/arch` `/loop` `/review` `/save` |
| Agentes | `planner` `builder` `reviewer` `scribe` |
| Guardas | recusam MediatR, comentario acima de cinco linhas, e tipo publico sem documentacao |

Detalhes em [`INTEGRACAO-KIT.md`](INTEGRACAO-KIT.md).
