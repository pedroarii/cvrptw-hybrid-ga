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

## 0.4.0 (2026-10-27)

Estado apresentado ao orientador na reunião de 2026-10-27.

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
