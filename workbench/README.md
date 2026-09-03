# workbench — o que e seu

Guarda o que atravessa todo projeto: quem voce e e como voce decidiu trabalhar.

| Arquivo | Guarda |
|---|---|
| `profile.md` | quem voce e: papel, stack, arquitetura padrao, regras inegociaveis |
| `decisions/` | ADRs sobre o **processo**, nao sobre um projeto |
| `knowledge-guide.md` | como voce consulta a sua base de conhecimento |

## Comecando

```bash
cp profile.example.md profile.md
```

Abra e reescreva. O passo a passo esta em [`../docs/SETUP.md`](../docs/SETUP.md), secao 3.

O `profile.md` e o unico arquivo lido em **toda** sessao, de qualquer projeto — vale mais que
qualquer outra documentacao do vault.

## Nao entra aqui

| O que | Vai para |
|---|---|
| Padrao tecnico reusavel | o kit, em `skills/bks-standards/` |
| Estado de um projeto | o `STATUS.md` daquele projeto |
| Template | o kit, em `templates/` |
| Conhecimento tecnico geral | `knowledge/wiki/` |

Um ADR aqui responde *"por que eu trabalho assim"*. Um ADR num projeto responde *"por que este
projeto e assim"*.

## Versionamento

`profile.md` **nao sobe** para o repositorio publico — e seu. Sobem apenas este README e o
`profile.example.md`.
