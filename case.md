# Case — Normalizador e enriquecedor de leads

> Enunciado entregue ao candidato no início do case. Use com a ferramenta de IA que você preferir.

## Contexto

O time de marketing recebe leads de uma fonte de dados, e os dados chegam **bagunçados**: campos faltando, formatos inconsistentes, emails inválidos, duplicatas. Antes de subir esses leads pro CRM, eles precisam ser limpos, validados e classificados.

Sua tarefa é **construir uma ferramenta que recebe o arquivo bruto e produz uma lista pronta pro CRM**.

O case tem duas etapas: primeiro a gente **discute a estratégia de ingestão**, e só depois você vai pra **mão na massa** construir a ferramenta.

## Etapa 1 — Discussão: estratégia de ingestão

Antes de codar, queremos conversar sobre **como** você levaria esses dados até o destino. Aqui não tem código nem resposta única certa — queremos seu raciocínio e os trade-offs por trás de cada escolha. Pense em voz alta sobre:

- **Qual seria o destino dos dados? Por quê?** 
- **O que você usaria para a ingestão?** 
- **Como monitorar a integração de dados?** 
- **E se o destino fosse o datalake, como você organizaria os dados?**

## Etapa 2 — Mão na massa

A partir daqui é a construção da ferramenta descrita acima.

## Entrada

O arquivo [`leads_raw.json`](leads_raw.json) — uma lista de leads crus, do jeito que chegaram. Espere inconsistências de verdade (você vai descobrir quais ao olhar).

## Saída desejada

Um JSON com **dois grupos** e um **resumo**:

```jsonc
{
  "leads": [
    {
      "email": "string",          // minúsculo, sem espaços, válido — é a chave do lead
      "name": "string | null",    // limpo (sem espaços sobrando); null se ausente
      "phone": "string | null",   // normalizado de forma consistente; null se ausente/ruim
      "company": "string | null", // null se vazio/ausente
      "source": "string | null",
      "created_at": "string | null", // data normalizada para o formato ISO YYYY-MM-DD
      "segment": "hot | warm | cold | unknown"
    }
  ],
  "rejected": [
    { "reason": "string", "raw": { } }   // leads que não dá pra aproveitar, com o motivo
  ],
  "summary": {
    "received": 0,
    "valid": 0,
    "duplicates_removed": 0,
    "rejected": 0
  }
}
```

## Regras

1. **Email é a identidade do lead.** Padronize e trate o que não for válido.
2. **Normalize as datas**, a entrada tem vários formatos.
3. **Telefone**: deixe num formato consistente.
4. **`segment`** é a intenção do lead, inferida a partir da **mensagem** dele:
   - `hot` = quer comprar / urgente · `warm` = comparando / decisão futura · `cold` = só pesquisando.
   - **Sem mensagem, não há o que inferir → `unknown`** (não chute).
5. O resultado tem que **bater com o schema** acima.

## Combinados

- Pense em voz alta — queremos acompanhar seu raciocínio e como você usa a IA.
- Comece pelo que entrega valor; o que não der tempo, explique como faria.
- Pode perguntar. Faça as perguntas que você faria num problema real antes de sair codando.
