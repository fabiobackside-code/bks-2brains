# Como usar

O ciclo de trabalho, do primeiro material bruto até o código entregue.

---

## O gesto de todo dia

**Não sabe em que mexer?** Abra a sessão na raiz do vault:

```
cd /caminho/do/vault
claude
/bks:brain
```

Sai o panorama: todos os projetos, em que fase, o que trava, quando foi tocado pela última vez.
Você escolhe.

**Já sabe?** Abra direto no projeto:

```
cd /caminho/do/vault/repos/backside/meu-projeto
claude
/bks:brain
```

Sai o `STATUS.md`: onde parou, o que trava, próximo passo.

Mesmo comando. O que muda e de onde você chama.

> **Por que não se trabalha a partir da raiz.** Os comandos de projeto — `/bks:spec`, `/bks:loop`,
> `/bks:save` — escrevem no repositório onde a sessão está aberta. Rodar da raiz gravaria no lugar
> errado. A raiz serve para decidir; o trabalho acontece dentro do projeto.

---

## O ciclo

### Comecar um projeto

```
cd <raiz do seu vault>
claude
/bks:new-project
```

Pergunta o nome, a categoria (`backside`, `w3`, `private`) e o **perfil** — o que o projeto gera.
Cria a estrutura completa em `repos/{categoria}/{nome}/`, com `STATUS.md`, `WORKFLOW.md`,
`JOURNAL.md` e `.bks-profile.json`.

Os perfis:

| Perfil | Gera |
|---|---|
| `docs` | escopo, arquitetura, apresentação — sem código |
| `fullstack` | documentação, design, front, back, banco, infra |
| `frontend` | design, mocks, componentes, integração |
| `backend` | API, domínio, persistência, scripts |
| `component` | biblioteca, SDK, pacote |
| `infra` | IaC, pipeline, observabilidade |
| `data` | ETL, modelagem, BI |
| `legacy-docs` | documentar um legado, sem altera-lo |
| `reengineering` | documentar e reescrever um legado |

O perfil determina quais fases se aplicam. Projeto `docs` nunca recebe pergunta sobre banco de
dados.

### Do material bruto ao código

Todos os passos abaixo rodam **com a sessão aberta na raiz do projeto**.

**1 · Material entra**

```
/bks:note arquitetura pretendida
```

Escreve em `docs/input/notas/`. Nota viva: cresce ao longo dos dias, com seção
`## Estado em AAAA-MM-DD`. Nunca decisão fechada — decisão vira ADR.

Material de terceiros vai a mao para `docs/input/research/`.

**2 · Consolidar**

```
/bks:canonize
```

Le tudo de `docs/input/` e `docs/design/` e escreve `docs/canonical/CONTEXT.md`. A partir daqui, e
essa a fonte — o material bruto para de ser lido pelos comandos seguintes.

Rode quando as notas pararem de mudar. Consolidar cedo demais congela o que ainda estava se
formando.

**3 · Produto**

```
/bks:prd
```

Do `CONTEXT.md` sai o PRD: o que o produto e, para quem, e o que conta como pronto.

**4 · Especificar**

```
/bks:spec
```

Entrevista por bounded context. Gera `specs/features/FEAT-*.md`. Aprovado, gera
`specs/tests/TEST-*.md`. Aprovado, gera `specs/tasks/TASK-*.md`.

As três aprovações importam. Spec sem teste vira código sem critério de aceite.

**5 · Arquitetura**

```
/bks:arch
```

Gera `outputs/ARCH-{projeto}.md` e atualiza o `README.md`. Diagramas na notação BKS.

**6 · Implementar**

```
/bks:loop
```

Implementa uma task sob LOOP-4: até quatro tentativas contra goals verificáveis — build limpo,
testes verdes, cenários da `TEST` cobertos.

**7 · Revisar**

```
/bks:review
```

Revisão independente, read-only, em invocação separada de quem implementou.

**8 · Fechar a sessão**

```
/bks:save
```

Roteia o que a sessão produziu: decisões para `decisions/`, specs para `specs/`, reescreve o
`STATUS.md`, acrescenta o marco no `JOURNAL.md`.

**Sempre feche com `/bks:save`.** E ele que mantém o `STATUS.md` util — e o `STATUS.md` e o que o
`/bks:brain` le da próxima vez.

---

## Retomando depois de semanas

```
cd /caminho/do/vault
claude
/bks:brain
```

O panorama mostra o que estava ativo e o que travou. Escolha, abra a sessão no projeto, e rode
`/bks:brain` de novo — agora ele le o `STATUS.md` daquele projeto.

Se o `STATUS.md` estiver velho em relação ao `JOURNAL.md` ou ao git, o `/bks:brain` avisa e oferece
atualizar.

---

## Conhecimento

**Do projeto** — o que o produto e vai para `brain/domain/`; como se constrói ali vai para
`brain/engineering/`.

**Transversal** — vale para mais de um projeto, ou para nenhum em particular: vai para
`knowledge/` do vault. Material bruto entra em `knowledge/raw/_inbox/` e o `/bks:ingest` classifica.

A regra: se só faz sentido dentro de um projeto, e do projeto.

---

## O que o kit traz

O vault não tem comandos nem skills. Vem tudo do plugin `bks-sdd-kit`:

| | |
|---|---|
| Skills | `bks-sdd`, `bks-dotnet-solutions`, `bks-typescript-solutions`, `bks-tests`, `bks-arch`, `bks-standards`, `bks-create-plan-tasks` |
| Comandos | `/bks:brain` `/bks:new-project` `/bks:note` `/bks:canonize` `/bks:prd` `/bks:spec` `/bks:arch` `/bks:loop` `/bks:review` `/bks:save` |
| Agentes | `planner` `builder` `reviewer` `scribe` |
| Guardas | recusam MediatR, comentario acima de cinco linhas, e tipo público sem documentação |

Detalhes em [`INTEGRACAO-KIT.md`](INTEGRACAO-KIT.md).
