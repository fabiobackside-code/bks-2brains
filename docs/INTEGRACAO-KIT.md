# Integracao com o kit

Como o vault e o plugin se encontram, e o que acontece quando um dos dois nao esta presente.

---

## A divisao

| | `bks-2brains` | `bks-sdd-kit` |
|---|---|---|
| E | o vault | o motor |
| Guarda | conhecimento, perfil, projetos | skills, comandos, agentes, hooks, templates |
| Muda quando | voce trabalha | o processo evolui |
| Serve | voce | qualquer um |
| Versionado em | seu repositorio | plugin publico, MIT |

A regra que decide onde uma coisa vai: **se outra pessoa usaria, e do kit; se e biografia, e do
vault.**

Por isso `dotnet-standards.md` foi para o kit — e metodo, reusavel. E `profile.md` ficou no vault
— e voce.

---

## Instalacao

**1 · O kit**

```
/plugin marketplace add fabiobackside-code/bks-sdd-kit
/plugin install bks-sdd-kit@bks-sdd-kit
```

**2 · O vault**

```bash
git clone https://github.com/fabiobackside-code/bks-2brains X:/2brains
```

**3 · A ligacao**

Em `~/.claude/settings.json`:

```json
{
  "env": {
    "BKS_VAULT": "X:/2brains",
    "BKS_KNOWLEDGE": "X:/2brains/knowledge"
  }
}
```

---

## As variaveis

| Variavel | Aponta para | Quem usa |
|---|---|---|
| `BKS_VAULT` | raiz do vault | `/brain` no modo panorama, `/new-project` |
| `BKS_KNOWLEDGE` | `knowledge/` | consulta a base transversal |

Sao duas, nao tres. A antiga `BKS_BRAIN` apontava para um hub central que nao existe mais —
memoria e decisao agora vivem dentro de cada projeto.

---

## Sem uma das partes

**Kit sem vault.** Funciona. As skills operam sobre o diretorio atual e nao leem o vault. Os
comandos de projeto — `/note`, `/canonize`, `/spec`, `/arch`, `/loop`, `/review`, `/save` —
trabalham dentro do repositorio onde a sessao esta aberta.

So dois comandos precisam do vault: `/brain` no modo panorama (que percorre `repos/`) e
`/new-project` (que cria dentro dele). Sem `BKS_VAULT`, ambos perguntam onde trabalhar.

**Vault sem kit.** Os arquivos continuam legiveis — sao markdown. O que se perde sao os comandos e
as skills. O `STATUS.md` de cada projeto segue sendo o ponto de entrada, so que lido a mao.

---

## Precedencia

Quando os dois existem, o vault e o projeto podem sobrepor o padrao do kit.

**Templates**

```
{projeto}/.bks/templates/     mais especifico
${BKS_VAULT}/workbench/templates/
${CLAUDE_PLUGIN_ROOT}/templates/    padrao do kit
```

O primeiro que existir vence.

**Skills**

Uma skill em `{projeto}/brain/engineering/` sobrescreve a equivalente do kit **para aquele
projeto**. E como o `nquantic` mantem o padrao de identificadores em pt-BR sem que isso vire regra
para os demais.

---

## Os guardas

O kit instala hooks que **recusam a escrita** quando a regra e violada:

| Guarda | Recusa |
|---|---|
| `no_dispatcher` | `MediatR`, `IMediator`, `IRequestHandler<>` e equivalentes em `.cs` |
| `comment_budget` | bloco de comentario acima de cinco linhas, marca de severidade |
| `dod_docs` | tipo publico novo enquanto `README.md` e `ARCHITECTURE.md` nao mudarem |

Ignoram arquivo de teste, arquivo fora de repositorio git, e o que nao e `.cs`.

Em repositorio legado, isso aparece na primeira edicao. Se a base ainda nao esta em conformidade,
desabilite o hook no `settings.json` do projeto ate estar — nao contorne arquivo a arquivo.

---

## Atualizando

```
/plugin update bks-sdd-kit@bks-sdd-kit
```

O vault nao e afetado: o kit nao escreve nele fora do que os comandos gravam a seu pedido.

Se uma atualizacao mudar o formato de um arquivo de estado — `STATUS.md`, `.bks-profile.json` — o
kit traz nota de migracao em `docs/MIGRATION.md`.
