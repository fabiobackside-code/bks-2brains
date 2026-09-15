# Setup — montando o seu vault

Do `git clone` até a primeira sessão produtiva. Meia hora, sem pressa.

Este repositório e um **template**: traz a estrutura e a documentação, não o conteúdo. O
conhecimento, o perfil e os projetos são seus, e nascem vazios — você os preenche seguindo os
passos abaixo.

---

## 0 · O que você precisa antes

| | |
|---|---|
| [Claude Code](https://claude.com/claude-code) | instalado e autenticado |
| `git` | qualquer versão recente |
| Um diretório para o vault | ele vai crescer; prefira um disco com folga |

Opcional, mas recomendado: [Obsidian](https://obsidian.md) apontado para a pasta do vault. Ele le
markdown puro e não interfere no git — serve para navegar e escrever com conforto.

---

## 1 · Clonar

```bash
git clone https://github.com/fabiobackside-code/bks-2brains meu-vault
cd meu-vault
```

O nome do diretório e seu. Nada no vault depende dele.

### Desligar do repositório de origem

O template já cumpriu o papel dele. O seu vault e outro repositório:

```bash
rm -rf .git
git init
git add -A
git commit -m "chore: vault inicial a partir do template"
```

Se quiser publicar o **seu** vault, crie um repositório **privado** e aponte para ele:

```bash
git remote add origin <url-do-seu-repositório-privado>
git push -u origin main
```

> **Privado, não público.** A partir do momento em que você escreve o perfil e o conhecimento, o
> vault passa a conter o que e seu. O `.gitignore` deste template protege as areas de conteúdo por
> padrão, mas a proteção real e o repositório ser privado.

---

## 2 · Instalar o kit

O vault não tem comando nenhum. Skills, comandos, agentes e guardas vêm do plugin
[`bks-sdd-kit`](https://github.com/fabiobackside-code/bks-sdd-kit), instalado uma vez por maquina:

```bash
git clone https://github.com/fabiobackside-code/bks-sdd-kit ~/bks-sdd-kit
claude plugin marketplace add ~/bks-sdd-kit
claude plugin install bks@bks-sdd-kit
```

Conferir:

```bash
claude plugin list
```

O plugin `bks` deve aparecer com escopo `user` — global, vale em qualquer pasta. O nome do plugin
é `bks`, o do repositório e do marketplace é `bks-sdd-kit`; é de `bks` que sai o prefixo dos
comandos.

Confira também que os comandos respondem: abra uma sessão e digite `/bks:` — a lista deve mostrar
`brain`, `save`, `canonize` e os demais. Se o plugin aparece em `plugin list` mas os comandos não
surgem, reinicie a sessão: o `claude plugin install` avisa `Restart to apply changes`.

### Apontar o kit para o vault

Duas variáveis de ambiente, em `~/.claude/settings.json`:

```json
{
  "env": {
    "BKS_VAULT": "/caminho/do/meu-vault",
    "BKS_KNOWLEDGE": "/caminho/do/meu-vault/knowledge"
  }
}
```

Use o caminho absoluto real. No Windows, barras normais funcionam: `C:/Users/você/meu-vault`.

---

## 3 · Escrever o seu perfil

O perfil é o único arquivo que o agente lê em **toda** sessão, de qualquer projeto. Ele responde:
quem e você, o que domina, como gosta de trabalhar, o que nunca deve ser sugerido.

```bash
cp workbench/profile.example.md workbench/profile.md
```

Abra e reescreva. O exemplo mostra a forma; o conteúdo tem que ser seu.

**O que faz diferença de verdade:**

| Secao | Por que importa |
|---|---|
| Identidade e experiência | calibra o nível da resposta — 20 anos de C# não precisam de explicação sobre `async` |
| Stack principal | o agente escolhe a lib certa sem perguntar |
| Arquitetura padrão | evita que cada projeto reinvente a estrutura |
| Regras inegociáveis | o que nunca fazer. Vale mais que tudo acima |
| Preferências de resposta | idioma, densidade, quando perguntar em vez de assumir |

**Escreva regra, não desejo.** "Nunca use MediatR — orquestração e explicita via pipeline" e
acionável. "Gosto de código limpo" não muda nada.

Comece curto. O perfil cresce quando você corrige o agente pela segunda vez na mesma coisa — essa
e a hora de virar regra escrita.

### Testar

```bash
cd /caminho/do/meu-vault
claude
```

Pergunte: *"Leia o profile.md. O que você entendeu sobre como eu trabalho? O que ficou ambiguo?"*

A resposta mostra o que o perfil comunica de fato. O que ele não souber responder, está faltando.

---

## 4 · Alimentar a base de conhecimento

`knowledge/` guarda o que atravessa projetos: padrões, fichamentos, referências. Nasce vazio.

```
knowledge/
├── raw/          material bruto, como veio
│   ├── _inbox/     entrada — ainda não classificado
│   ├── articles/   artigos e posts
│   ├── papers/     artigos academicos, PDFs
│   ├── videos/     transcrições de palestra e curso
│   ├── clippings/  recortes
│   ├── notes/      anotação sua
│   └── links/      só a referência
├── wiki/         conhecimento consolidado, por area
└── tools/        ingest e busca
```

### O ciclo: bruto entra, consolidado fica

```
raw/_inbox/  ──/ingest──>  raw/{tipo}/  +  wiki/{area}/
```

**1 · Jogue o material em `raw/_inbox/`.** PDF, markdown, texto colado, link. Sem organizar.

**2 · Rode o ingest**, com a sessão aberta na raiz do vault:

```
/bks:ingest
```

Ele le o que está no inbox, classifica por tipo, move para a pasta certa em `raw/` e escreve o
fichamento correspondente em `wiki/{area}/`.

**3 · O fichamento e o que se usa.** O bruto fica como fonte; a wiki e o que o agente consulta.

### Lote grande

Para processar vários de uma vez, liste em `knowledge/tools/batch-ingest.md`:

| # | Type | Path or URL | Title | Priority |
|---|---|---|---|---|
| 1 | pdf | `raw/papers/arquitetura-hexagonal.pdf` | Arquitetura Hexagonal | high |
| 2 | url | `https://exemplo.com/artigo` | Titulo do artigo | medium |

E peça: *"Processe todas as fontes de `knowledge/tools/batch-ingest.md`"*.

### Escrever direto na wiki

Nem tudo vem de fora. Para fichar o que você já sabe:

```
knowledge/wiki/patterns/nome-do-padrão.md
```

Um arquivo por assunto. As areas que vem no template: `architecture/`, `patterns/`, `ddd/`,
`sdd/`, `tdd/`, `foundations/`, `comparisons/`, `examples/`, `diagrams/`, `templates/`. Crie
outras se precisar — não há lista fechada.

**O que faz uma ficha util:** a ideia central em uma frase no topo, quando aplicar e quando não,
e um exemplo concreto. Resumo genérico não ajuda ninguém — nem você daqui a seis meses, nem o
agente.

### Buscar

```bash
./knowledge/tools/search.sh "circuit breaker"
```

Busca literal sobre a wiki. Para pergunta em linguagem natural, pergunte ao agente com a sessão
aberta no vault — ele le a wiki como contexto.

### O que NAO entra em knowledge/

Domínio de um produto específico. O método de treinamento do seu app de treino vive em
`repos/{categoria}/{projeto}/brain/domain/`, não aqui.

A regra: **se só faz sentido dentro de um projeto, e do projeto.**

---

## 5 · Criar o primeiro projeto

Com a sessão aberta na raiz do vault:

```
/bks:new-project
```

Pergunta o nome, a categoria (`backside`, `w3`, `private` — renomeie como quiser) e o **perfil**,
que determina o que o projeto gera:

| Perfil | Gera |
|---|---|
| `docs` | escopo, arquitetura, apresentação — sem código |
| `fullstack` | documentação, design, front, back, banco, infra |
| `frontend` | design, mocks, componentes, integração |
| `backend` | API, domínio, persistência, scripts |
| `component` | biblioteca, SDK, pacote |
| `infra` | IaC, pipeline, observabilidade |
| `data` | ETL, modelagem, BI |
| `legacy-docs` | documentar um legado, sem altera-lo |
| `reengineering` | documentar e reescrever um legado |

Cria `repos/{categoria}/{nome}/` completo, com `STATUS.md`, `WORKFLOW.md`, `JOURNAL.md` e
`.bks-profile.json`.

**Cada projeto tem git próprio.** O `.gitignore` do vault ignora `/repos/` justamente por isso: o
vault versiona a organização, não o conteúdo dos projetos.

Daqui em diante o ciclo de trabalho está em [`COMO-USAR.md`](COMO-USAR.md).

---

## 6 · Conferir que está de pé

```
cd /caminho/do/meu-vault
claude
/bks:brain
```

Deve sair o panorama — vazio, se você ainda não criou projeto. Se o comando não existir, o plugin
não está instalado ou não está habilitado; volte ao passo 2.

---

## O que fica fora do git

O `.gitignore` do template protege por lista de permissão: dentro de `knowledge/` e `workbench/`,
**tudo e ignorado por padrão** e só o que está liberado com `!` sobe. Um arquivo novo nasce
protegido.

Ficam de fora:

| O que | Por que |
|---|---|
| `knowledge/**` (menos READMEs e ferramentas) | acervo e seu, e parte dele e material de terceiro |
| `workbench/profile.md` | perfil pessoal |
| `STATUS.md`, `JOURNAL.md` | estado do seu vault |
| `/repos/`, `/kit/` | cada um tem git próprio |
| `*.mp4`, `*.pdf`, `*.docx` e afins | midia e documento pesado estouram o limite de 100 MB por arquivo do GitHub |
| `.env`, `*.pem`, `*.key`, `id_rsa*` | credencial nunca entra em git |
| `**/.logs/`, `.claude/settings.local.json` | log e configuração locais |

Se você for versionar o seu vault num repositório **privado** e quiser incluir o conhecimento,
libere o que precisar com `!` — mas mantenha as regras de credencial e midia intactas.

---

## Onde uma coisa nova vai

```
E sobre você, e vale para todo projeto?          → workbench/
E conhecimento geral, de mais de um projeto?     → knowledge/
E o que o produto E?                             → {projeto}/brain/domain/
E como se constrói neste projeto?                → {projeto}/brain/engineering/
E uma decisão fechada deste projeto?             → {projeto}/decisions/
E material bruto ainda não consolidado?          → {projeto}/docs/input/
E ferramenta, template, skill reusável?          → bks-sdd-kit, não aqui
```

Detalhe de cada diretório em [`ESTRUTURA.md`](ESTRUTURA.md).
