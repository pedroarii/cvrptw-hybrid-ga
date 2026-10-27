# 001 — Janela de tempo rígida ou flexível

- **Status:** decidido (opção C), pendente de validação do grupo
- **Data:** 2026-10-27
- **Decisores:** Rafael (com o orientador)

## Contexto

O Cap. 3 define métricas que pressupõem modelos diferentes (ver
[revisão do Cap. 3, item 1](../revisao-cap3.md)).
A decisão afeta o avaliador de soluções (M1), a função objetivo do AG e as métricas.

## Opções

**A. Rígida.** Chegar depois de `l_i` é inviável; o cliente fica sem atendimento ou exige outro
veículo.
- Métrica "não atendidos" faz sentido; "desvio" é sempre 0 e sai.
- O peso de penalidade 50 sai do texto ou vira penalidade de inviabilidade durante a busca.
- Comparável direto com a melhor solução conhecida do Solomon, que usa janela rígida.

**B. Flexível.** Pode atrasar; o atraso é penalizado na função objetivo com peso 50.
- Métrica "desvio" faz sentido; "não atendidos" tende a 0 e perde poder de discriminação.
- Não é comparável com a literatura do Solomon sem ressalva.

**C. Rígida na solução final, flexível durante a busca.** O AG aceita indivíduos com atraso
penalizado (peso 50) para explorar melhor o espaço, mas só soluções sem atraso são reportadas.
- É a prática comum em AGs para VRPTW.
- Mantém "não atendidos" e a comparação com a literatura; "desvio" vira métrica de diagnóstico
  da busca, não de qualidade final.

## Decisão

**Opção C**, decidida em 2026-10-27. Falta o orientador validar.

- Durante a busca, o atraso é permitido e penalizado na função de aptidão com peso 50.
- Na solução final reportada, a janela é rígida. Todo cliente atendido após `l_i` conta como
  não atendido.
- O desvio acumulado é medido na melhor solução da busca, antes dessa viabilização. É indicador
  da busca, não de qualidade final. No NN ele é nulo por construção.

## Consequências

- **Texto:** o Cap. 3 foi ajustado no 3.4 (agrupamento das métricas, parágrafo novo sobre o
  tratamento das janelas, alíneas "não atendidos" e "desvio") e no 3.5 (peso 50 descrito como
  penalidade da função de aptidão durante a busca). O Cap. 4 precisa formalizar a função de
  aptidão penalizada e o passo de viabilização.
- **Análise (3.8 e 3.9):** a frase "tolerância máxima de 15 minutos" saiu do 3.8 (Rafael
  confirmou o modelo C puro, sem tolerância). No 3.9, o desvio é comparado só entre GA e GA+LS
  (no NN é nulo por construção), o que reduz a correção de Holm para 10 comparações. O custo é
  sempre lido junto com a taxa de não atendidos, porque retirar clientes atrasados encurta a rota.
- **Avaliador (M1):** devolve custo, atraso acumulado, clientes atrasados e violação de
  capacidade separadamente. A fitness combina esses valores com o peso; a viabilização remove os
  clientes atrasados e os conta como não atendidos. Os testes cobrem os dois caminhos.
- **Comparação externa:** a solução final é comparável às melhores soluções conhecidas do
  Solomon, que usam janela rígida.
