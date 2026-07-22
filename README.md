# IA Builder — Case Técnico

> Teste técnico pra avaliar como você **constrói com IA**: raciocínio, trade-offs e mão na massa. Use a ferramenta de IA que preferir.

## Menu rápido

- [Hey there 👋](#hey-there-)
- [O que tem nesse repo](#o-que-tem-nesse-repo)
- [Como funciona o case](#como-funciona-o-case)
- [Entrada e saída](#entrada-e-saída)
- [Como começar](#como-começar)
- [Como funciona a sessão](#como-funciona-a-sessão)
- [Combinados](#combinados)

## Hey there 👋

A ideia desse case é **simular um problema real** e ver como você chega na solução. Não estamos atrás da resposta perfeita — queremos acompanhar seu **raciocínio**, as **decisões** que você toma e **como você usa a IA** pra acelerar (ou não) cada etapa.

O problema: o time de marketing recebe leads de uma fonte de dados e eles chegam **bagunçados** — campos faltando, formatos inconsistentes, emails inválidos, duplicatas. Sua missão é **construir uma ferramenta que recebe o arquivo bruto e devolve uma lista pronta pro CRM**.

Pode pensar em voz alta, errar, voltar atrás e perguntar. É assim que a gente trabalha de verdade. Boa sorte ✌️

## O que tem nesse repo

| Arquivo | O que é |
| --- | --- |
| [`case.md`](case.md) | 📄 O enunciado completo — contexto, etapas, schema de saída e regras. **Comece por aqui.** |
| [`leads_raw.json`](leads_raw.json) | 📥 A entrada: lista de leads crus, do jeito que chegaram (com as inconsistências de verdade). |

## Como funciona o case

**🛠️ Mão na massa** Você constrói a ferramenta que lê o `leads_raw.json` e produz a saída no schema esperado.

> **Info:** os detalhes de cada etapa, o schema de saída e as regras estão no [`case.md`](case.md). Leia com calma antes de começar.

## Entrada e saída

- **Entrada:** [`leads_raw.json`](leads_raw.json).
- **Saída:** um JSON com `leads` (prontos pro CRM), `rejected` (com o motivo) e um `summary`. O schema completo e as regras de normalização (email como identidade, dedupe, datas em ISO, telefone, `segment`) estão no [`case.md`](case.md#saída-desejada).

## Como começar

1. Leia o [`case.md`](case.md) por inteiro.
2. Abra o [`leads_raw.json`](leads_raw.json) e **investigue** — parte do case é descobrir quais são as inconsistências.
3. Escolha a stack e a ferramenta de IA que você quiser. **Você é livre 📚🧦** — o que importa é o resultado e o caminho até ele.
4. Comece pelo que entrega valor primeiro; o que não der tempo, explique como faria.

## Como funciona a sessão

Esse case é feito **ao vivo, junto com a gente** — não tem entrega pra fazer depois. A ideia é exatamente acompanhar você construindo em tempo real:

- **Como você interage com a IA** — o que pede, como itera nos prompts, como valida o que ela devolve.
- **Como você usa a IA pra desenvolver** — onde ela acelera, onde você assume o volante e por quê.
- **Seu raciocínio no caminho** — as decisões, os trade-offs e como você lida com o que dá errado.

Não precisa subir nada em repositório nem mandar depois. O que importa acontece **durante a conversa**: relaxa, pensa em voz alta e toca o problema como tocaria no dia a dia.

## Combinados

- **Pense em voz alta** — queremos acompanhar seu raciocínio e como você usa a IA.
- **Comece pelo que entrega valor**; o que não der tempo, explique como faria.
- **Pode perguntar.** Faça as perguntas que você faria num problema real antes de sair codando.
