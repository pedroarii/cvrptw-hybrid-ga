# 001 — Janela de tempo rígida ou flexível

- **Status:** em aberto
- **Data:** 2026-10-27
- **Decisores:** Eduardo, Esther, Rafael (com o orientador)

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

_A preencher._

## Consequências

_A preencher: seções do Cap. 3 a ajustar, impacto no avaliador e nos testes._
