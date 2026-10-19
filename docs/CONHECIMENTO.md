---
tipo: guia
atualizado: 2026-09-15
---
# Alimentar o vault

Um vault vazio não muda nada. O que faz o agente decidir melhor não é o método — é o acervo que
ele consulta antes de responder. Este guia cobre como o acervo cresce: fontes externas, lições da
própria prática, e decisões que você não quer tomar duas vezes.

Há três destinos, e escolher errado é o defeito mais comum:

| O que você tem | Onde vai | Por quê |
|---|---|---|
| Artigo, paper, vídeo, livro — material de terceiro | `knowledge/raw/` → `knowledge/wiki/` | conhecimento transversal, vale para muitos projetos |
| Lição da sua prática, regra de como você trabalha | `workbench/` | é biografia sua, não conhecimento geral |
| Decisão que só vale para um produto | `repos/.../decisions/` | morre com o projeto, não polui o resto |

A pergunta que separa os três: **outra pessoa usaria isto?** Se sim, é `knowledge/`. Se só faz
sentido porque é você, é `workbench/`. Se só faz sentido dentro de um projeto, é do projeto.

---

## Fonte externa: de bruto a curado

O ciclo tem dois lados, e a separação entre eles é o que impede o acervo de apodrecer.

```
knowledge/
├── raw/      material como veio — imutável
└── wiki/     o que você concluiu dele — evolui
```

`raw/` é **imutável por convenção**: o arquivo original nunca é editado. Se a conclusão mudar,
muda a página em `wiki/`, não a fonte. Isso preserva a capacidade de conferir de onde uma
afirmação veio — que é o que separa conhecimento de lembrança.

### Onde cada tipo entra

```
raw/
├── papers/          PDFs, artigos acadêmicos
├── articles/        artigos web — .md clipado ou .html salvo
├── videos/          transcrições de vídeo, nunca o arquivo de mídia
├── clippings/       recortes de leitura
├── links/           URLs ainda não processadas
├── notes/           anotações soltas
├── notas-pessoais/  prospecção, linha de pensamento — não vira wiki
├── images/          imagens
├── assets/          diagramas que acompanham uma fonte
└── _inbox/          drop-zone: jogue aqui sem classificar
```

A distinção entre `notes/` e `notas-pessoais/` importa: a primeira é anotação sobre uma fonte, e
pode virar página curada. A segunda é pensamento em formação — fica arquivada, não vira wiki.

### O comando

```
/bkhar:ingest raw/papers/nome.pdf        uma fonte específica
/bkhar:ingest https://exemplo.com/artigo busca, salva cópia em raw/, ingere
/bkhar:ingest raw/_inbox/                classifica e processa tudo que está lá
/bkhar:ingest                            sem argumento: assume _inbox/
```

Cada tipo tem uma armadilha diferente para alucinação, e o comando trata cada um de um jeito —
transcrição de vídeo tem ruído de fala, PDF acadêmico tem citação a rastrear, artigo web tem
opinião vendida como fato.

O resultado é uma página em `wiki/{área}/`, mais as entradas em `wiki/index.md` e `wiki/log.md`.

---

## Curadoria: o que merece virar página

Ingerir tudo é tão ruim quanto não ingerir nada — um acervo inchado dilui o que importa e custa
contexto em toda sessão.

**Vira página de wiki** o que você vai querer citar de novo: um padrão que resolveu um problema
real, um trade-off que você mediu, uma armadilha que custou caro. O teste é a citabilidade — se
daqui a seis meses você diria "como está na minha wiki sobre X", é página.

**Não vira página** o que é resumo de leitura sem conclusão sua, o que o modelo já sabe sem
consultar nada, e o que você guardaria "porque pode ser útil um dia". Conteúdo guardado por via
das dúvidas nunca é consultado e sempre é carregado.

Uma página madura tem: a afirmação, a fonte que a sustenta, e o contexto em que vale. Afirmação
sem fonte é lembrança; fonte sem afirmação é recorte.

### Estado da página

O `/bkhar:ingest` marca a página como `draft`. Ela vira `stable` quando você a usou numa decisão
real e ela se sustentou. Página que nunca saiu de `draft` depois de meses é candidata a sair — ou
a conclusão não era tão útil, ou não estava madura.

---

## Erro para não repetir

Este é o material mais valioso do vault e o mais fácil de perder, porque o impulso depois de
resolver um problema é seguir em frente.

**Onde vai depende do alcance:**

- Errou por causa de uma característica de um produto → `repos/{projeto}/decisions/` ou o
  `JOURNAL.md` daquele projeto
- Errou por causa de uma característica de uma tecnologia → `knowledge/wiki/{área}/`, anonimizado
- Errou por causa de como você trabalha → `workbench/`

O terceiro é o que ninguém escreve, e é o que mais se repete. "Comecei a implementar antes de
fechar a spec" não é lição sobre .NET nem sobre o cliente — é sobre o seu processo, e só o
`workbench/` a guarda.

**O que registrar**, em qualquer dos três: o que você esperava, o que aconteceu, e o sinal que
teria avisado antes. Sem o terceiro, é desabafo — não muda a próxima vez.

**Anonimize ao subir para `knowledge/`.** Lição de projeto de cliente vira conhecimento geral
tirando nome, domínio e número. O que sobra é o padrão, que é o que vale.

---

## Decisão: global ou de projeto

| Pergunta | Se sim |
|---|---|
| Vale para todo projeto que eu tocar? | `workbench/decisions/` |
| Vale só enquanto este produto existir? | `repos/{projeto}/decisions/` |

Na dúvida, é do projeto. Decisão global que na verdade era de projeto contamina os próximos; o
contrário só custa uma cópia.

Decisão global é rara — é sobre o **processo de trabalho**, não sobre uma escolha técnica.
"Passamos a usar Dapper em vez de EF Core neste serviço" é de projeto. "Nunca fecho task sem
teste" é global.

**Só decisão fechada vira registro.** Discussão em aberto fica no `STATUS.md` do projeto, na
seção do que trava. Registro que documenta hesitação polui o log — quem lê depois não distingue o
que foi decidido do que foi cogitado.

---

## Por que isso reduz alucinação

Não é mágica, é mecânica: quanto mais o agente cita a sua wiki, menos ele recorre à memória do
treinamento. Uma afirmação com fonte em `raw/` é conferível; uma afirmação que o modelo "lembra"
não é.

O mesmo vale para o custo. Conhecimento no vault é lido sob demanda, quando a pergunta o exige —
não ocupa contexto em toda sessão. Um acervo curado de cinquenta páginas custa menos que
quinhentas linhas de instrução carregadas sempre.

O que o vault não resolve: se a página estiver errada, o agente erra com confiança e com citação.
Por isso a fonte em `raw/` é imutável e a página em `wiki/` tem estado — para você poder voltar e
conferir de onde a conclusão veio.

---

## Ver também

- [`ESTRUTURA.md`](ESTRUTURA.md) — o que cada diretório guarda, e o que não guarda
- [`COMO-USAR.md`](COMO-USAR.md) — o ciclo de trabalho num projeto
- [`OBSIDIAN.md`](OBSIDIAN.md) — navegar o acervo depois que ele cresce
