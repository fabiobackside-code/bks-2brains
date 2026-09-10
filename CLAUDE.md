# bks-2brains — vault

Você está na raiz do vault. Aqui se **decide** em que trabalhar; o trabalho acontece dentro do
repositório de cada projeto.

## O que este repositório é

O vault guarda o que atravessa projetos: perfil, base de conhecimento e decisões sobre o próprio
processo. Ferramenta não mora aqui — skills, comandos, agentes e templates vêm do plugin
`bks-sdd-kit`.

```
workbench/     perfil, decisões de processo
knowledge/     base transversal: wiki, material bruto, ingest
repos/         os projetos, por categoria
docs/          os guias deste vault
```

## O que fazer numa sessão aberta aqui

Rode `/brain`. Ele monta o panorama de todos os projetos a partir dos `STATUS.md` e diz qual tem
trabalho pronto para seguir.

Para trabalhar num projeto, abra uma sessão nova na pasta dele. Os comandos de projeto escrevem no
repositório onde a sessão está aberta — rodar daqui gravaria no lugar errado.

`/new-project` é a exceção: roda aqui, cria em `repos/{categoria}/{nome}/`.

## Antes de responder qualquer coisa

Leia `workbench/profile.md`. Ele diz quem é o usuário e como ele trabalha.

Se o arquivo não existir, o vault ainda não foi configurado: aponte `docs/SETUP.md` e ofereça
partir de `workbench/profile.example.md`.

## Onde uma coisa nova vai

| O que | Onde |
|---|---|
| Sobre o usuário, vale para todo projeto | `workbench/` |
| Conhecimento geral, mais de um projeto | `knowledge/` |
| Lição prática de Go, anonimizada | `knowledge/wiki/go/` |
| O que um produto é | `repos/.../brain/domain/` |
| Como se constrói num projeto | `repos/.../brain/engineering/` |
| Decisão fechada de um projeto | `repos/.../decisions/` |
| Ferramenta, template, skill reusável | `bks-sdd-kit`, não aqui |

Detalhes em `docs/ESTRUTURA.md`.

## Idioma

Documentação e artefatos em português do Brasil. Código, nomes de tipo, método e variável em
inglês.
