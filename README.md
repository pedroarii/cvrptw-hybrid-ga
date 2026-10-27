# cvrptw-hybrid-ga

Hybrid Genetic Algorithm (GA + 2-opt local search) for the CVRPTW, benchmarked against Nearest Neighbor on Solomon instances. Undergraduate thesis — UNIP 2026.

## Como abrir o PDF do TCC

O texto é compilado e visualizado no VS Code com a extensão **LaTeX Workshop**
(`james-yu.latex-workshop`), recomendada em `.vscode/extensions.json`. Ela precisa de uma
distribuição TeX com `latexmk` instalada.

1. Instale a extensão e recarregue o VS Code: `Ctrl+Shift+P` → **Developer: Reload Window**.
2. Abra um `.tex` do projeto, por exemplo `tcc/main.tex`.
3. Abra o PDF com `Ctrl+Alt+V`, pelo ícone **View LaTeX PDF** no canto superior direito do
   editor ou pela barra lateral (ícone **TeX** → **View LaTeX PDF**).

O PDF abre numa aba do VS Code. Arraste-a para o lado para ver o texto e o PDF juntos.

### No dia a dia

| Ação | Como |
|---|---|
| Compilar | Salvar o `.tex` (`Ctrl+S`); o PDF aberto se atualiza sozinho. Manualmente: `Ctrl+Alt+B`. |
| Ir do código para o PDF | Cursor na linha do `.tex` e `Ctrl+Alt+J`. |
| Ir do PDF para o código | `Ctrl+clique` no trecho do PDF. |
| Ver erros | Aba **Problems** (`Ctrl+Shift+M`); log completo em **TeX** → **View LaTeX compiler log**. |

Sem o VS Code, o PDF pode ser gerado pelo terminal:

```bash
cd tcc && latexmk main.tex    # gera tcc/build/main.pdf
```

### Outros PDFs (como `docs/original/`)

O LaTeX Workshop costuma abrir PDFs avulsos ao clicar no arquivo. Se não abrir:

- botão direito no arquivo → **Reveal in File Explorer** e abrir no leitor do sistema; ou
- instalar a extensão **vscode-pdf** (`tomoki1207.pdf`). No WSL, use **Install Locally**, porque
  ela só roda no lado Windows do VS Code.
