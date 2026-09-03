# bks-2brains

Template de vault para trabalho assistido por IA. Traz a **estrutura** e a **documentacao** —
o conteudo e seu, e nasce vazio.

Um vault guarda o que atravessa projetos: quem voce e, o que voce aprendeu, e as decisoes sobre
como voce trabalha. Nao guarda ferramenta — skills, comandos, agentes e templates vem do plugin
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

## Comecando

**Leia [`docs/SETUP.md`](docs/SETUP.md).** Do `git clone` a primeira sessao produtiva, com os
comandos de cada passo.

O caminho curto:

```bash
git clone https://github.com/fabiobackside-code/bks-2brains meu-vault
cd meu-vault
rm -rf .git && git init          # o seu vault e outro repositorio
```

Instale o kit:

```
/plugin marketplace add fabiobackside-code/bks-sdd-kit
/plugin install bks-sdd-kit@bks-sdd-kit
```

Aponte o vault, em `~/.claude/settings.json`:

```json
{
  "env": {
    "BKS_VAULT": "/caminho/do/meu-vault",
    "BKS_KNOWLEDGE": "/caminho/do/meu-vault/knowledge"
  }
}
```

Escreva o seu perfil:

```bash
cp workbench/profile.example.md workbench/profile.md
```

## Estrutura

```
bks-2brains/
├── workbench/          o que e seu e atravessa projetos
│   ├── profile.md      quem voce e, como trabalha
│   ├── decisions/      ADRs sobre o processo, nao sobre um projeto
│   └── knowledge-guide.md
├── knowledge/          base de conhecimento transversal
│   ├── wiki/           conhecimento consolidado, por area
│   ├── raw/            material bruto por tipo
│   └── tools/          ingest e busca
├── repos/              os projetos, por categoria
│   ├── backside/
│   ├── w3/
│   └── private/
└── docs/               os guias deste vault
```

As pastas de conteudo vem vazias, com `.gitkeep`. O que preenche cada uma esta no
[`SETUP.md`](docs/SETUP.md).

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
| [`docs/SETUP.md`](docs/SETUP.md) | do clone a primeira sessao: instalar, configurar, alimentar |
| [`docs/COMO-USAR.md`](docs/COMO-USAR.md) | o ciclo de trabalho, do inicio ao fim |
| [`docs/ESTRUTURA.md`](docs/ESTRUTURA.md) | cada diretorio, o que entra e o que nao entra |
| [`docs/INTEGRACAO-KIT.md`](docs/INTEGRACAO-KIT.md) | como vault e kit se encontram |

## O que este repositorio nao publica

Nem o conteudo do vault de quem o mantem, nem o seu. O `.gitignore` protege por lista de
permissao: dentro de `knowledge/` e `workbench/`, tudo e ignorado por padrao e so o que esta
liberado com `!` sobe — um arquivo novo nasce protegido.

Ficam de fora acervo, perfil, estado (`STATUS.md`, `JOURNAL.md`), midia, documento pesado,
credencial e configuracao local. A lista completa esta no [`SETUP.md`](docs/SETUP.md).

Se voce for versionar o **seu** vault, use um repositorio **privado**.

## Licenca

Veja [`LICENSE`](LICENSE).
