# workbench — o que e seu

Guarda o que atravessa todo projeto: quem você e e como você decidiu trabalhar.

| Arquivo | Guarda |
|---|---|
| `profile.md` | quem você e: papel, stack, arquitetura padrão, regras inegociáveis |
| `decisions/` | ADRs sobre o **processo**, não sobre um projeto |
| `knowledge-guide.md` | como você consulta a sua base de conhecimento |

## Comecando

```bash
cp profile.example.md profile.md
```

Abra e reescreva. O passo a passo está em [`../docs/SETUP.md`](../docs/SETUP.md), seção 3.

O `profile.md` e o único arquivo lido em **toda** sessão, de qualquer projeto — vale mais que
qualquer outra documentação do vault.

## Não entra aqui

| O que | Vai para |
|---|---|
| Padrão técnico reusável | o kit, em `skills/bks-standards/` |
| Estado de um projeto | o `STATUS.md` daquele projeto |
| Template | o kit, em `templates/` |
| Conhecimento técnico geral | `knowledge/wiki/` |

Um ADR aqui responde *"por que eu trabalho assim"*. Um ADR num projeto responde *"por que este
projeto e assim"*.

## Versionamento

`profile.md` **não sobe** para o repositório público — e seu. Sobem apenas este README e o
`profile.example.md`.
