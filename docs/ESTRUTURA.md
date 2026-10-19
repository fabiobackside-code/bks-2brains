# Estrutura

O que cada diretório guarda, e — mais importante — o que ele **não** guarda.

---

## A regra que organiza tudo

**O projeto e autossuficiente.** Abrir o repositório de um projeto da acesso a tudo que ele
precisa: especificação, decisão, domínio, padrão técnico local, e onde o trabalho parou. Nenhum
comando de projeto le o vault para funcionar.

O vault guarda o que **atravessa** projetos: quem você e, o que você aprendeu em geral, e as
decisões sobre como você trabalha.

Isso substitui o layout anterior, em que um hub central (`brain/_bks-ai/`) guardava memória,
agentes e templates de todos os projetos. O hub tinha um defeito: um projeto só funcionava com ele
por perto, e ele envelhecia sem que ninguém percebesse.

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
| `profile.md` | quem você e: papel, experiência, preferências de trabalho |
| `decisions/` | ADRs sobre o **processo**, não sobre um projeto |
| `knowledge-guide.md` | como consultar a base de conhecimento |

**Não entra:** padrão técnico reusável (vai para o kit, em `skills/bks-standards/`), estado de
projeto (vai para o `STATUS.md` do projeto), template (vai para o kit).

Um ADR aqui responde "por que eu trabalho assim". Um ADR num projeto responde "por que este
projeto e assim".

### `knowledge/` — o que você aprendeu

```
knowledge/
├── wiki/       conhecimento consolidado, por area
├── raw/        material bruto, por tipo
│   ├── articles/ papers/ videos/ clippings/ notes/ links/
│   └── _inbox/   entrada, ainda não classificado
└── tools/      ingest e busca
```

Conhecimento **transversal**: vale para mais de um projeto, ou para nenhum em particular.

**Não entra:** domínio de um produto específico. O método de treinamento de um app de treino vive em
`repos/backside/{projeto}/brain/domain/`, não aqui. A regra: se só faz sentido dentro de um projeto,
e do projeto.

### `repos/` — os projetos

```
repos/
├── backside/
├── w3/
├── private/
└── old/        projetos encerrados, mantidos para consulta
```

Cada projeto tem git próprio. O vault versiona a organização, não o conteúdo deles.

### `docs/` — os guias

Como usar o vault. Não e conhecimento técnico — isso e `knowledge/`.

---

## Projeto

Todo projeto criado pelo `/bkhar:new-project` nasce assim:

```
{{projeto}}/
├── STATUS.md              onde parei, o que trava, próximo passo
├── WORKFLOW.md            o fluxo de comandos deste projeto
├── JOURNAL.md             marcos e sessões, do mais recente ao mais antigo
├── README.md              o que é o projeto
├── CLAUDE.md              contexto que o agente carrega
├── .bks-profile.json      perfil, renderer, eixos
│
├── brain/
│   ├── domain/            o que o produto E — regra de negócio, método, normativo
│   └── engineering/       como se constrói AQUI — padrão técnico, skill local
│
├── docs/
│   ├── input/             material bruto: notas, entrevistas, pesquisa, escopo
│   ├── design/            bancada de trabalho
│   ├── canonical/         contexto consolidado — a fonte após o /canonize
│   ├── history/           o que foi superado
│   └── prompts/           registro de auditoria do próprio processo
│
├── specs/
│   ├── features/          FEAT-*.md
│   ├── tests/             TEST-*.md
│   └── tasks/             TASK-*.md
│
├── decisions/             ADR-NNN deste projeto
├── outputs/               entregáveis gerados
└── app/                   código
```

### Os três arquivos de estado

| Arquivo | Responde | Escrito por | Reescrito? |
|---|---|---|---|
| `STATUS.md` | onde o projeto está **agora** | `/bkhar:save` | sim, por inteiro |
| `JOURNAL.md` | como chegou até aqui | `/bkhar:save` | não, só acrescenta |
| `WORKFLOW.md` | como se trabalha aqui | `/bkhar:new-project` | só quando o fluxo muda |

O `STATUS.md` e o ponto de entrada. O `/bkhar:brain` le ele.

### `brain/domain/` contra `brain/engineering/`

A separação existe porque são conhecimentos de natureza diferente, e o agente carrega um ou outro
conforme a tarefa.

**`domain/`** — o que o produto e. Regra de negócio, método, normativo, glossario do domínio.
Muda quando o produto muda. Exemplo: a metodologia de treinamento, a regra bancaria, o catalogo de
exercicios.

**`engineering/`** — como se constrói neste projeto. Padrão técnico local, skill de
implementação, convenção que vale só aqui. Muda quando a arquitetura muda. Exemplo: identificadores
em pt-BR sem acento, o contrato do motor de transações.

Uma skill em `engineering/` sobrescreve a equivalente do kit **para este projeto**.

---

## Onde uma coisa nova vai

```
E sobre você, e vale para todo projeto?          → workbench/
E conhecimento geral, de mais de um projeto?     → knowledge/
E o que o produto E?                             → {projeto}/brain/domain/
E como se constrói neste projeto?                → {projeto}/brain/engineering/
E uma decisão fechada deste projeto?             → {projeto}/decisions/
E material bruto ainda não consolidado?          → {projeto}/docs/input/
E ferramenta, template, skill reusável?          → o plugin bkhar, não aqui
```

---

## Convenções que não se negociam

- **Idioma:** nome de pasta e de arquivo em inglês; conteúdo e conversa em PT-BR; código em inglês.
- **Encoding:** UTF-8 sem BOM, quebras de linha `
`. Vale para todo arquivo do vault.
- **`knowledge/raw/` é imutável.** A fonte nunca é editada — só a página curada em `wiki/` evolui
  a partir dela. É o que permite conferir de onde uma afirmação veio.
- **Segurança:** nunca gravar segredo, token ou dado de cliente no vault. Ele é versionado e o
  repositório é público; o que está em `knowledge/` fica fora do git, mas o resto sobe.

## O que este arranjo busca

Três objetivos, e nenhum deles é organização pela organização:

- **Assertividade** — decisão ancorada na wiki e nas specs, não em achismo.
- **Menos alucinação** — o agente consulta a base curada antes de gerar, e marca o que é incerto
  em vez de chutar.
- **Menos tokens** — conteúdo curto, delimitado e cruzado por links, lido sob demanda, em vez de
  reexplicar tudo a cada sessão.

Como alimentar a base que sustenta os três: [`CONHECIMENTO.md`](CONHECIMENTO.md).
