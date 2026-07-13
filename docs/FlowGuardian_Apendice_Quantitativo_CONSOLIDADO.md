# FlowGuardian — Apêndice Quantitativo (Núcleo Determinístico)

**Versão:** 1.0 — consolidada
**Status:** Para validação antes do fatiamento nos comandos
**Função:** fixar todo parâmetro que hoje seria decidido pelo modelo em tempo de execução, para que qualquer LLM produza os mesmos números sobre os mesmos dados.

Este apêndice é a fonte única dos parâmetros de cálculo. Os três comandos v3.0 herdam dele os recortes relevantes a cada módulo. Onde uma regra dependeu de decisão registrada, a decisão está referenciada (D01–D10).

---

## 1. Escopo do Universo da Análise

### 1.1 Tipos de item
Card = Story, Bug, Tarefa, Dívida Técnica ou equivalente.

### 1.2 Subtarefas — excluídas (D01)
Subtarefas não entram no universo nem em nenhuma métrica. Se os dados de entrada as contiverem, devem ser removidas antes da análise e a remoção registrada.

### 1.3 Cancelados (D02)
- Permanecem no universo (evidência de retrabalho/desperdício).
- Fora do Throughput.
- Fora da Taxa de Conclusão — categoria própria: Planejado / Concluído / Cancelado.
- Subdivisão obrigatória:
  - **Cancelado após início efetivo** (§2.2): desperdício, com tempo investido quantificado (dias úteis de Desenvolvimento até o cancelamento).
  - **Cancelado antes do início efetivo**: correção de escopo, sem desperdício.

---

## 2. Definições de Status

O critério é sempre o status do item, nunca a coluna visual do board. A coluna "ITENS CONCLUÍDOS" do board agrupa status distintos e não pode ser usada como critério (D03).

### 2.1 Concluído (D03)
Concluído = exclusivamente o status **CONCLUÍDO**.
Marco de conclusão = data da transição para CONCLUÍDO no histórico.
Não são conclusão: Pronto para Homologação, Homologação, Aguardando Teste de Regressão, Aguardando Deploy. São fila de espera. Aguardando Deploy nunca é entrega, sem exceção.
Cancelado = encerramento sem entrega (D02).

### 2.2 Início efetivo — base do Cycle Time (D04)
Início efetivo = **primeira** transição para o status **DESENVOLVIMENTO**.
Em reabertura/retorno de fluxo, vale a primeira entrada em Desenvolvimento (o Cycle Time captura os retornos, não os oculta).
Card que chegou a CONCLUÍDO sem transição registrada para DESENVOLVIMENTO → Cycle Time **Não calculável** para esse card, com a razão. Proibida aproximação por outro status.

### 2.3 Data de referência do Aging (D05)
Data de referência = data da **última transição de status**.
Aplicável apenas a cards abertos (não concluídos).
Comentário ou edição de campo não conta como referência — só transição de status.

---

## 3. Calendário Oficial

### 3.1 Regra base
Todas as métricas temporais em **dias úteis**. Fuso `America/Sao_Paulo`. Proibido dias corridos onde a métrica define dias úteis.

### 3.2 Dias não-úteis (D06, D07)
Sábados, domingos, feriados nacionais (lista federal) e 25/01 (São Paulo Capital).
Regra literal: pontos facultativos contam como dias úteis. **Carnaval, Quarta-feira de Cinzas e Corpus Christi são dias úteis.** Sexta-feira Santa é dia não-útil (feriado nacional).

### 3.3 Lista de datas — não-úteis (excluindo sábados e domingos)

**2025**
- 01/01 (qua) — Confraternização Universal
- 18/04 (sex) — Sexta-feira Santa
- 21/04 (seg) — Tiradentes
- 01/05 (qui) — Dia do Trabalho
- 25/01 (sáb, já fim de semana) — Aniversário de São Paulo
- 07/09 (dom, já fim de semana) — Independência
- 12/10 (dom, já fim de semana) — Nossa Senhora Aparecida
- 02/11 (dom, já fim de semana) — Finados
- 15/11 (sáb, já fim de semana) — Proclamação da República
- 20/11 (qui) — Consciência Negra
- 25/12 (qui) — Natal

**2026**
- 01/01 (qui) — Confraternização Universal
- 25/01 (dom, já fim de semana) — Aniversário de São Paulo (não transferido; sem efeito em dias úteis)
- 03/04 (sex) — Sexta-feira Santa
- 21/04 (ter) — Tiradentes
- 01/05 (sex) — Dia do Trabalho
- 07/09 (seg) — Independência
- 12/10 (seg) — Nossa Senhora Aparecida
- 02/11 (seg) — Finados
- 15/11 (dom, já fim de semana) — Proclamação da República
- 20/11 (sex) — Consciência Negra
- 25/12 (sex) — Natal

**Regra de transferência (D07 estendida):** feriado que cai em sábado ou domingo não é transferido — dissolve-se no fim de semana e não gera dia não-útil adicional. Aplica-se a 25/01/2026 (domingo), sem efeito no cálculo.

Sexta-feira Santa calculada por algoritmo (Páscoa − 2 dias): 18/04/2025, 03/04/2026. Ambas em sexta.

---

## 4. Prioridade de Resolução de Conflito entre Fontes

Quando fontes discordam sobre o mesmo fato (doc 03 — Engine):

1. Histórico de transições
2. Campos do card
3. Comentários
4. Sprint Report

Persistindo o conflito após aplicar a ordem, registrar como limitação. Não completar por suposição.

---

## 5. Modo de Análise (D08)

Antes de calcular qualquer métrica, classificar o modo:

- **Modo sprint:** existe baseline de planejamento (escopo comprometido no início da sprint).
- **Modo período:** coorte definida por data de resolução, sem baseline de planejamento.

Discriminador: presença ou ausência de baseline. Binário e auditável.

Consequência no cálculo:
- Modo sprint: MET-05, MET-06 e MET-09 calculam normalmente.
- Modo período: MET-05, MET-06 e MET-09 = **Não aplicável** (não "Não calculável"). A Saúde da Sprint é substituída pela análise de fluxo de coorte (§5.1).

### 5.1 Coorte do modo período — definição e medidas

**Coorte = cards resolvidos dentro do período** (âncora: data de resolução). Coorte fechada e determinística: o mesmo intervalo retorna o mesmo conjunto em qualquer reexecução e qualquer modelo. Não usar "atividade no período" como âncora — depende de definir o que conta como atividade e deixa de ser reproduzível.

Não existe "entrou / aberto" nesta coorte: por construção, ela contém apenas o que foi resolvido no período. Todo card já saiu. As medidas abaixo descrevem **como o conjunto fluiu**, não balanço de entrada e saída.

Medidas obrigatórias:
- **Tempo de fluxo:** Lead Time e Cycle Time da coorte, em distribuição (mínimo, mediana, máximo), não só média. A média isolada esconde os outliers, que são o sinal.
- **Composição por tipo:** contagem por Story / Bug / Tarefa / Dívida Técnica.
- **Composição por retrabalho:** quantos cards da coorte passaram por reabertura (MET-08).
- **Composição por bloqueio:** quantos tiveram bloqueio registrado (MET-07), com a limitação de comparabilidade da §6.1 quando aplicável.
- **Throughput** do período (MET-01).

O que este modo não responde: aderência a planejamento (não há baseline) e balanço de WIP (backlog aberto ao fim do período é outra métrica e outra coorte; não forçar dentro desta).

---

## 6. Catálogo de Métricas Oficiais

Todas as temporais obedecem à Seção 3. Sem dado suficiente → **Não calculável** (nunca estimada). Sem sentido no modo → **Não aplicável** (D08).

| Código | Métrica | Fórmula | Unidade | Fonte |
|---|---|---|---|---|
| MET-01 | Throughput | cards concluídos ÷ dias úteis do período | cards/dia útil | status, data de conclusão, período |
| MET-02 | Lead Time | data de conclusão − data de criação | dias úteis | datas de criação e conclusão |
| MET-03 | Cycle Time | data de conclusão − início efetivo (§2.2) | dias úteis | histórico de transições |
| MET-04 | Aging | data da análise − última transição de status (§2.3) | dias úteis | histórico; só cards abertos |
| MET-05 | Planejado × Executado | Planejado vs Executado | cards e pontos | Sprint Report e cards; só modo sprint |
| MET-06 | Taxa de Conclusão | (Concluídos ÷ Planejados) × 100 | % | Sprint Report; só modo sprint |
| MET-07 | Bloqueios | contagem + dias úteis bloqueados (§6.1) | cards e dias úteis | cascata flag/comentário |
| MET-08 | Reaberturas | contagem de retornos de CONCLUÍDO para status anterior | cards | histórico |
| MET-09a | Cards inseridos após início da sprint | contagem | cards | histórico; só modo sprint |
| MET-09b | Cards removidos após início da sprint | contagem | cards | histórico; só modo sprint |
| MET-09c | Cards com alteração de story points após início da sprint | contagem + variação em pontos | cards e pontos | histórico; só modo sprint |
| MET-10 | Progressão do épico (portfólio) | concluídos ÷ total de cards do épico × 100 | % e quantidade | épico completo |
| MET-10b | Avanço do épico no período | concluídos no período ÷ cards do épico no universo × 100 | % e quantidade | universo |
| MET-11 | Progressão da iniciativa (portfólio) | concluídos ÷ total de cards da iniciativa × 100 | % e quantidade | iniciativa completa |
| MET-11b | Avanço da iniciativa no período | concluídos no período ÷ cards da iniciativa no universo × 100 | % e quantidade | universo |

"Concluídos" em toda métrica = só status CONCLUÍDO (D03).

### 6.1 Duração de bloqueio — cascata por card (D09)
Ordem de precedência, por card:
1. Flag de bloqueio via changelog (início = adição, fim = remoção ou data da análise) — se changelog disponível e flag usada.
2. Comentário datado de espera (início = primeiro comentário de espera, fim = comentário de encerramento ou data da análise).
3. Nenhum → duração Não calculável; card visível apenas no Aging.

Causa do bloqueio: sempre do comentário (a flag não carrega causa).
Sem `expand=changelog`: nível 1 inacessível; declarar limitação; cair para nível 2 ou 3.
Comparabilidade: boards de maturidades diferentes no mesmo relatório → declarar quais usam flag e **proibir** comparação direta de contagem/duração de bloqueios entre eles.

### 6.1.1 Mudança de escopo — três componentes separados (D11)
MET-09a, 09b e 09c são reportados **separadamente**, nunca somados. Somar mistura fenômenos incompatíveis: inserção/remoção medem instabilidade do compromisso da sprint; alteração de story points mede qualidade de estimativa. Inserção e remoção têm sinais opostos e podem se cancelar num total, escondendo churn severo.
Âncora das três: data de início da sprint (campo da sprint), não primeira transição de card.
Resumo opcional, se desejado, em duas medidas distintas — nunca uma: **churn de escopo** = inseridos + removidos; **volatilidade de estimativa** = re-estimativas.

### 6.2 Progressões de épico/iniciativa — reporte duplo (D10)
MET-10 e MET-10b (idem MET-11/11b) são **sempre reportadas juntas**, com rótulos completos, nunca abreviados como "progressão".
Avanço no período sempre calcula. Progressão de portfólio = Não calculável quando o épico/iniciativa completo não vier nas entradas.
O modelo deve ler o contraste entre as duas: avanço alto + portfólio baixo = épico no começo; avanço baixo + portfólio alto = quase pronto mas parado; avanço zero + portfólio estável = abandonado sem cancelamento formal.

---

## 7. Regra de Declaração de Ausência

- Dado insuficiente → **Não calculável**, com a razão.
- Métrica sem sentido no modo → **Não aplicável**, com a razão.
- Nunca preencher lacuna com estimativa, conhecimento externo ou suposição.

---

## Anexo — Rastreabilidade das decisões

| Decisão | Onde entra neste apêndice |
|---|---|
| D01 Subtarefas | §1.2 |
| D02 Cancelados | §1.3 |
| D03 Concluído | §2.1, §6 |
| D04 Início efetivo | §2.2 |
| D05 Aging | §2.3 |
| D06 Feriados móveis | §3.2, §3.3 |
| D07 Nacionais + municipal | §3.2, §3.3 |
| D08 Modo de análise | §5, MET-05/06 |
| D09 Duração de bloqueio | §6.1 |
| D10 Progressões | §6.2, MET-10/10b/11/11b |
| D11 Mudança de escopo | §6.1.1, MET-09a/09b/09c |
| D12 Coorte do modo período | §5.1 |
