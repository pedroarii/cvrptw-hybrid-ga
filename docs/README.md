# docs/

Material de apoio ao TCC. Nada daqui entra no PDF; o texto fica em [`../tcc/`](../tcc/).

```
docs/
├── original/         # PDF de onde o texto LaTeX foi convertido (referência, não editar)
├── decisoes/         # registros de decisão (ADR): um .md por decisão, numerados
├── reunioes/         # atas com o orientador e do grupo: AAAA-MM-DD.md
└── revisao-cap3.md   # problemas apontados no Cap. 3, aguardando o grupo
```

## Decisões (`decisoes/`)

Cada arquivo registra uma escolha que a banca pode questionar: contexto, opções, decisão e
consequências. Nome: `NNN-titulo-curto.md`. Status: `em aberto`, `decidido` ou `substituído
por NNN`. Uma decisão tomada não se apaga; se mudar, cria-se outra que a substitui.

| # | Decisão | Status |
|---|---|---|
| [001](decisoes/001-janela-rigida-ou-flexivel.md) | Janela de tempo rígida ou flexível | decidido (C), validar com o grupo |
| [002](decisoes/002-instancias-solomon.md) | Quais instâncias de Solomon usar | em aberto |
| [003](decisoes/003-capacidade-rigida.md) | Capacidade rígida, garantida por construção | decidido |

## Atas (`reunioes/`)

Uma por reunião, curta: presentes, o que foi discutido, o que ficou decidido e quem faz o quê.
Pedidos do orientador entram sempre aqui.

## Artigos

PDFs de artigos **não** são versionados (direitos autorais e tamanho). Cite pelo
`tcc/referencias.bib`, com DOI ou URL.
