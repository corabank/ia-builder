# Case — Organizador de lançamentos financeiros

> Enunciado entregue à pessoa candidata no início do case. Use a ferramenta de IA que você preferir.

## Contexto

Todo mês o time financeiro junta as movimentações da empresa para fechar o caixa. Elas podem vir de **três lugares diferentes** (o extrato do banco, o sistema financeiro e uma planilha preenchida à mão), e por isso chegam **despadronizadas**: valores escritos de jeitos diferentes, datas em vários formatos, lançamentos repetidos, campos faltando.

Antes de usar esses dados no fechamento, alguém precisa limpar e conferir cada lançamento.

Sua tarefa é **construir uma automação que recebe o arquivo bruto, despadronizado, e devolve uma lista de lançamentos pronta para o fechamento**.

## Mão na massa

A partir daqui é a construção da automação descrita acima.

## Entrada

O arquivo [`transacoes_raw.json`](transacoes_raw.json): uma lista de lançamentos crus, do jeito que chegaram. Espere inconsistências de verdade (você vai descobrir quais ao olhar).

## Saída desejada

Um JSON com **dois grupos** e um **resumo**:

```jsonc
{
  "transactions": [
    {
      "id": "string",                // maiúsculo, sem espaços (ex.: "TX-1001"); é a identidade do lançamento
      "date": "string | null",       // data no formato ISO YYYY-MM-DD
      "description": "string | null",
      "amount": 0.00,                // número positivo, com 2 casas decimais
      "direction": "in | out",       // in = entrou dinheiro · out = saiu dinheiro
      "document": "string | null",   // CPF ou CNPJ só com números; null se ausente ou inválido
      "source": "string | null"
    }
  ],
  "rejected": [
    { "reason": "string", "raw": { } }   // lançamentos que não dá para aproveitar, com o motivo
  ],
  "summary": {
    "received": 0,
    "valid": 0,
    "duplicates_removed": 0,
    "rejected": 0,
    "total_in": 0.00,                // soma dos valores que entraram
    "total_out": 0.00                // soma dos valores que saíram
  }
}
```

## Regras

1. **O `id` é a identidade do lançamento.** Padronize. Sem `id`, não dá para conferir: vai para `rejected`.
2. **O mesmo lançamento pode aparecer em mais de uma fonte.** Ele deve entrar **uma vez só** na lista.
3. **Valor**: a entrada mistura formatos (`1.250,00`, `780.00`, `R$ 640`…). Na saída, é um número com 2 casas decimais. Valor que não é número vai para `rejected`.
4. **Normalize as datas**: a entrada tem vários formatos.
5. O resultado tem que **bater com o schema** acima, e o `summary` tem que **bater com a lista**.

## Combinados

- Pense em voz alta: queremos acompanhar seu raciocínio e como você usa a IA.
- Comece pelo que entrega valor; o que não der tempo, explique como faria.
- Pode perguntar. Faça as perguntas que você faria num problema real antes de sair construindo.

## Glossário

**Lançamento**: cada movimentação de dinheiro registrada (um pagamento, um recebimento, uma tarifa). É uma linha do arquivo.
**Fechamento**: o momento, geralmente mensal, em que o financeiro confere todas as movimentações do período para saber quanto entrou, quanto saiu e se os números batem.
**Estorno**: a devolução de um valor que já tinha sido pago ou cobrado.
**ISO (YYYY-MM-DD)**: um jeito padrão de escrever datas (ano-mês-dia), por exemplo `2026-09-01`. Sistemas preferem esse formato porque ele não é ambíguo.
