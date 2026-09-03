# Setup — montando o seu vault

Do `git clone` ate a primeira sessao produtiva. Meia hora, sem pressa.

Este repositorio e um **template**: traz a estrutura e a documentacao, nao o conteudo. O
conhecimento, o perfil e os projetos sao seus, e nascem vazios — voce os preenche seguindo os
passos abaixo.

---

## 0 · O que voce precisa antes

| | |
|---|---|
| [Claude Code](https://claude.com/claude-code) | instalado e autenticado |
| `git` | qualquer versao recente |
| Um diretorio para o vault | ele vai crescer; prefira um disco com folga |

Opcional, mas recomendado: [Obsidian](https://obsidian.md) apontado para a pasta do vault. Ele le
markdown puro e nao interfere no git — serve para navegar e escrever com conforto.

---

## 1 · Clonar

```bash
git clone https://github.com/fabiobackside-code/bks-2brains meu-vault
cd meu-vault
```

O nome do diretorio e seu. Nada no vault depende dele.

### Desligar do repositorio de origem

O template ja cumpriu o papel dele. O seu vault e outro repositorio:

```bash
rm -rf .git
git init
git add -A
git commit -m "chore: vault inicial a partir do template"
```

Se quiser publicar o **seu** vault, crie um repositorio **privado** e aponte para ele:

```bash
git remote add origin <url-do-seu-repositorio-privado>
git push -u origin main
```

> **Privado, nao publico.** A partir do momento em que voce escreve o perfil e o conhecimento, o
> vault passa a conter o que e seu. O `.gitignore` deste template protege as areas de conteudo por
> padrao, mas a protecao real e o repositorio ser privado.

---

## 2 · Instalar o kit

O vault nao tem comando nenhum. Skills, comandos, agentes e guardas vem do plugin
[`bks-sdd-kit`](https://github.com/fabiobackside-code/bks-sdd-kit), instalado uma vez por maquina:

```bash
git clone https://github.com/fabiobackside-code/bks-sdd-kit ~/bks-sdd-kit
claude plugin marketplace add ~/bks-sdd-kit
claude plugin install bks-sdd-kit@bks-sdd-kit
```

Conferir:

```bash
claude plugin list
```

`bks-sdd-kit` deve aparecer com escopo `user` — global, vale em qualquer pasta.

### Apontar o kit para o vault

Duas variaveis de ambiente, em `~/.claude/settings.json`:

```json
{
  "env": {
    "BKS_VAULT": "/caminho/do/meu-vault",
    "BKS_KNOWLEDGE": "/caminho/do/meu-vault/knowledge"
  }
}
```

Use o caminho absoluto real. No Windows, barras normais funcionam: `C:/Users/voce/meu-vault`.

---

## 3 · Escrever o seu perfil

O perfil e o unico arquivo que o agente le em **toda** sessao, de qualquer projeto. Ele responde:
quem e voce, o que domina, como gosta de trabalhar, o que nunca deve ser sugerido.

```bash
cp workbench/profile.example.md workbench/profile.md
```

Abra e reescreva. O exemplo mostra a forma; o conteudo tem que ser seu.

**O que faz diferenca de verdade:**

| Secao | Por que importa |
|---|---|
| Identidade e experiencia | calibra o nivel da resposta — 20 anos de C# nao precisam de explicacao sobre `async` |
| Stack principal | o agente escolhe a lib certa sem perguntar |
| Arquitetura padrao | evita que cada projeto reinvente a estrutura |
| Regras inegociaveis | o que nunca fazer. Vale mais que tudo acima |
| Preferencias de resposta | idioma, densidade, quando perguntar em vez de assumir |

**Escreva regra, nao desejo.** "Nunca use MediatR — orquestracao e explicita via pipeline" e
acionavel. "Gosto de codigo limpo" nao muda nada.

Comece curto. O perfil cresce quando voce corrige o agente pela segunda vez na mesma coisa — essa
e a hora de virar regra escrita.

### Testar

```bash
cd /caminho/do/meu-vault
claude
```

Pergunte: *"Leia o profile.md. O que voce entendeu sobre como eu trabalho? O que ficou ambiguo?"*

A resposta mostra o que o perfil comunica de fato. O que ele nao souber responder, esta faltando.

---

## 4 · Alimentar a base de conhecimento

`knowledge/` guarda o que atravessa projetos: padroes, fichamentos, referencias. Nasce vazio.

```
knowledge/
├── raw/          material bruto, como veio
│   ├── _inbox/     entrada — ainda nao classificado
│   ├── articles/   artigos e posts
│   ├── papers/     artigos academicos, PDFs
│   ├── videos/     transcricoes de palestra e curso
│   ├── clippings/  recortes
│   ├── notes/      anotacao sua
│   └── links/      so a referencia
├── wiki/         conhecimento consolidado, por area
└── tools/        ingest e busca
```

### O ciclo: bruto entra, consolidado fica

```
raw/_inbox/  ──/ingest──>  raw/{tipo}/  +  wiki/{area}/
```

**1 · Jogue o material em `raw/_inbox/`.** PDF, markdown, texto colado, link. Sem organizar.

**2 · Rode o ingest**, com a sessao aberta na raiz do vault:

```
/ingest
```

Ele le o que esta no inbox, classifica por tipo, move para a pasta certa em `raw/` e escreve o
fichamento correspondente em `wiki/{area}/`.

**3 · O fichamento e o que se usa.** O bruto fica como fonte; a wiki e o que o agente consulta.

### Lote grande

Para processar varios de uma vez, liste em `knowledge/tools/batch-ingest.md`:

| # | Type | Path or URL | Title | Priority |
|---|---|---|---|---|
| 1 | pdf | `raw/papers/arquitetura-hexagonal.pdf` | Arquitetura Hexagonal | high |
| 2 | url | `https://exemplo.com/artigo` | Titulo do artigo | medium |

E peca: *"Processe todas as fontes de `knowledge/tools/batch-ingest.md`"*.

### Escrever direto na wiki

Nem tudo vem de fora. Para fichar o que voce ja sabe:

```
knowledge/wiki/patterns/nome-do-padrao.md
```

Um arquivo por assunto. As areas que vem no template: `architecture/`, `patterns/`, `ddd/`,
`sdd/`, `tdd/`, `foundations/`, `comparisons/`, `examples/`, `diagrams/`, `templates/`. Crie
outras se precisar — nao ha lista fechada.

**O que faz uma ficha util:** a ideia central em uma frase no topo, quando aplicar e quando nao,
e um exemplo concreto. Resumo generico nao ajuda ninguem — nem voce daqui a seis meses, nem o
agente.

### Buscar

```bash
./knowledge/tools/search.sh "circuit breaker"
```

Busca literal sobre a wiki. Para pergunta em linguagem natural, pergunte ao agente com a sessao
aberta no vault — ele le a wiki como contexto.

### O que NAO entra em knowledge/

Dominio de um produto especifico. O metodo de treinamento do seu app de treino vive em
`repos/{categoria}/{projeto}/brain/domain/`, nao aqui.

A regra: **se so faz sentido dentro de um projeto, e do projeto.**

---

## 5 · Criar o primeiro projeto

Com a sessao aberta na raiz do vault:

```
/new-project
```

Pergunta o nome, a categoria (`backside`, `w3`, `private` — renomeie como quiser) e o **perfil**,
que determina o que o projeto gera:

| Perfil | Gera |
|---|---|
| `docs` | escopo, arquitetura, apresentacao — sem codigo |
| `fullstack` | documentacao, design, front, back, banco, infra |
| `frontend` | design, mocks, componentes, integracao |
| `backend` | API, dominio, persistencia, scripts |
| `component` | biblioteca, SDK, pacote |
| `infra` | IaC, pipeline, observabilidade |
| `data` | ETL, modelagem, BI |
| `legacy-docs` | documentar um legado, sem altera-lo |
| `reengineering` | documentar e reescrever um legado |

Cria `repos/{categoria}/{nome}/` completo, com `STATUS.md`, `WORKFLOW.md`, `JOURNAL.md` e
`.bks-profile.json`.

**Cada projeto tem git proprio.** O `.gitignore` do vault ignora `/repos/` justamente por isso: o
vault versiona a organizacao, nao o conteudo dos projetos.

Daqui em diante o ciclo de trabalho esta em [`COMO-USAR.md`](COMO-USAR.md).

---

## 6 · Conferir que esta de pe

```
cd /caminho/do/meu-vault
claude
/brain
```

Deve sair o panorama — vazio, se voce ainda nao criou projeto. Se o comando nao existir, o plugin
nao esta instalado ou nao esta habilitado; volte ao passo 2.

---

## O que fica fora do git

O `.gitignore` do template protege por lista de permissao: dentro de `knowledge/` e `workbench/`,
**tudo e ignorado por padrao** e so o que esta liberado com `!` sobe. Um arquivo novo nasce
protegido.

Ficam de fora:

| O que | Por que |
|---|---|
| `knowledge/**` (menos READMEs e ferramentas) | acervo e seu, e parte dele e material de terceiro |
| `workbench/profile.md` | perfil pessoal |
| `STATUS.md`, `JOURNAL.md` | estado do seu vault |
| `/repos/`, `/kit/` | cada um tem git proprio |
| `*.mp4`, `*.pdf`, `*.docx` e afins | midia e documento pesado estouram o limite de 100 MB por arquivo do GitHub |
| `.env`, `*.pem`, `*.key`, `id_rsa*` | credencial nunca entra em git |
| `**/.logs/`, `.claude/settings.local.json` | log e configuracao locais |

Se voce for versionar o seu vault num repositorio **privado** e quiser incluir o conhecimento,
libere o que precisar com `!` — mas mantenha as regras de credencial e midia intactas.

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

Detalhe de cada diretorio em [`ESTRUTURA.md`](ESTRUTURA.md).
