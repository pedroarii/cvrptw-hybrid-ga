# Revisão do Cap. 3 — Metodologia

Problemas encontrados em `tcc/capitulos/03-metodologia.tex` depois da conversão do PDF.
Os itens 1 a 7 foram corrigidos em 2026-10-27 (ver "Correções aplicadas" no fim). Os números de
linha abaixo se referem à versão **anterior** à correção. O grupo deve revisar o texto novo.

Legenda: 🔴 conceitual (muda o método) · 🟡 consistência interna · ⚪ forma

| # | Tipo | Seção | Linha | Status |
|---|---|---|---|---|
| 1 | 🔴 | 3.4 (Etapa 2) | 127–155 | corrigido, modelo C do [ADR 001](decisoes/001-janela-rigida-ou-flexivel.md) |
| 2 | 🔴 | 3.4 (Etapa 2) | 106–112 | corrigido |
| 3 | 🟡 | 3.2 e 3.5 | 52, 183, 221 | corrigido |
| 4 | 🟡 | 3.6 (Etapa 4) | 243–246 | corrigido |
| 5 | 🟡 | 3.1 | 14–18 | corrigido |
| 6 | 🟡 | 3.4 (Etapa 2) | 143–144 | corrigido |
| 7 | ⚪ | vários | — | corrigido (um subitem mantido, ver abaixo) |
| 8 | 🟡 | 3.5 (a) | 172–177 | corrigido |
| 9 | 🟡 | 3.5 (b) | 190 | corrigido: valor declarado empírico |
| 10 | 🟡 | 3.4 e 3.5 (b) | — | corrigido: [ADR 003](decisoes/003-capacidade-rigida.md) |

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

## 8. Fator primário com "dois níveis"

L. 172–177 (3.5 a) diz que o fator algoritmo tem dois níveis, NN e GA+LS. O 3.5 (b) introduz o GA
puro como "nível adicional de controle", e o 3.4 passou a comparar os três no tempo de execução.
Na prática o fator tem três níveis.

**Ação sugerida:** dizer em (a) que o fator tem três níveis (NN, GA e GA+LS) e que o GA serve como
ablação da busca local. O (b) passa a só justificar o terceiro nível.

**Resolvido (2026-10-27):** o 3.5 (a) passou a listar três níveis, com o GA como controle da
hibridização. O (b) ficou como estava.

## 9. Peso 50 sem justificativa

O 3.5 (b) fixa o peso da penalidade de atraso em 50, mas não diz de onde veio o valor. O peso é a
"taxa de câmbio" entre atraso e distância: na aptidão `distância + 50 × atraso`, uma unidade de
atraso custa o mesmo que 50 de distância. Peso pequeno faz o AG preferir rotas curtas e atrasadas;
peso enorme equivale a descartar as soluções inviáveis. A banca tende a perguntar "por que 50?".

**Ação sugerida (escolher uma):**
- citar um trabalho que use um peso nessa faixa;
- fazer um teste piloto com alguns valores (por exemplo 10, 50 e 200) e relatar o resultado;
- declarar que o valor foi definido empiricamente e deixar a análise de sensibilidade para
  trabalhos futuros, como já se faz com os outros parâmetros.

**Resolvido (2026-10-27):** a pesquisa não achou fonte verificável para o 50. A pista mais
próxima é o GIDEON de Thangiah (AG para VRPTW dos anos 1990), cujos pesos de penalidade foram
"derivados empiricamente" e incluem um valor 50. Mas os trechos encontrados não deixam claro a
que restrição esse 50 se aplica, e o texto completo não estava acessível. Por decisão do grupo,
o 3.5 (b) passou a declarar o valor como empírico, com a calibração para trabalhos futuros. Se
alguém tiver acesso ao texto do Thangiah e confirmar o peso de atraso, a citação pode entrar.

## 10. Tratamento da capacidade indefinido

O texto define como a janela de tempo é tratada (modelo C), mas não diz o que acontece quando uma
rota excede a capacidade do veículo durante a busca: se o excesso também é penalizado na aptidão
ou se é proibido (por exemplo, pelo *split* do *giant tour*, que já abre uma rota nova ao lotar).

**Ação sugerida:** decidir com o grupo e registrar no 3.4/3.5 e no Cap. 4. A escolha afeta o
avaliador (M1). Se for proibido por construção, basta uma frase dizendo isso.

**Resolvido (2026-10-27):** capacidade rígida, garantida por construção ([ADR 003](decisoes/003-capacidade-rigida.md)).
O 3.4 ganhou uma frase dizendo isso logo após o tratamento das janelas.

---

## Correções aplicadas (2026-10-27)

| # | O que mudou |
|---|---|
| 1 | Modelo C: parágrafo novo no 3.4 sobre o tratamento das janelas. "Não atendidos" inclui os clientes atrasados; "desvio" foi redefinido como indicador da busca, nulo no NN; o peso 50 é descrito como penalidade da função de aptidão durante a busca. |
| 2 | As métricas ficaram em três grupos: qualidade (custo, não atendidos), indicador de busca (desvio) e esforço (tempo). |
| 3 | Saíram a "análise fatorial completa" do 3.2, o "(item 8)" e a exceção do critério de parada. |
| 4 | "já apresentadas nas seções anteriores" → "apresentadas no `\autoref{cap:modelagem}`". |
| 5 | A lista do 3.1 passou a seguir as seções reais (com "seleção das instâncias de teste"), cita 3.10 e 3.11 e remete a apresentação dos resultados ao `\autoref{cap:resultados}`. |
| 6 | O GA entrou na comparação do tempo de execução. |
| 7 | "frotal" virou "frota"; a frase do 3.3 foi refeita; o título solto e a introdução duplicada saíram; "Solomon (1987)" virou `\citeonline{solomon1987}` nos 5 lugares; "instâncias sintéticas calibradas" (l. 26) virou "instâncias padronizadas do benchmark". Ficou "sintéticas e padronizadas" na l. 249, porque está correto: as instâncias foram geradas por Solomon. |

Compilado: 20 páginas, sem erros nem referências indefinidas; Solomon (1987) aparece nas Referências.

---

## Riscos experimentais (não são erro de texto, mas afetam o capítulo)

- **1500 ms tende a estourar. Status: pendente (medir no spike de tempo do M3).** 100
  indivíduos × 150 gerações × 2-opt em Python deve levar segundos. Desde 2026-10-27 o critério
  é o **pior caso** das 30 execuções (3.4 e 3.10), o que deixa o limite mais difícil de cumprir.
  Se estourar, o grupo decide entre otimizar a implementação, reduzir população/gerações ou
  rever o limite, e o 3.4, o 3.5 e o 3.10 precisam ser ajustados.
- **Só a C101 é fraco.** Ela é fácil e tem frota folgada; não atendidos tende a 0% para todos.
  Ver [ADR 002](decisoes/002-instancias-solomon.md).
- **Falta a métrica de número de veículos.** O padrão do Solomon compara primeiro veículos,
  depois distância. A comparação com a melhor solução conhecida fica incompleta sem ela.
