# 003 — Capacidade rígida, garantida por construção

- **Status:** decidido
- **Data:** 2026-10-27
- **Decisores:** grupo delegou ao Claude, com o prazo curto do TCC como critério

## Contexto

O [ADR 001](001-janela-rigida-ou-flexivel.md) definiu o tratamento da janela de tempo, mas o texto
não dizia o que acontece quando uma rota passa da capacidade do veículo (200 na C101). Havia duas
opções: penalizar o excesso na aptidão, como o atraso, ou proibir.

## Decisão

**Proibir por construção.** Nenhuma fase forma rota com demanda acima da capacidade:

- no AG, a decodificação do indivíduo (o *split* do *giant tour*, se essa for a representação)
  abre uma rota nova quando a próxima entrega excederia a capacidade;
- no NN, um cliente só é inserido se couber no veículo atual.

## Por quê

- Não cria um segundo peso de penalidade para justificar na banca.
- Deixa o avaliador e os testes mais simples: a capacidade vira uma checagem que nunca deveria
  falhar (útil como `assert` nos testes), não um termo da aptidão.
- É o tratamento usual com *giant tour* + *split* (Prins, 2004), a representação sugerida no M3.
- Na C101 a frota é folgada (25 veículos), então a restrição quase não limita a busca.

## Consequências

- **Texto:** frase no 3.4, logo após o tratamento das janelas. O Cap. 4 deve formalizar a
  decodificação.
- **Código:** o avaliador verifica a capacidade e falha em teste se ela for violada; a aptidão
  só penaliza o atraso.
