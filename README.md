# bks-2brains

O vault. Guarda o que e **seu**: perfil, base de conhecimento, decisoes sobre o proprio processo,
e os projetos.

Nao guarda ferramenta. Skills, comandos, agentes e templates vem do plugin
[`bks-sdd-kit`](https://github.com/fabiobackside-code/bks-sdd-kit), que se instala uma vez e serve
qualquer maquina.

## A divisao

| | `bks-2brains` | `bks-sdd-kit` |
|---|---|---|
| O que e | o vault | o motor |
| Contem | conhecimento, perfil, projetos | skills, comandos, agentes, hooks, templates |
| Muda quando | voce trabalha | o processo evolui |
| Serve para | voce | qualquer um |

Os dois funcionam separados. Juntos, o kit sabe onde procurar o que e seu.

## Instalacao

```bash
git clone https://github.com/fabiobackside-code/bks-2brains
```

Instale o kit:

```
/plugin marketplace add fabiobackside-code/bks-sdd-kit
/plugin install bks-sdd-kit@bks-sdd-kit
```

E aponte o vault, em `~/.claude/settings.json`:

```json
{
  "env": {
    "BKS_VAULT": "X:/2brains",
    "BKS_KNOWLEDGE": "X:/2brains/knowledge"
  }
}
```

## Estrutura

```
bks-2brains/
├── workbench/          o que e seu e atravessa projetos
│   ├── profile.md      quem voce e, como trabalha
│   ├── decisions/      ADRs sobre o processo, nao sobre um projeto
│   └── knowledge-guide.md
├── knowledge/          base de conhecimento transversal
│   ├── wiki/           conhecimento consolidado
│   ├── raw/            material bruto por tipo
│   └── tools/          ingest e busca
├── repos/              os projetos, por categoria
│   ├── backside/
│   ├── w3/
│   └── private/
└── docs/               os guias deste vault
```

## Como se trabalha

Cada projeto e autossuficiente. Abrir o repositorio dele da acesso a tudo que ele precisa —
especificacao, decisao, dominio, e onde o trabalho parou.

```
sessao na raiz do vault    →  /brain  →  panorama de todos os projetos
sessao na raiz de um repo  →  /brain  →  onde este projeto parou
```

O ciclo completo esta em [`docs/COMO-USAR.md`](docs/COMO-USAR.md).

## Documentacao

| Documento | Sobre |
|---|---|
| [`docs/COMO-USAR.md`](docs/COMO-USAR.md) | o ciclo de trabalho, do inicio ao fim |
| [`docs/ESTRUTURA.md`](docs/ESTRUTURA.md) | cada diretorio, o que entra e o que nao entra |
| [`docs/INTEGRACAO-KIT.md`](docs/INTEGRACAO-KIT.md) | como vault e kit se encontram |

## Historico

Este repositorio continua o `bks-obsidian-2brains-ai-pattern`. Os commits anteriores a
reestruturacao estao preservados — o layout antigo, com hub central em `brain/_bks-ai/`, e
consultavel no historico.
