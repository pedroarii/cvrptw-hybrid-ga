# CLAUDE.md — cvrptw-hybrid-ga

Contexto para o Claude Code neste repositório. Leia antes de qualquer tarefa.

## O projeto

TCC de Ciência da Computação (UNIP Brasília, 2026): **"Algoritmo Genético Híbrido para o CVRPTW em Logística Urbana de Última Milha"**.

- **Autores:** Eduardo Gabriel de Sales Rodrigues, Esther Chen, Rafael Silva dos Santos (Fael).
- **Orientador:** Prof. Me. Fabricio Rodrigues Freire.
- **Quem está trabalhando aqui:** Pedro, dev fullstack (TS/Node/React/Java), que entrou para ajudar o Fael. Ele fala português, prefere comunicação direta e avaliação honesta, sem rodeios.

**Pergunta central:** um Algoritmo Genético com busca local 2-opt (GA+LS) gera rotas melhores que a heurística gulosa do Vizinho Mais Próximo (NN) para o CVRPTW, sem passar de 1500 ms por instância?

O repositório tem duas partes:

1. **Texto do TCC** em LaTeX (abnTeX2), na pasta `tcc/`.
2. **Código Python** do experimento (DEAP). Ainda não começou.

## Conceitos-chave

| Termo | Significado |
|---|---|
| CVRPTW | Roteamento de veículos com capacidade e janelas de tempo. É NP-difícil. |
| NN | Vizinho Mais Próximo, a heurística gulosa usada como baseline. |
| GA | Algoritmo Genético puro (sem busca local). Serve de ablação. |
| GA+LS | GA híbrido com busca local 2-opt. É a proposta do trabalho. |
| Solomon (1987) | Benchmark de VRPTW. Usa-se a instância **C101**: 100 clientes, 25 veículos, capacidade 200, clientes agrupados, janelas amplas. |

## Desenho experimental (Cap. 3 do texto, baseado em Jain, 1991)

- **Fator primário:** o algoritmo, com três níveis na prática: NN, GA e GA+LS.
- **Parâmetros fixos do AG:** população 100, 150 gerações, crossover 0,8, mutação 0,1, peso da penalidade de janela 50 e 2-opt ativo.
- **Métricas:**
  - custo total (distância);
  - taxa de entregas não atendidas;
  - tempo de execução (ms: média, desvio e pior caso);
  - desvio acumulado das janelas.
- **Repetições:** 30 execuções independentes por configuração, com seed variada a cada uma.
- **Fatores fixos:** Python + DEAP, mesmo hardware, critério de parada por número de gerações.
- **Comparação externa:** melhor solução conhecida da C101 na literatura.
- **Estatística prevista:** descritivas, intervalos de confiança e testes não-paramétricos.

## Estado atual

O texto foi convertido de um PDF para LaTeX, de forma fiel ao original:

- **Escrito:** só o Cap. 3 (Metodologia), seções 3.1 a 3.7.
- **Vazio:** seções 3.8 a 3.11, que estão marcadas com `% TODO`.
- **Placeholders:** Introdução, Fundamentação, Cap. 4 a 7, Resumo e Abstract.

**Próxima tarefa combinada:** escrever as seções 3.8 (Desenho do experimento), 3.9 (Análise dos dados), 3.10 (Critérios e Avaliação da Hipótese) e 3.11 (Tecnologias utilizadas).

### Problemas conhecidos no Cap. 3 (ainda não corrigidos)

1. **Janela de tempo rígida ou flexível?** A conclusão e a métrica de "não atendidos" dizem que é rígida. A métrica de desvio e o peso de penalidade 50 pressupõem que é flexível. Isso precisa ser decidido com o grupo.
2. **O 3.4 classifica o "desvio de janela" como esforço de processamento.** Está errado: o desvio é qualidade da solução. Só o tempo de execução mede esforço.
3. **O 3.2 promete "análise fatorial completa dos parâmetros do AG", mas o 3.5 fixa os parâmetros.** O 3.5 ainda cita um "item 8" que não existe e tem a frase "exceto nas execuções em que este parâmetro constitui o próprio fator".
4. **O 3.6 diz que as equações de custo e a função objetivo "já foram apresentadas" no capítulo.** Não foram; elas vão para o Cap. 4.
5. **As 7 etapas listadas no 3.1 não batem com a numeração das seções.**
6. **Erros de forma:**
   - "frotal" no 3.4 (a);
   - frase quebrada no 3.3 ("concentram-se na comparação busca verificar");
   - introdução da lista de objetivos duplicada no 3.3;
   - Solomon (1987) é citado mas não aparece nas Referências.

### Riscos experimentais

- **O limite de 1500 ms provavelmente estoura.** Com população 100 × 150 gerações × 2-opt em Python, o tempo tende a ficar na casa dos segundos. Medir cedo.
- **Usar só a C101 é fraco.** Ela é fácil e tem frota folgada, então a taxa de não atendidos tende a 0% para todos os algoritmos. Considerar R101/RC101.
- **Falta a métrica de nº de veículos.** O padrão do Solomon compara primeiro veículos, depois distância.

## Milestones planejados

| Milestone | Escopo |
|---|---|
| M1 Fundação | Estrutura do projeto, parser Solomon, modelo de dados, matriz de distâncias, avaliador de soluções com testes, decisão janela rígida/flexível. |
| M2 Baseline | Vizinho Mais Próximo e medição de tempo. |
| M3 AG puro | Representação (sugerido giant tour + split), operadores, DEAP, seed. Inclui um spike de tempo. |
| M4 GA+LS | 2-opt, flag liga/desliga, profiling. |
| M5 Experimentos | Runner CLI, CSV bruto, execução de 3 algoritmos × 30 seeds. |
| M6 Análise | Estatística, gráficos, gap para a melhor solução conhecida. |
| M7 Escrita | Em paralelo com os outros. |
| M8 Entrega e defesa | Fechamento e banca. |

## Texto do TCC — `tcc/`

```
tcc/
├── main.tex            # dados do trabalho, pacotes, ordem dos capítulos
├── referencias.bib     # BibTeX (abntex2cite, estilo alf)
├── pretextual/         # capa, folha-aprovacao, resumo, abstract
├── capitulos/          # 01-introducao ... 07-conclusao (03-metodologia é o principal)
├── apendices/          # material dos autores
├── anexos/             # material de terceiros
├── figuras/
│   ├── estaticas/      # logo, diagramas à mão
│   └── geradas/        # só scripts de análise escrevem aqui
├── tabelas/geradas/    # .tex gerados pela análise
└── .latexmkrc          # saída em tcc/build/
```

## Apoio — `docs/`

Não entra no PDF.

- `original/`: o PDF de onde o LaTeX foi convertido.
- `decisoes/`: ADRs numerados (001 janela rígida/flexível, 002 instâncias). Estão em aberto.
- `reunioes/`: atas, uma por arquivo (`AAAA-MM-DD.md`).
- `revisao-cap3.md`: os problemas do Cap. 3 com número de linha, aguardando o grupo.

Ao resolver um problema do Cap. 3, atualize o status em `docs/revisao-cap3.md`. Ao tomar uma
decisão, preencha o ADR correspondente.

**Compilar:**

```bash
cd tcc && latexmk main.tex    # gera build/main.pdf
```

O PDF deve ter 19 páginas no estado atual. Depois de editar, compile e verifique se não há erros nem referências indefinidas.

**Convenções do LaTeX:**

- Títulos de capítulo em MAIÚSCULAS no fonte, por exemplo `\chapter{METODOLOGIA}`. Seções seguem o padrão "Etapa N - Título".
- Citações: `\citeonline{jain1991}` produz "Jain (1991)"; `\cite{gil2022}` produz "(GIL, 2022)". Novas referências vão em `referencias.bib`.
- Referências cruzadas sempre com `\label`/`\ref`/`\autoref`, nunca com o número escrito à mão. Os labels existentes são `sec:delineamento`, `sec:natureza` e `sec:etapa1` a `sec:etapa7`, `sec:criterios`, `sec:tecnologias`, `cap:*`.
- Listas a), b), c) usam o ambiente `alineas`; tabelas usam `booktabs`; termos em inglês vão em `\textit{}`.
- **Não reescreva** trechos que não foram pedidos. O texto é dos autores. Aponte problemas, mas só corrija quando for solicitado.

## Código (quando começar)

- Python + DEAP, com testes. O avaliador de soluções é a peça mais crítica e precisa de testes unitários.
- Pré-calcular a matriz de distâncias.
- Toda execução estocástica deve receber uma seed explícita.
- Resultados brutos em CSV, uma linha por execução.
- O tempo de execução é medido do recebimento da instância até a solução final, em ms.
