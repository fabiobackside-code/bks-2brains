---
tipo: guia
atualizado: 2026-09-15
---
# Ler o vault no Obsidian

O Claude Code escreve o vault; o Obsidian e como voce o le. Os dois olham para os mesmos arquivos
`.md` na mesma pasta — nao ha sincronizacao, nao ha nuvem no meio, nao ha formato proprietario.

Este guia e opcional: o vault funciona sem o Obsidian, porque e markdown em disco. O que o
Obsidian acrescenta e navegacao — busca, backlinks, grafo — sobre o que ja esta la.

O Obsidian é só um leitor/editor de arquivos `.md` de uma pasta (o *vault*). Ele não guarda nada em nuvem nem em banco: o que está na pasta é o que existe. Isso é perfeito pro seu caso, porque o Claude Code escreve arquivos e o Obsidian os mostra na hora.

## 1 Abrir o vault certo

Abra o Obsidian → **Open folder as vault** → aponte para a raiz do vault (`X:\2brains`, ou onde voce o clonou).
Pronto: `CLAUDE.md`, `workbench/`, `knowledge/`, `repos/`, tudo aparece na barra lateral esquerda (*File explorer*).

> Dica: `workbench/`, `knowledge/` e `repos/` são conceitualmente diferentes, mas mantê-los no **mesmo vault** do Obsidian é o que permite linkar uma spec a uma página da wiki com `[[ ]]`. Deixe um vault só.

## 2 Os 5 painéis que você vai usar o tempo todo

1. **File explorer** (`Ctrl+Shift+E`) — a árvore de pastas.
2. **Search** (`Ctrl+Shift+F`) — busca full-text em todo o vault. É o seu `grep` visual.
3. **Quick switcher** (`Ctrl+O`) — pula para qualquer arquivo digitando o nome. Você vai viver aqui.
4. **Graph view** (`Ctrl+G`) — o grafo de links. Útil para ver como specs, ADRs e conhecimento se conectam.
5. **Command palette** (`Ctrl+P`) — executa qualquer ação/plugin pelo nome.

Decore só três: `Ctrl+O` (abrir), `Ctrl+Shift+F` (buscar), `Ctrl+P` (comandos). Com esses três você já anda rápido.

> **Exemplo de uso (bks-marine):** você quer lembrar onde ficou a decisão da stack. `Ctrl+Shift+F` → digite `Supabase` → a busca lista `decisoes-abertas.md`, o `ADR-001` e o `arquitetura-macro.md`, todos com o trecho destacado. Achou o ADR? `Ctrl+O` → digite `FEAT-autenticacao` → abre a spec direto, sem navegar pasta por pasta. Quis ver como as specs desse projeto se relacionam com a wiki de conhecimento? `Ctrl+G` abre o grafo e você vê visualmente os nós de `specs/features/` puxando linhas para `brain/knowledge/wiki/`.

## 3 Links e backlinks — o que faz virar "cérebro"

Dentro de qualquer nota, `[[nome-da-nota]]` cria um link. No rodapé do painel direito, **Backlinks** mostra quem aponta para a nota atual. Isso é o que transforma pastas soltas em rede de conhecimento.

> **Exemplo passo a passo:** abra `specs/features/FEAT-autenticacao.md` e escreva a frase `Baseado em [[txc-transaction-context]]`. O Obsidian sublinha o texto como link (fica vermelho/pontilhado se a página ainda não existir, azul se já existir). Agora abra `brain/knowledge/wiki/architecture/txc-transaction-context.md` e olhe o painel **Backlinks** no rodapé direito: ele lista `FEAT-autenticacao.md` como uma das notas que apontam para ali — sem você ter feito nada além de escrever o `[[ ]]`. Repita o mesmo em `ADR-001.md` com `Afeta [[FEAT-autenticacao]]`, e agora a própria `FEAT-autenticacao.md` passa a mostrar o ADR no seu painel de Backlinks. É esse ir-e-vir automático que vira rede — não uma pasta, um grafo.

Uso concreto no seu fluxo:
- Num `FEAT-*.md` (agora dentro do repo, em `specs/features/`), linke a página da wiki que fundamentou a decisão: `Baseado em [[txc-transaction-context]]`.
- Num `ADR-NNN.md` (agora dentro do repo, em `decisions/`), linke a feature afetada: `Afeta [[FEAT-login]]`.
- No `STATUS.md` do projeto, linke as specs relevantes: assim a ficha vira um índice vivo.

## 4 Plugins — o mínimo que vale a pena (Community plugins)

Ative em **Settings → Community plugins → Browse**. Comece com poucos; adicione só quando sentir falta.

| Plugin | Para quê | Prioridade |
|--------|----------|-----------|
| **Dataview** | Monta tabelas/painéis vivos a partir do frontmatter (dashboard de specs, ADRs, projetos) | Alta |
| **Templater** | Cria nota nova já preenchida a partir dos seus templates | Alta |
| **Obsidian Git** | Faz commit/backup automático do vault (versiona seu conhecimento) | Média |
| **Mermaid** (core, já embutido) | Renderiza os diagramas C4 que o `/bkhar:arch` gera | Já tem |
| **Kanban** | Board visual de tarefas do projeto, se você gosta de quadro | Baixa |
| **Home tab / Dashboard++** | Uma home page do vault | Baixa |

> Core plugins (nativos) que valem ligar: **Templates**, **Backlinks**, **Outline**, **Page preview**, **Command palette**. Mermaid já vem ligado.

**Exemplo de uso de cada plugin de prioridade Alta/Média** (instale, ative em Community plugins, e teste assim):

- **Dataview** — crie uma nota `HOME.md` na raiz e cole:
  ````markdown
  ```dataview
  table status, context as "Bounded Context"
  from "repos/backside/bks-marine/specs/features"
  where tipo = "feat"
  ```
  ````
  Salve e abra em modo leitura (`Ctrl+E`): aparece uma tabela viva com todas as `FEAT-*.md` do bks-marine e o status de cada uma — sem você montar a tabela à mão. Queries prontas para copiar: Apêndice A.
- **Templater** — em Settings → Templater, aponte a pasta de templates para onde voce guarda os seus. Depois, `Ctrl+P` → "Templater: Create new note from template" → escolha `FEAT.md` → ele cria a nota já com o frontmatter (`tipo: feat`, `status: rascunho`) preenchido, em vez de você copiar/colar manualmente.
- **Obsidian Git** — em Settings → Git, ligue "Vault backup interval" para `60` (minutos) e "Commit message on backup" para algo como `backup: {{date}}`. A partir daí, a cada hora o plugin roda `git add . && git commit` sozinho sobre o vault inteiro — seu conhecimento fica versionado sem você lembrar de commitar.

## 5 Frontmatter — o que destrava os painéis

Hoje seus templates usam header inline (`**Status:** Rascunho`). O Obsidian não consegue filtrar por isso. Para ter dashboards, basta pôr um bloco YAML no topo das notas (o Obsidian chama de *Properties*):

```markdown
---
tipo: feat
projeto: bks-marine
categoria: backside
context: Autenticacao
status: rascunho     # rascunho | aprovada | em-execucao | concluida
---
# FEAT-login
...
```

Com isso, o Dataview monta sozinho a tabela de todas as features do projeto e seu status (queries prontas no Apêndice A). Os templates já vêm com frontmatter (seção 6).

## 6 Rotina de fluência (2 semanas, 10 min/dia)

- **Dia 1–2:** abrir o vault, navegar com `Ctrl+O`, ler o `CONTEXT.md` e 2 páginas da `knowledge/wiki/`.
  > *O que você deve conseguir fazer ao final:* abrir `CONTEXT.md` sem usar o mouse — só `Ctrl+O` + digitar "context" + Enter.
- **Dia 3–4:** criar uma nota em `brain/notes/`, linkar (`[[ ]]`) para uma página da wiki, ver o backlink aparecer.
  > *Exemplo:* crie `brain/notes/estudo-hexagonal.md`, escreva `Ver também [[hexagonal-architecture]]` e confirme no painel Backlinks da página da wiki que sua nota nova apareceu listada lá — é o mesmo mecanismo do exemplo da seção 2.3.
- **Dia 5–6:** instalar Dataview + Templater; colar um dashboard do Apêndice A numa nota `HOME.md`.
  > *O que você deve ver ao final:* abrir `HOME.md` em modo leitura e enxergar uma tabela viva com as features do bks-marine (não um bloco de código cru) — sinal de que o Dataview está processando a query.
- **Semana 2:** rodar um projeto de verdade (o bks-marine) e usar o Obsidian só para **ler** o que o Claude Code escreve — specs, ADRs, o ARCH com diagrama. A fluência vem do uso real, não de estudar o app.
  > *Exemplo:* depois de um `/bkhar:spec` no terminal, abra `specs/features/FEAT-autenticacao.md` no Obsidian — não no editor de texto — e confirme que os `[[ ]]` que o Claude escreveu já aparecem clicáveis e o Mermaid do `/bkhar:arch` renderiza como diagrama, não como texto bruto.

---

