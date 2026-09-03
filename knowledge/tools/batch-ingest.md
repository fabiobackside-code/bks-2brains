# Batch ingest — lista de fontes

Liste aqui o que quer processar de uma vez, e peca ao agente, com a sessao aberta na raiz do
vault:

> Processe todas as fontes de `knowledge/tools/batch-ingest.md`

Para material avulso, o caminho normal e mais simples: jogue em `raw/_inbox/` e rode `/ingest`.

## Fontes

| # | Tipo | Caminho ou URL | Titulo | Prioridade |
|---|---|---|---|---|
| 1 | pdf | `raw/papers/{{arquivo}}.pdf` | {{titulo}} | high |
| 2 | url | `https://{{endereco}}` | {{titulo}} | medium |
| 3 | md | `raw/articles/{{arquivo}}.md` | {{titulo}} | low |

Tipos aceitos: `pdf` · `url` · `md` · `txt` · `video` (transcricao).

Prioridade orienta a ordem e a profundidade do fichamento: `high` rende ficha completa, `low`
rende registro curto com a referencia.

## Instrucoes deste lote

{{O recorte que interessa. Exemplo: "Foque em arquitetura, padroes de sistemas distribuidos e
orientacao pratica de implementacao — ignore comparativo de ferramenta e conteudo de marketing."}}

Sem esta secao o fichamento sai generico. Diga o que voce quer extrair.
