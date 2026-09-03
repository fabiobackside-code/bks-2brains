# Estrutura

O que cada diretorio guarda, e — mais importante — o que ele **nao** guarda.

---

## A regra que organiza tudo

**O projeto e autossuficiente.** Abrir o repositorio de um projeto da acesso a tudo que ele
precisa: especificacao, decisao, dominio, padrao tecnico local, e onde o trabalho parou. Nenhum
comando de projeto le o vault para funcionar.

O vault guarda o que **atravessa** projetos: quem voce e, o que voce aprendeu em geral, e as
decisoes sobre como voce trabalha.

Isso substitui o layout anterior, em que um hub central (`brain/_bks-ai/`) guardava memoria,
agentes e templates de todos os projetos. O hub tinha um defeito: um projeto so funcionava com ele
por perto, e ele envelhecia sem que ninguem percebesse.

---

## Vault

```
bks-2brains/
├── workbench/
├── knowledge/
├── repos/
└── docs/
```

### `workbench/` — o que e seu

| Arquivo | Guarda |
|---|---|
| `profile.md` | quem voce e: papel, experiencia, preferencias de trabalho |
| `decisions/` | ADRs sobre o **processo**, nao sobre um projeto |
| `knowledge-guide.md` | como consultar a base de conhecimento |

**Nao entra:** padrao tecnico reusavel (vai para o kit, em `skills/bks-standards/`), estado de
projeto (vai para o `STATUS.md` do projeto), template (vai para o kit).

Um ADR aqui responde "por que eu trabalho assim". Um ADR num projeto responde "por que este
projeto e assim".

### `knowledge/` — o que voce aprendeu

```
knowledge/
├── wiki/       conhecimento consolidado, por area
├── raw/        material bruto, por tipo
│   ├── articles/ papers/ videos/ clippings/ notes/ links/
│   └── _inbox/   entrada, ainda nao classificado
└── tools/      ingest e busca
```

Conhecimento **transversal**: vale para mais de um projeto, ou para nenhum em particular.

**Nao entra:** dominio de um produto especifico. O metodo de treinamento de um app de treino vive em
`repos/backside/{projeto}/brain/domain/`, nao aqui. A regra: se so faz sentido dentro de um projeto,
e do projeto.

### `repos/` — os projetos

```
repos/
├── backside/
├── w3/
├── private/
└── old/        projetos encerrados, mantidos para consulta
```

Cada projeto tem git proprio. O vault versiona a organizacao, nao o conteudo deles.

### `docs/` — os guias

Como usar o vault. Nao e conhecimento tecnico — isso e `knowledge/`.

---

## Projeto

Todo projeto criado pelo `/new-project` nasce assim:

```
{{projeto}}/
├── STATUS.md              onde parei, o que trava, proximo passo
├── WORKFLOW.md            o fluxo de comandos deste projeto
├── JOURNAL.md             marcos e sessoes, do mais recente ao mais antigo
├── README.md              o que e o projeto
├── CLAUDE.md              contexto que o agente carrega
├── .bks-profile.json      perfil, renderer, eixos
│
├── brain/
│   ├── domain/            o que o produto E — regra de negocio, metodo, normativo
│   └── engineering/       como se constroi AQUI — padrao tecnico, skill local
│
├── docs/
│   ├── input/             material bruto: notas, entrevistas, pesquisa, escopo
│   ├── design/            bancada de trabalho
│   ├── canonical/         contexto consolidado — a fonte apos o /canonize
│   ├── history/           o que foi superado
│   └── prompts/           registro de auditoria do proprio processo
│
├── specs/
│   ├── features/          FEAT-*.md
│   ├── tests/             TEST-*.md
│   └── tasks/             TASK-*.md
│
├── decisions/             ADR-NNN deste projeto
├── outputs/               entregaveis gerados
└── app/                   codigo
```

### Os tres arquivos de estado

| Arquivo | Responde | Escrito por | Reescrito? |
|---|---|---|---|
| `STATUS.md` | onde o projeto esta **agora** | `/save` | sim, por inteiro |
| `JOURNAL.md` | como chegou ate aqui | `/save` | nao, so acrescenta |
| `WORKFLOW.md` | como se trabalha aqui | `/new-project` | so quando o fluxo muda |

O `STATUS.md` e o ponto de entrada. O `/brain` le ele.

### `brain/domain/` contra `brain/engineering/`

A separacao existe porque sao conhecimentos de natureza diferente, e o agente carrega um ou outro
conforme a tarefa.

**`domain/`** — o que o produto e. Regra de negocio, metodo, normativo, glossario do dominio.
Muda quando o produto muda. Exemplo: a metodologia de treinamento, a regra bancaria, o catalogo de
exercicios.

**`engineering/`** — como se constroi neste projeto. Padrao tecnico local, skill de
implementacao, convencao que vale so aqui. Muda quando a arquitetura muda. Exemplo: identificadores
em pt-BR sem acento, o contrato do motor de transacoes.

Uma skill em `engineering/` sobrescreve a equivalente do kit **para este projeto**.

---

## Onde uma coisa nova vai

```
E sobre voce, e vale para todo projeto?          → workbench/
E conhecimento geral, de mais de um projeto?     → knowledge/
E o que o produto E?                             → {projeto}/brain/domain/
E como se constroi neste projeto?                → {projeto}/brain/engineering/
E uma decisao fechada deste projeto?             → {projeto}/decisions/
E material bruto ainda nao consolidado?          → {projeto}/docs/input/
E ferramenta, template, skill reusavel?          → bks-sdd-kit, nao aqui
```
