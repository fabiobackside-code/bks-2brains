# Perfil — {{seu nome ou papel}}

> Copie para `profile.md` e reescreva. Este arquivo é um exemplo da **forma**; o conteúdo tem que
> ser seu.
>
> O `profile.md` e o único arquivo lido em toda sessão, de qualquer projeto. Vale mais que
> qualquer outra documentação do vault: ele calibra o nível da resposta e evita que você corrija a
> mesma coisa toda semana.

## Identidade

{{Papel e tempo de experiência. Uma ou duas linhas.}}

Exemplo: *Arquiteto backend, 15 anos. Prescritivo: prefiro recomendação com argumento a lista de
opções. Quando discordar de mim, discorde com argumento técnico.*

## Stack principal

{{As linguagens, frameworks e bancos que você usa de verdade. Diga a versão quando ela importa —
".NET 10 para projeto novo, .NET Framework 4.7 em legado sob manutenção" muda a resposta;
"C#" sozinho não.}}

- Linguagem e runtime:
- Framework de API / worker:
- Banco de dados:
- Mensageria e cache:
- Observabilidade:

## Arquitetura padrão

{{Como você estrutura um projeto novo. Nomeie o padrão e diga o que ele exige na prática.}}

Exemplo: *Hexagonal. Domínio sem dependência de framework — só a biblioteca padrão da linguagem.
Dependência sempre para dentro: adaptadores conhecem a aplicação, a aplicação conhece o domínio,
nunca o contrario.*

## Regras inegociáveis

{{A parte que mais rende. Escreva o que **nunca** deve ser feito, e por que. Uma linha cada.}}

- NUNCA {{o que}} — {{por que}}
- SEMPRE {{o que}} — {{por que}}

Exemplos do formato:

- NUNCA use `float` ou `double` em campo monetario — sempre `decimal`.
- NUNCA adicione dependência nova sem confirmação explicita — liste e aguarde.
- SEMPRE escreva teste junto com a implementação. Task sem teste não está concluida.

**Escreva regra, não desejo.** "Gosto de código limpo" não muda nada. "Metodo acima de 20 linhas
precisa de justificativa" e verificável.

## Qualidade

{{Os critérios que você aplica em revisão. Diga também quais são guia e quais são lei — a
diferença importa quando o agente tiver que escolher.}}

## Preferências de trabalho

| | |
|---|---|
| Idioma da conversa | {{português do Brasil / inglês}} |
| Idioma do código | {{inglês — nomes de tipo, método, variável}} |
| Densidade da resposta | {{direto e técnico / com contexto e alternativas}} |
| Dúvida de arquitetura | {{perguntar antes de implementar / assumir e sinalizar}} |
| Escopo | {{responder o que foi pedido / sugerir melhorias adjacentes}} |

## O que eu já cansei de corrigir

{{Deixe vazio no comeco. Toda vez que você corrigir o agente pela segunda vez na mesma coisa,
escreva aqui — e a seção que mais economiza tempo ao longo dos meses.}}
