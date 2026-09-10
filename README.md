# bks-2brains

Template de vault para trabalho assistido por IA. Traz a **estrutura** e a **documentação** —
o conteúdo e seu, e nasce vazio.

Um vault guarda o que atravessa projetos: quem você e, o que você aprendeu, e as decisões sobre
como você trabalha. Não guarda ferramenta — skills, comandos, agentes e templates vêm do plugin
[`bks-sdd-kit`](https://github.com/fabiobackside-code/bks-sdd-kit), que se instala uma vez e serve
qualquer maquina.

## A divisão

| | `bks-2brains` | `bks-sdd-kit` |
|---|---|---|
| O que e | o vault | o motor |
| Contem | conhecimento, perfil, projetos | skills, comandos, agentes, hooks, templates |
| Muda quando | você trabalha | o processo evolui |
| Serve para | você | qualquer um |

Os dois funcionam separados. Juntos, o kit sabe onde procurar o que e seu.

## Comecando

**Leia [`docs/SETUP.md`](docs/SETUP.md).** Do `git clone` a primeira sessão produtiva, com os
comandos de cada passo.

O caminho curto:

```bash
git clone https://github.com/fabiobackside-code/bks-2brains meu-vault
cd meu-vault
rm -rf .git && git init          # o seu vault e outro repositório
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
│   ├── profile.md      quem você e, como trabalha
│   ├── decisions/      ADRs sobre o processo, não sobre um projeto
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

As pastas de conteúdo vem vazias, com `.gitkeep`. O que preenche cada uma está no
[`SETUP.md`](docs/SETUP.md).

## Como se trabalha

Cada projeto e autossuficiente. Abrir o repositório dele da acesso a tudo que ele precisa —
especificação, decisão, domínio, e onde o trabalho parou.

```
sessão na raiz do vault    →  /brain  →  panorama de todos os projetos
sessão na raiz de um repo  →  /brain  →  onde este projeto parou
```

O ciclo completo está em [`docs/COMO-USAR.md`](docs/COMO-USAR.md).

## Documentação

| Documento | Sobre |
|---|---|
| [`docs/SETUP.md`](docs/SETUP.md) | do clone a primeira sessão: instalar, configurar, alimentar |
| [`docs/COMO-USAR.md`](docs/COMO-USAR.md) | o ciclo de trabalho, do inicio ao fim |
| [`docs/ESTRUTURA.md`](docs/ESTRUTURA.md) | cada diretório, o que entra e o que não entra |
| [`docs/INTEGRACAO-KIT.md`](docs/INTEGRACAO-KIT.md) | como vault e kit se encontram |

## O que este repositório não publica

Nem o conteúdo do vault de quem o mantém, nem o seu. O `.gitignore` protege por lista de
permissão: dentro de `knowledge/` e `workbench/`, tudo e ignorado por padrão e só o que está
liberado com `!` sobe — um arquivo novo nasce protegido.

Ficam de fora acervo, perfil, estado (`STATUS.md`, `JOURNAL.md`), midia, documento pesado,
credencial e configuração local. A lista completa está no [`SETUP.md`](docs/SETUP.md).

Se você for versionar o **seu** vault, use um repositório **privado**.

## Licenca

Veja [`LICENSE`](LICENSE).
