# Perfil — {{seu nome ou papel}}

> Copie para `profile.md` e reescreva. Este arquivo e um exemplo da **forma**; o conteudo tem que
> ser seu.
>
> O `profile.md` e o unico arquivo lido em toda sessao, de qualquer projeto. Vale mais que
> qualquer outra documentacao do vault: ele calibra o nivel da resposta e evita que voce corrija a
> mesma coisa toda semana.

## Identidade

{{Papel e tempo de experiencia. Uma ou duas linhas.}}

Exemplo: *Arquiteto backend, 15 anos. Prescritivo: prefiro recomendacao com argumento a lista de
opcoes. Quando discordar de mim, discorde com argumento tecnico.*

## Stack principal

{{As linguagens, frameworks e bancos que voce usa de verdade. Diga a versao quando ela importa —
".NET 10 para projeto novo, .NET Framework 4.7 em legado sob manutencao" muda a resposta;
"C#" sozinho nao.}}

- Linguagem e runtime:
- Framework de API / worker:
- Banco de dados:
- Mensageria e cache:
- Observabilidade:

## Arquitetura padrao

{{Como voce estrutura um projeto novo. Nomeie o padrao e diga o que ele exige na pratica.}}

Exemplo: *Hexagonal. Dominio sem dependencia de framework — so a biblioteca padrao da linguagem.
Dependencia sempre para dentro: adaptadores conhecem a aplicacao, a aplicacao conhece o dominio,
nunca o contrario.*

## Regras inegociaveis

{{A parte que mais rende. Escreva o que **nunca** deve ser feito, e por que. Uma linha cada.}}

- NUNCA {{o que}} — {{por que}}
- SEMPRE {{o que}} — {{por que}}

Exemplos do formato:

- NUNCA use `float` ou `double` em campo monetario — sempre `decimal`.
- NUNCA adicione dependencia nova sem confirmacao explicita — liste e aguarde.
- SEMPRE escreva teste junto com a implementacao. Task sem teste nao esta concluida.

**Escreva regra, nao desejo.** "Gosto de codigo limpo" nao muda nada. "Metodo acima de 20 linhas
precisa de justificativa" e verificavel.

## Qualidade

{{Os criterios que voce aplica em revisao. Diga tambem quais sao guia e quais sao lei — a
diferenca importa quando o agente tiver que escolher.}}

## Preferencias de trabalho

| | |
|---|---|
| Idioma da conversa | {{portugues do Brasil / ingles}} |
| Idioma do codigo | {{ingles — nomes de tipo, metodo, variavel}} |
| Densidade da resposta | {{direto e tecnico / com contexto e alternativas}} |
| Duvida de arquitetura | {{perguntar antes de implementar / assumir e sinalizar}} |
| Escopo | {{responder o que foi pedido / sugerir melhorias adjacentes}} |

## O que eu ja cansei de corrigir

{{Deixe vazio no comeco. Toda vez que voce corrigir o agente pela segunda vez na mesma coisa,
escreva aqui — e a secao que mais economiza tempo ao longo dos meses.}}
