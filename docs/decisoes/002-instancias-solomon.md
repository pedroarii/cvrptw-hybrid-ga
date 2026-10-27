# 002 — Quais instâncias de Solomon usar

- **Status:** em aberto
- **Data:** 2026-10-27
- **Decisores:** Eduardo, Esther, Rafael (com o orientador)

## Contexto

O 3.7 (Etapa 5) usa só a C101: 100 clientes agrupados, janelas amplas, frota folgada. É a
instância mais fácil do benchmark. NN, GA e GA+LS tendem a atender todos os clientes, e a
diferença entre eles pode aparecer só no custo.

## Opções

**A. Só C101.** Escopo atual; menor tempo de execução dos experimentos.
O risco é a banca questionar a generalização.

**B. Uma por classe: C101, R101, RC101.** Clientes agrupados, aleatórios e mistos. Triplica as
execuções (3 algoritmos × 3 instâncias × 30 seeds = 270) e torna a instância um fator de fato.

**C. Classe C1 inteira (C101–C109).** Mais robusto dentro de um tipo, sem variar a distribuição
espacial.

## Decisão

_A preencher._

## Consequências

_A preencher: ajuste do 3.5 (fator instância) e do 3.7, tempo total de experimento._
