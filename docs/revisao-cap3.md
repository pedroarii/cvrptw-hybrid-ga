# Revisão do Cap. 3 — Metodologia

Problemas encontrados em `tcc/capitulos/03-metodologia.tex` depois da conversão do PDF.
**Nada aqui foi corrigido no texto.** Cada item espera decisão ou aprovação do grupo.

Legenda: 🔴 conceitual (muda o método) · 🟡 consistência interna · ⚪ forma

| # | Tipo | Seção | Linha | Status |
|---|---|---|---|---|
| 1 | 🔴 | 3.4 (Etapa 2) | 127–155 | aberto, depende de [ADR 001](decisoes/001-janela-rigida-ou-flexivel.md) |
| 2 | 🔴 | 3.4 (Etapa 2) | 106–112 | aberto |
| 3 | 🟡 | 3.2 e 3.5 | 52, 183, 221 | aberto |
| 4 | 🟡 | 3.6 (Etapa 4) | 243–246 | aberto |
| 5 | 🟡 | 3.1 | 14–18 | aberto |
| 6 | 🟡 | 3.4 (Etapa 2) | 143–144 | aberto |
| 7 | ⚪ | vários | — | aberto |

---

## 1. Janela de tempo: rígida ou flexível?

O texto usa os dois modelos ao mesmo tempo:

- **Rígida:** a métrica "taxa de entregas não atendidas" (l. 127–133) fala em "restrições
  rígidas de capacidade e de janela de tempo".
- **Flexível:** a métrica "desvio das janelas de tempo" (l. 147–155) e o "peso da penalidade
  de desvio de janela: 50" (l. 190) só fazem sentido se o atraso for permitido com penalização.

A própria l. 148–150 admite isso ("aplicável nos casos em que o modelo permite tolerância").
Com janela rígida, o desvio é sempre zero. Com janela flexível, a taxa de não atendidos tende a
zero. Uma das métricas fica sem sentido em qualquer dos dois casos.

**Ação:** decidir no [ADR 001](decisoes/001-janela-rigida-ou-flexivel.md) e depois ajustar 3.4 e 3.5.

## 2. Desvio de janela classificado como esforço de processamento

L. 106–112: "o tempo de execução e o desvio das janelas de tempo, associados ao esforço de
processamento". O desvio é **qualidade da solução**, assim como custo e não atendidos. Só o tempo
de execução mede esforço.

**Ação:** reagrupar como "qualidade: custo, não atendidos, desvio" e "esforço: tempo".

## 3. "Análise fatorial completa" contra parâmetros fixos

- L. 52 (3.2) promete "análise fatorial completa dos parâmetros do Algoritmo Genético".
- L. 180–183 (3.5) fixa todos os parâmetros e deixa essa análise "para trabalhos futuros (item 8)".
  Não existe item 8.
- L. 220–221 (3.5): "exceto nas execuções em que este parâmetro constitui o próprio fator sob
  análise". Nenhum parâmetro é fator, então a frase é resto de uma versão anterior.

**Ação:** tirar a análise fatorial do 3.2 (ou trocar por "comparação entre os níveis do fator
algoritmo"), trocar "(item 8)" por `\ref{cap:conclusao}` ou retirar, e apagar a exceção da l. 221.

## 4. Equações "já apresentadas"

L. 243–246 (3.6) diz que as equações de custo, as restrições e a função objetivo foram "já
apresentadas nas seções anteriores deste capítulo". Não foram. Elas vão para o Cap. 4 (Modelagem).

**Ação:** trocar por "apresentadas no `\autoref{cap:modelagem}`".

## 5. As sete etapas do 3.1 não batem com as seções

L. 14–18 lista as etapas de Jain (1991) e diz que "cada etapa corresponde a uma seção própria".
Mas:

| Etapa no 3.1 | Seção que existe |
|---|---|
| execução e análise dos dados | "Etapa 7 - Análise dos dados" (sem "execução") |
| apresentação dos resultados | não existe; ficaria no Cap. 6 |
| — | "Etapa 5 - Instâncias dos testes" não aparece na lista do 3.1 |
| — | 3.10 Critérios e 3.11 Tecnologias, sem etapa |

**Ação:** alinhar a lista do 3.1 com as seções reais, ou dizer que a apresentação dos resultados
fica no `\autoref{cap:resultados}`.

## 6. Tempo de execução compara só NN e GA+LS

L. 143–144: os valores de tempo são "comparados entre a heurística do Vizinho Mais Próximo e o
Algoritmo Genético Híbrido (GA+LS)". O GA puro é nível do fator (l. 194–200) e precisa entrar
também. O custo em tempo do 2-opt é justamente o que a ablação mede.

**Ação:** incluir o GA na comparação.

## 7. Erros de forma

- [ ] L. 118: "frotal" → "frota".
- [ ] L. 66: frase quebrada, "concentram-se na comparação busca verificar".
- [ ] L. 70–74: "Objetivos da avaliação" é texto solto, não título. Em seguida a lista é
      introduzida duas vezes ("A avaliação experimental é conduzida..." e "Os dois objetivos do
      experimento são:").
- [ ] Solomon (1987) aparece como texto puro (l. 203, 250, 269, 276), então não entra nas
      Referências. A entrada `solomon1987` já está em `referencias.bib`; basta trocar por
      `\citeonline{solomon1987}`.
- [ ] L. 26: "instâncias sintéticas calibradas". As instâncias de Solomon são um benchmark
      público; "sintéticas" pode confundir a banca.

---

## Riscos experimentais (não são erro de texto, mas afetam o capítulo)

- **1500 ms tende a estourar.** 100 indivíduos × 150 gerações × 2-opt em Python deve levar
  segundos. Medir no M3; se estourar, o critério de viabilidade do 3.4 precisa ser revisto.
- **Só a C101 é fraco.** Ela é fácil e tem frota folgada; não atendidos tende a 0% para todos.
  Ver [ADR 002](decisoes/002-instancias-solomon.md).
- **Falta a métrica de número de veículos.** O padrão do Solomon compara primeiro veículos,
  depois distância. A comparação com a melhor solução conhecida fica incompleta sem ela.
