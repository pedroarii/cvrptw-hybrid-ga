# Histórico de versões do TCC

A versão fica em `tcc/main.tex` (`\versaotcc`) e segue o formato `MAIOR.MENOR.CORREÇÃO`:

| Parte | Quando sobe | Exemplo |
|---|---|---|
| MAIOR | Entrega oficial | `1.0.0` = versão entregue à banca |
| MENOR | Conteúdo novo ou mudança de método | capítulo ou seção escrita, decisão de método |
| CORREÇÃO | Ajuste sem conteúdo novo | erro de digitação, formatação ABNT, referência |

Versões `0.x.y` são de desenvolvimento. A versão sobe quando um conjunto de mudanças vai ser
apresentado ou entregue, não a cada commit. Para achar o commit de uma versão:
`git log --oneline -- CHANGELOG.md`.

Ao subir a versão:

1. altere `\versaotcc` em `tcc/main.tex`;
2. registre a versão aqui, no topo;
3. na entrega oficial, troque `\rascunhotrue` por `\rascunhofalse` para tirar a versão do rodapé.

---

## 0.5.0 (2026-10-27)

Estado levado ao orientador na reunião. Aprovado por Rafael e Pedro; as próximas mudanças
dependem da opinião do orientador.

- Cap. 4 (Modelagem do Algoritmo Genético Híbrido) escrito em rascunho, seções 4.1 a 4.7:
  formulação de três índices, *giant tour* + *Split*, função de aptidão penalizada, operadores
  genéticos, busca local 2-opt, viabilização da solução final e fluxo do algoritmo (Quadro 4.1).
- Ambiente `quadro` (ABNT) definido no preâmbulo.
- Sete referências novas: Cordeau et al. (2002), Prins (2004), Holland (1975),
  Goldberg (1989), Davis (1985), Moscato (1989) e Croes (1958).
- Ata e roteiro da reunião atualizados com o Cap. 4 e a quarta pergunta ao orientador.

## 0.4.0 (2026-10-27)

- Seção 3.11 (Tecnologias utilizadas) escrita; o hardware do experimento segue a definir.
- Ata e roteiro da reunião em `docs/reunioes/`.
- Rafael Silva dos Santos como único autor.
- Versão do texto no rodapé (rascunho) e nos metadados do PDF.

## 0.3.0 (2026-10-27)

- Seções 3.8 a 3.10 escritas: desenho do experimento, análise dos dados e critérios de avaliação
  da hipótese.

## 0.2.0 (2026-10-27)

- Inconsistências do Cap. 3 corrigidas (ver `docs/revisao-cap3.md`).
- Janela de tempo pelo modelo C (ADR 001) e capacidade rígida por construção (ADR 003).

## 0.1.0 (2026-10-27)

- Texto convertido do PDF original para LaTeX (abnTeX2), de forma fiel.
