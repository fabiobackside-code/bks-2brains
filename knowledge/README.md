# knowledge — o que voce aprendeu

Base transversal: vale para mais de um projeto, ou para nenhum em particular.

Nasce **vazia**. O passo a passo para alimenta-la esta em
[`../docs/SETUP.md`](../docs/SETUP.md), secao 4.

## Estrutura

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

## O ciclo

```
raw/_inbox/  ──/ingest──>  raw/{tipo}/  +  wiki/{area}/
```

1. Jogue o material em `raw/_inbox/` — sem organizar.
2. Rode `/ingest` com a sessao aberta na raiz do vault.
3. O bruto vai para a pasta certa em `raw/`; o fichamento nasce em `wiki/{area}/`.

A wiki e o que se consulta. O bruto fica como fonte.

## Areas da wiki

`architecture/` · `patterns/` · `ddd/` · `sdd/` · `tdd/` · `foundations/` · `comparisons/` ·
`examples/` · `diagrams/` · `templates/`

Nao e lista fechada — crie o que precisar.

## Buscar

```bash
./tools/search.sh "circuit breaker"
```

Busca literal sobre a wiki. Para pergunta em linguagem natural, pergunte ao agente com a sessao
aberta no vault.

## Nao entra aqui

Dominio de um produto especifico. O metodo de treinamento do seu app vive em
`repos/{categoria}/{projeto}/brain/domain/`, nao aqui.

**Se so faz sentido dentro de um projeto, e do projeto.**

## Versionamento

O acervo **nao sobe** para o repositorio publico: parte dele e material de terceiro, e o resto e
seu. Sobem apenas a estrutura de pastas, este README e as ferramentas de `tools/`.
