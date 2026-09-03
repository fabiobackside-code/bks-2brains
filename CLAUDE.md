# bks-2brains — vault

Voce esta na raiz do vault. Aqui se **decide** em que trabalhar; o trabalho acontece dentro do
repositorio de cada projeto.

## O que este repositorio e

O vault guarda o que atravessa projetos: perfil, base de conhecimento e decisoes sobre o proprio
processo. Ferramenta nao mora aqui — skills, comandos, agentes e templates vem do plugin
`bks-sdd-kit`.

```
workbench/     perfil, decisoes de processo
knowledge/     base transversal: wiki, material bruto, ingest
repos/         os projetos, por categoria
docs/          os guias deste vault
```

## O que fazer numa sessao aberta aqui

Rode `/brain`. Ele monta o panorama de todos os projetos a partir dos `STATUS.md` e diz qual tem
trabalho pronto para seguir.

Para trabalhar num projeto, abra uma sessao nova na pasta dele. Os comandos de projeto escrevem no
repositorio onde a sessao esta aberta — rodar daqui gravaria no lugar errado.

`/new-project` e a excecao: roda aqui, cria em `repos/{categoria}/{nome}/`.

## Antes de responder qualquer coisa

Leia `workbench/profile.md`. Ele diz quem e o usuario e como ele trabalha.

Se o arquivo nao existir, o vault ainda nao foi configurado: aponte `docs/SETUP.md` e ofereca
partir de `workbench/profile.example.md`.

## Onde uma coisa nova vai

| O que | Onde |
|---|---|
| Sobre o usuario, vale para todo projeto | `workbench/` |
| Conhecimento geral, mais de um projeto | `knowledge/` |
| O que um produto e | `repos/.../brain/domain/` |
| Como se constroi num projeto | `repos/.../brain/engineering/` |
| Decisao fechada de um projeto | `repos/.../decisions/` |
| Ferramenta, template, skill reusavel | `bks-sdd-kit`, nao aqui |

Detalhes em `docs/ESTRUTURA.md`.

## Idioma

Documentacao e artefatos em portugues do Brasil. Codigo, nomes de tipo, metodo e variavel em
ingles.
