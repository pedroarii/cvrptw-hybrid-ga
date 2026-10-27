# Texto do TCC (LaTeX / abnTeX2)

Fonte LaTeX do TCC *Algoritmo Genético Híbrido para o CVRPTW em Logística Urbana de Última Milha* (UNIP Brasília, 2026), no modelo ABNT via [abnTeX2](https://www.abntex.net.br/).

## Estrutura

```
tcc/
├── main.tex              # arquivo principal: dados do trabalho, pacotes e ordem dos capítulos
├── referencias.bib       # referências (BibTeX, estilo ABNT)
├── pretextual/           # capa, folha de aprovação, resumo, abstract
├── capitulos/            # um arquivo por capítulo (01-introducao ... 07-conclusao)
├── apendices/            # material dos autores (pseudocódigo, tabelas completas)
├── anexos/               # material de terceiros (ABNT distingue de apêndice)
├── figuras/
│   ├── estaticas/        # logo, diagramas feitos à mão
│   └── geradas/          # saída dos scripts de análise; não editar à mão
├── tabelas/
│   └── geradas/          # tabelas .tex geradas pela análise, entram com \input
└── .latexmkrc            # configuração de compilação (saída em build/)
```

As pastas `geradas/` são escritas só pelos scripts de análise do experimento. Assim o Cap. 6 se
atualiza quando os experimentos rodam de novo, sem copiar números à mão. Material de apoio que não
entra no PDF (decisões, atas, revisões) fica em [`../docs/`](../docs/).

Para editar um capítulo, abra o arquivo correspondente em `capitulos/`. Título, autores, orientador e data ficam no topo de `main.tex`.

## Como compilar

### VS Code (recomendado)

1. Instale uma distribuição LaTeX:
   - **Windows:** [MiKTeX](https://miktex.org/download) (instala pacotes como o abnTeX2 automaticamente) — também é preciso ter Perl para o `latexmk` ([Strawberry Perl](https://strawberryperl.com/));
   - **Linux:** `sudo apt install texlive-latex-extra texlive-publishers texlive-lang-portuguese latexmk`;
   - **macOS:** [MacTeX](https://www.tug.org/mactex/).
2. Instale a extensão **LaTeX Workshop** (o VS Code sugere ao abrir o repositório).
3. Abra `tcc/main.tex` e salve (`Ctrl+S`): o PDF é gerado em `tcc/build/main.pdf` e abre numa aba ao lado.

### Terminal

```bash
cd tcc
latexmk main.tex      # gera build/main.pdf
latexmk -c            # limpa os auxiliares
```

## Convenções

- Citações: `\citeonline{jain1991}` → "Jain (1991)"; `\cite{gil2022}` → "(GIL, 2022)". Novas referências entram em `referencias.bib`.
- Referências cruzadas: use `\label{...}` e `\ref{...}` / `\autoref{...}` em vez de escrever o número da seção à mão.
- Alíneas a), b), c): ambiente `alineas`.
- Tabelas: `booktabs` (`\toprule`, `\midrule`, `\bottomrule`).
- O PDF gerado (`build/`) não é versionado.
