# Integração com o kit

Como o vault e o plugin se encontram, e o que acontece quando um dos dois não está presente.

---

## A divisão

| | `bks-2brains` | `bks-sdd-kit` |
|---|---|---|
| E | o vault | o motor |
| Guarda | conhecimento, perfil, projetos | skills, comandos, agentes, hooks, templates |
| Muda quando | você trabalha | o processo evolui |
| Serve | você | qualquer um |
| Versionado em | seu repositório | plugin público, MIT |

A regra que decide onde uma coisa vai: **se outra pessoa usaria, e do kit; se e biografia, e do
vault.**

Por isso `dotnet-standards.md` foi para o kit — e método, reusável. E `profile.md` ficou no vault
— e você.

---

## Instalação

**1 · O kit**

```
/plugin marketplace add fabiobackside-code/bks-sdd-kit
/plugin install bks-sdd-kit@bks-sdd-kit
```

**2 · O vault**

```bash
git clone https://github.com/fabiobackside-code/bks-2brains X:/2brains
```

**3 · A ligação**

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

## As variáveis

| Variável | Aponta para | Quem usa |
|---|---|---|
| `BKS_VAULT` | raiz do vault | `/brain` no modo panorama, `/new-project` |
| `BKS_KNOWLEDGE` | `knowledge/` | consulta a base transversal |

São duas, não três. A antiga `BKS_BRAIN` apontava para um hub central que não existe mais —
memória e decisão agora vivem dentro de cada projeto.

---

## Sem uma das partes

**Kit sem vault.** Funciona. As skills operam sobre o diretório atual e não leem o vault. Os
comandos de projeto — `/note`, `/canonize`, `/spec`, `/arch`, `/loop`, `/review`, `/save` —
trabalham dentro do repositório onde a sessão está aberta.

Só dois comandos precisam do vault: `/brain` no modo panorama (que percorre `repos/`) e
`/new-project` (que cria dentro dele). Sem `BKS_VAULT`, ambos perguntam onde trabalhar.

**Vault sem kit.** Os arquivos continuam legíveis — são markdown. O que se perde são os comandos e
as skills. O `STATUS.md` de cada projeto segue sendo o ponto de entrada, só que lido a mao.

---

## Precedência

Quando os dois existem, o vault e o projeto podem sobrepor o padrão do kit.

**Templates**

```
{projeto}/.bks/templates/     mais específico
${BKS_VAULT}/workbench/templates/
${CLAUDE_PLUGIN_ROOT}/templates/    padrão do kit
```

O primeiro que existir vence.

**Skills**

Uma skill em `{projeto}/brain/engineering/` sobrescreve a equivalente do kit **para aquele
projeto**. E como um projeto mantém o padrão de identificadores em pt-BR sem que isso vire regra
para os demais.

---

## Os guardas

O kit instala hooks que **recusam a escrita** quando a regra e violada:

| Guarda | Recusa |
|---|---|
| `no_dispatcher` | `MediatR`, `IMediator`, `IRequestHandler<>` e equivalentes em `.cs` |
| `comment_budget` | bloco de comentario acima de cinco linhas, marca de severidade |
| `dod_docs` | tipo público novo enquanto `README.md` e `ARCHITECTURE.md` não mudarem |

Ignoram arquivo de teste, arquivo fora de repositório git, e o que não e `.cs`.

Em repositório legado, isso aparece na primeira edição. Se a base ainda não está em conformidade,
desabilite o hook no `settings.json` do projeto até estar — não contorne arquivo a arquivo.

---

## Atualizando

```
/plugin update bks-sdd-kit@bks-sdd-kit
```

O vault não e afetado: o kit não escreve nele fora do que os comandos gravam a seu pedido.

Se uma atualização mudar o formato de um arquivo de estado — `STATUS.md`, `.bks-profile.json` — o
kit traz nota de migração em `docs/MIGRATION.md`.
