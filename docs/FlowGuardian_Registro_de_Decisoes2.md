# FlowGuardian — Registro de Decisões Metodológicas

**Tipo:** Registro de decisões (racional)
**Origem:** Sessão de revisão da metodologia, Julho/2026
**Status:** Decisões fechadas, aguardando incorporação ao apêndice quantitativo e aos comandos v3.0

Este documento registra o que foi decidido e por quê. Ele não é normativo — a regra executável vive nos comandos e no apêndice quantitativo. Aqui está o racional, para que futuras revisões não reabram decisões sem entender o motivo original.

Cada decisão indica as métricas ou o comportamento afetado, para rastreabilidade.

---

## Decisão 01 — Subtarefas

**Decidido:** Subtarefas são excluídas do universo da análise e de todas as métricas.

**Por quê:** Subtarefas não são unidades de entrega independentes. Incluí-las distorce em duas direções ao mesmo tempo: inflam contagens (Throughput, Taxa de Conclusão), porque um card com cinco subtarefas vira seis itens; e puxam as médias de tempo para baixo (Lead Time, Cycle Time), porque uma subtarefa nasce e morre dentro do ciclo do card-pai, durando horas contra os dias úteis de um card real. Misturar as duas populações produz média que não descreve nenhuma. A exclusão já era feita na coleta via JQL; a decisão promove a regra à metodologia para que o comando autocontido não dependa de a coleta ter filtrado.

**Afeta:** MET-01, MET-02, MET-03, MET-06.

**Condição de reabertura:** se algum board passar a usar subtarefa como unidade real de trabalho rastreada individualmente, a regra vira condicional por board.

---

## Decisão 02 — Itens cancelados

**Decidido:**
- Cancelados permanecem no universo da análise (evidência de retrabalho e desperdício).
- Não contam no Throughput.
- Não entram na Taxa de Conclusão; ficam como categoria própria (Planejado / Concluído / Cancelado).
- Cancelado é subdividido em: **após início efetivo** = desperdício, com tempo investido quantificado; **antes do início efetivo** = correção de escopo, sem desperdício.

**Por quê:** O denominador da Taxa de Conclusão é onde a escolha engana. Somar cancelado a "não concluído" pune a equipe por decisão que muitas vezes foi acertada — cortar escopo que deixou de fazer sentido é boa gestão, não falha de entrega. Uma sprint que planejou 13, entregou 8 e cancelou 5 conscientemente leria como 62% quando entregou 100% do que continuou fazendo sentido. Separar em três categorias preserva a evidência sem contaminar a leitura de saúde.

A subdivisão existe porque cancelamento e desperdício não são a mesma coisa. Card cancelado antes de qualquer trabalho não é desperdício, é correção de escopo cedo — cenário saudável. Card cancelado após dias em desenvolvimento é desperdício real. A distinção está no histórico (houve transição para início efetivo antes do cancelamento?). Sem a subdivisão, uma sprint que só cortou escopo cedo seria reportada como desperdício — a história oposta da que aconteceu.

**Afeta:** MET-01, MET-06. Depende da Decisão 04 (início efetivo) para a fronteira desperdício/correção.

---

## Decisão 03 — Status "concluído"

**Decidido:**
- Concluído = exclusivamente o status **CONCLUÍDO**.
- Os demais status agrupados na coluna visual "ITENS CONCLUÍDOS" (Pronto para Homologação, Homologação, Aguardando Teste de Regressão, Aguardando Deploy) são fila de espera, não conclusão, e não contam em Throughput, Lead Time ou Taxa de Conclusão.
- Cancelado = encerramento sem entrega (Decisão 02).
- Marco de conclusão = entrada no status CONCLUÍDO (data da transição no histórico).
- Regra explícita no comando: a coluna visual do board não é critério; o critério é o status.
- Aguardando Deploy não é considerado entregue em nenhum caso.

**Por quê:** O board agrupa sete status sob a coluna "ITENS CONCLUÍDOS", dos quais só CONCLUÍDO é entrega. Homologação, Aguardando Teste de Regressão, Aguardando Deploy e Pronto para Homologação são estágios de espera pós-desenvolvimento — o card está parado aguardando algo, não entregue. Um LLM olhando a coluna visual (614 + 113 + 2 + 2 tickets) conta esses estágios como entregues e infla Throughput e Taxa de Conclusão. A distinção coluna-versus-status precisa estar escrita porque é o erro mais provável de um modelo sem o aviso.

O marco em "entrada no status CONCLUÍDO", sem exigir confirmação de deploy além do status, é a escolha auditável: a data da transição existe no histórico e é reproduzível. Ancorar em deploy real traria dado que raramente está no card e viraria não auditável.

**Afeta:** MET-01, MET-02, MET-06.

---

## Decisão 04 — Início efetivo do Cycle Time

**Decidido:**
- Início efetivo = **primeira transição para o status DESENVOLVIMENTO**.
- Em caso de reabertura ou retorno de fluxo, vale a **primeira** entrada em Desenvolvimento.
- Card que chegou a CONCLUÍDO sem transição registrada para DESENVOLVIMENTO → Cycle Time **Não calculável** para esse card, com a razão. Sem aproximação.

**Por quê:** "Aberto" e "Pronto para Desenvolvimento" são fila de entrada — o trabalho não começou, o card espera ser puxado. Incluir esse tempo no Cycle Time o transformaria em Lead Time disfarçado, apagando a distinção que as duas métricas existem para manter. Cycle Time mede o tempo depois que o trabalho começou; ancorar em Desenvolvimento preserva isso, e a transição está no histórico, logo é reproduzível.

A primeira entrada (não a última) vale em reabertura porque o Cycle Time deve capturar o tempo total de execução, incluindo retornos. Ancorar na última entrada apagaria do número justamente os ciclos de retrabalho, que são o sinal mais importante que a métrica pode dar. A última entrada esconde o problema; a primeira o expõe.

Não calculável em vez de aproximação porque cair para outro status como base contaminaria a média com valor inventado, violando a proibição de estimativa.

**Afeta:** MET-03. Fecha por herança a fronteira da Decisão 02.

---

## Decisão 05 — Data de referência do Aging

**Decidido:**
- Data de referência = **data da última transição de status** (não última atualização genérica do card).
- Aplicável apenas a cards abertos (não concluídos).
- Comentário ou edição de campo não reseta o Aging; só transição de status conta.

**Por quê:** Ancorar na criação transformaria o Aging em "idade total do card", que é o Lead Time de um card ainda não terminado — redundante. Ancorar na última transição mede "há quanto tempo o card não se mexe", que é o sinal que denuncia as filas do board (os sete estágios de espera pós-desenvolvimento). Um card parado 12 dias úteis em "Aguardando Deploy" é o problema acionável; a idade desde o nascimento é menos acionável.

A âncora precisa ser transição de status, não última atualização qualquer, senão um comentário ou edição de descrição reseta o Aging e mascara um card travado há semanas.

**Afeta:** MET-04. Instrumenta a análise de Gargalos e serve de rede de segurança para bloqueio silencioso (Decisão 09).

---

## Decisão 06 — Feriados móveis

**Decidido:**
- Regra literal. Dias não-úteis = sábados, domingos, feriados nacionais e 25/01 (São Paulo).
- Sexta-feira Santa entra (feriado nacional).
- Carnaval, Quarta-feira de Cinzas e Corpus Christi contam como dias úteis (pontos facultativos, excluídos).
- Mantém a redação atual do doc 04 sem alteração.

**Por quê:** "Feriado nacional" é fato objetivo, verificável, que não muda de empresa para empresa nem de ano para ano por decisão de ninguém. Ponto facultativo é decisão organizacional. No momento em que a metodologia passa a incorporar "o que a empresa considera feriado", ela vira dependente de contexto local que um LLM externo não tem como saber — o que quebraria a autocontenção que é o objetivo da v3.0. A regra literal é a única que mantém o calendário derivável de fontes públicas sem input organizacional.

**Custo aceito conscientemente:** Lead Times e Cycle Times que atravessarem Carnaval ou Corpus Christi virão inflados por dias que ninguém trabalhou, e o time pode contestar. A escolha só se sustenta se, ao ser contestada, a resposta for "o número está correto pela definição da metodologia". A regra literal privilegia auditabilidade e comparabilidade histórica sobre percepção operacional.

**Consequência técnica:** o comando precisa da lista de datas por ano com Sexta-feira Santa pré-calculada, não só da regra — um LLM fraco erra o cálculo da Páscoa.

**Afeta:** todas as métricas temporais (MET-01 a MET-04, MET-07).

---

## Decisão 07 — Feriados nacionais e municipal

**Decidido:**
- Feriados nacionais = lista federal padrão, incluindo 20/11 (Consciência Negra) a partir de 2024.
- Único feriado municipal aplicável = 25/01 (São Paulo Capital).

**Por quê:** 20/11 virou feriado nacional por lei federal a partir de 2024. Como as coortes são de 2025 e 2026, ele entra em todas. Registrado explicitamente porque um LLM com corte de conhecimento anterior a 2024 omite esse feriado e infla em 1 dia útil qualquer métrica temporal que cruze 20/11 — erro silencioso que a lista fixa de datas previne.

**Afeta:** todas as métricas temporais.

---

## Decisão 08 — Modo de análise e nomenclatura de ausência

**Decidido:**
- Distinção adotada: **Não aplicável** (métrica sem sentido no modo) vs **Não calculável** (falta de dado).
- Introduzido o conceito de **modo de análise** (sprint / período) como classificação explícita na Validação das Entradas.
- Discriminador objetivo: existe baseline de planejamento (escopo comprometido no início da sprint) → modo sprint; coorte por data de resolução sem baseline → modo período.
- CORE-10 passa a ser condicional ao modo. No modo período, MET-05 e MET-06 = Não aplicável, e a seção Saúde da Sprint reporta fluxo de coorte (entrou / saiu / ainda aberto) em vez de Planejado × Executado.

**Por quê:** Planejado × Executado e Taxa de Conclusão precisam de baseline de sprint. Em análise por período, esse baseline não existe. "Não calculável" diz *faltou dado* e faria todo relatório periódico parecer incompleto, induzindo alguém a inventar um baseline artificial — exatamente o número inventado que a metodologia proíbe. "Não aplicável" diz *a pergunta não faz sentido neste modo*, sem lacuna a preencher.

A nomenclatura não executa sem a detecção de modo — o modelo não sabe qual rótulo aplicar se não sabe em que modo está. Por isso as duas decisões são inseparáveis: a detecção de modo é o que se decide, a nomenclatura é a saída correta uma vez que o modo existe. O discriminador (presença ou ausência de baseline) é binário e auditável, não depende de julgamento.

Isto quita o gap estrutural "os comandos assumem sprint em todo lugar", que estouraria na primeira análise periódica rodada num LLM externo. Análise periódica é caso de uso oficial (doc 01) e foi usada nas corridas de maio e junho.

**Afeta:** MET-05, MET-06. Altera CORE-10 e a Validação das Entradas do comando Operacional.

---

## Decisão 09 — Duração de bloqueio

**Decidido:**
- Causa do bloqueio: sempre do comentário (a flag não carrega causa).
- Duração, por card, em cascata de precedência:
  1. flag de bloqueio via changelog, se changelog disponível e flag usada;
  2. comentário datado de espera;
  3. nenhum → duração Não calculável; card visível só no Aging.
- Pré-condição: sem `expand=changelog`, o nível 1 é inacessível; declarar como limitação.
- Limitação de comparabilidade obrigatória: quando boards de maturidades diferentes entram no mesmo relatório, declarar quais usam flag e proibir comparação direta de contagem/duração de bloqueios entre eles.
- Aging (Decisão 05) permanece como rede de segurança para bloqueio silencioso.

**Por quê:** O board não tem status de bloqueio dedicado — um card bloqueado continua visualmente em "Desenvolvimento" ou "Aguardando Deploy", o status não muda quando trava. Ancorar a duração em transições de status daria duração zero a todo bloqueio sem mudança de coluna, perdendo justamente os bloqueios que mais importam: os invisíveis.

A flag é superior ao comentário quando existe, porque é evento binário e datado no changelog — elimina a interpretação de texto livre onde dois LLMs divergem. Mas alguns times não usam flag, então uma regra "flag primeiro" produziria comportamento inconsistente entre boards. A cascata resolve: a fonte não é escolhida por preferência, é escolhida pelo que existe naquele card. Mesma regra para todos; resultado difere porque os dados diferem.

A limitação de comparabilidade é séria e não aparece como "Não calculável" — aparece como número que parece válido e não é. Um board sem flag parece ter menos bloqueios quando na verdade tem menos bloqueios *documentados*. Comparar os dois sem ressalva seria enganoso, por isso a metodologia proíbe.

A pré-condição do changelog espelha a regra já existente de declarar Cycle Time não-auditável quando o changelog falta: sem ele, a data de adição/remoção da flag não é recuperável mesmo com a flag setada.

**Afeta:** MET-07.

---

## Decisão 10 — Base das progressões de épico e iniciativa

**Decidido:**
- Duas bases, sempre reportadas juntas, com rótulos fixos e nunca abreviados:
  - **Progressão do épico (portfólio):** Concluídos ÷ total de cards do épico × 100.
  - **Avanço no período:** concluídos no período ÷ cards do épico no universo × 100.
- Concluídos = só status CONCLUÍDO nas duas bases (Decisão 03).
- Fallback assimétrico: avanço no período sempre calcula; progressão do épico = Não calculável quando o épico completo não vier nas entradas. Nunca apresentar uma como a outra.
- O comando deve instruir o modelo a ler o contraste entre as duas bases, não só reportar os números.

**Por quê:** As duas bases respondem perguntas diferentes que a liderança faz na mesma reunião: "vamos entregar o épico?" (portfólio) e "esse épico andou neste período ou está parado?" (período). Nenhuma sozinha mostra o épico estagnado — um épico em 75% de portfólio com 0% de avanço no período é um épico travado perto do fim, e só as duas medidas juntas revelam isso.

Dois números exigem disciplina de rótulo: "progressão" genérica sem base declarada faz o leitor supor a que confirma o que ele já quer acreditar. Dois números mal rotulados é pior que um número, porque dá aparência de rigor a uma ambiguidade. Por isso os rótulos completos, sempre juntos.

O contraste entre as bases é ele próprio evidência: avanço alto e portfólio baixo = épico no começo, andando bem; avanço baixo e portfólio alto = quase pronto mas parado, provável dependência ou despriorização silenciosa; avanço zero e portfólio estável = abandonado sem cancelamento formal. Reportar só os números e não instruir a leitura do contraste seria coletar dois dados e perder a inferência que eles habilitam.

**Custo aceito:** progressão de portfólio exige que as entradas tragam o épico completo, não só os cards do período. Isso muda o contrato de entrada do comando Estratégico — a coleta passa a buscar, para cada épico tocado, todos os seus cards, inclusive fora da janela.

**Afeta:** MET-10, MET-11. Altera o contrato de entrada do comando Estratégico.

---

## Decisão 11 — Mudança de escopo em três componentes

**Decidido:** MET-09 é reportado em três componentes separados, nunca somados:
- Cards inseridos após o início da sprint;
- Cards removidos após o início da sprint;
- Cards com alteração de story points após o início da sprint (com a variação em pontos quando disponível).
Âncora: data de início da sprint. Não aplicável no modo período.

**Por quê:** Somar os três mistura fenômenos incompatíveis. Inserção e remoção medem instabilidade do compromisso da sprint; alteração de story points mede qualidade de estimativa. Uma sprint com 5 re-estimativas e zero cards mexidos teria o mesmo total de uma com 5 cards trocados e zero re-estimativas, e a leitura das duas é oposta. Além disso, inserção e remoção têm sinais opostos e podem se cancelar num total, escondendo churn severo (3 inseridos + 3 removidos = escopo inteiro trocado, não "zero mudança"). Resumo, se desejado, em duas medidas distintas: churn de escopo (inseridos + removidos) e volatilidade de estimativa (re-estimativas).

**Afeta:** MET-09. Não aplicável no modo período (não há início de sprint).

---

## Decisão 12 — Coorte e medidas do modo período

**Decidido:** No modo período, a coorte = cards resolvidos dentro do período (âncora: data de resolução). A Saúde da Sprint é substituída por análise de fluxo de coorte, com medidas: Lead Time e Cycle Time em distribuição (mín/mediana/máx), composição por tipo, por retrabalho e por bloqueio, e Throughput.

**Por quê:** Âncora de resolução dá coorte fechada e determinística — o mesmo intervalo retorna o mesmo conjunto em qualquer reexecução e qualquer modelo. "Atividade no período" dependeria de definir o que conta como atividade (transição, comentário, edição) e cada definição muda o conjunto, reintroduzindo a ambiguidade que o apêndice existe para eliminar.

O vocabulário "entrou / saiu / aberto" foi descartado: é enquadramento de fluxo contínuo (Kanban ao vivo), incoerente com coorte fechada retrospectiva, onde todo card já saiu por construção. A coorte por resolução mede como o conjunto fluiu (velocidade e composição), não balanço de entrada e saída.

Este modo não responde aderência a planejamento (não há baseline) nem WIP (backlog aberto ao fim do período é outra métrica e outra coorte). Distribuição em vez de só média porque a média isolada esconde os outliers, que são o sinal.

**Afeta:** substitui MET-05/06 no modo período. Usa MET-01, 02, 03, 07, 08.

---

## Consequências de escopo travadas por estas decisões

Três alterações fora do apêndice decorrem das decisões acima e precisam ser aplicadas quando os comandos forem reescritos:

1. **CORE-10 vira condicional ao modo** (Decisão 08). Deixa de ser "toda avaliação da Sprint usa Planejado × Executado" e passa a depender do modo detectado.

2. **Contrato de entrada do comando Estratégico fica mais pesado** (Decisão 10). Coleta passa a exigir épicos completos, não recortados por período. Toda instrução de coleta que hoje diz "cards do período" no contexto estratégico está incompleta.

3. **Lista fixa de feriados 2025–2026** (Decisões 06 e 07). Anexo do apêndice, com Sexta-feira Santa calculada por ano e 20/11 incluído. A regra do doc 04 permanece; deixa de depender de o LLM calcular Páscoa e conhecer a lei de 2024.
