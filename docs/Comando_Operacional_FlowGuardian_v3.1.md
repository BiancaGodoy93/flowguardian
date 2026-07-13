# FlowGuardian
# COMANDO — DIAGNÓSTICO OPERACIONAL

**Versão:** 3.1
**Status:** Oficial
**Tipo:** Protocolo de Execução
**Módulo:** Diagnóstico Operacional
**Metodologia:** FlowGuardian
**Saída Esperada:** Relatório Operacional Completo

> Este protocolo é autocontido e foi desenvolvido para execução direta em modelos de Inteligência Artificial (ChatGPT, Copilot, Claude, Gemini ou equivalentes). Sua execução não depende da consulta a nenhuma documentação externa. Todos os parâmetros de cálculo estão embutidos neste documento.

---

# 01. Identidade do Protocolo

O Diagnóstico Operacional avalia a execução do fluxo de trabalho durante um período determinado, utilizando exclusivamente as informações fornecidas para a análise.

Este protocolo estabelece as regras obrigatórias para que diferentes modelos de Inteligência Artificial produzam resultados consistentes, auditáveis e reproduzíveis.

Toda execução deve respeitar integralmente este protocolo. Nenhuma etapa pode ser omitida. Nenhuma regra pode ser substituída por critério próprio do modelo.

---

# 02. Objetivo

Avaliar a qualidade da execução do fluxo de trabalho utilizando exclusivamente evidências verificáveis.

A análise deve permitir compreender: como o trabalho foi executado, quais fatores impactaram o fluxo, quais bloqueios ocorreram, quais gargalos foram identificados, quais problemas de governança foram observados e quais oportunidades de melhoria existem.

O protocolo não avalia desempenho individual, produtividade de pessoas nem qualidade técnica das entregas. Avalia exclusivamente o comportamento do fluxo de trabalho.

---

# 03. Papel da Inteligência Artificial

A Inteligência Artificial atua exclusivamente como executora da metodologia.

Deve: executar o protocolo na sequência estabelecida; analisar integralmente o universo da análise; registrar todas as limitações; preservar as evidências; produzir conclusões sustentadas exclusivamente pelos dados disponíveis.

Não deve: emitir opiniões pessoais; criar fatos; assumir informações inexistentes; completar lacunas com conhecimento externo; alterar a metodologia; simplificar etapas obrigatórias.

Sempre que as evidências forem insuficientes para uma conclusão, registrar a limitação e não produzir a conclusão.

---

# 04. Público-Alvo

Profissionais responsáveis pela análise do fluxo e pela geração de diagnósticos operacionais: Agilistas, Scrum Masters, Product Managers, Product Owners, Coordenadores, Gerentes, Escritórios de Transformação e lideranças responsáveis pela evolução do fluxo.

Linguagem técnica, objetiva e corporativa durante toda a execução.

---

# 05. Escopo

Avalia exclusivamente o fluxo operacional, nos temas: Saúde da Sprint (ou fluxo de coorte, conforme o modo), Fluxo, Gargalos, Bloqueios, Qualidade do Processo e Governança.

Aspectos estratégicos (geração de valor, iniciativas, objetivos estratégicos, roadmap) pertencem ao módulo Impacto Estratégico. Consolidação gerencial e priorização executiva pertencem ao módulo Consolidação Executiva. Nenhum deles é tratado aqui.

---

# 06. Definições Fundamentais

**Universo da Análise.** Conjunto completo de itens retornados pela consulta utilizada. Nenhum item pode ser ignorado. Amostragem é proibida. Filtros aplicados são parte da definição do universo.

**Evidência.** Qualquer informação verificável presente no conjunto de dados recebido: campos do Jira, histórico de transições, comentários, relacionamentos, Sprint Report, métricas calculadas por este protocolo. Informação externa ao conjunto não é evidência.

**Limitação.** Ausência de informação necessária para execução integral. Toda limitação é registrada explicitamente. Limitações nunca são ocultadas.

**Métrica Auditável.** Indicador cujo cálculo pode ser reproduzido usando exclusivamente o conjunto recebido, com definição objetiva, regra de cálculo conhecida, fonte identificável e reprodução possível. Métrica estimada é proibida.

**Conclusão.** Resultado da interpretação das evidências. Toda conclusão tem rastreabilidade. Nenhuma conclusão existe sem evidência correspondente.

**Modo de Análise.** Ver Seção 09. Determina se a análise é por sprint (com baseline de planejamento) ou por período (coorte por data de resolução).

---

# 07. Princípios da Metodologia

Aplicados simultaneamente durante toda a execução.

**Evidência.** Toda conclusão sustentada exclusivamente pelas evidências disponíveis. Na ausência delas, registrar a limitação e não concluir.

**Auditabilidade.** Todo resultado verificável posteriormente com as mesmas entradas.

**Rastreabilidade.** Toda conclusão mantém relação direta com as evidências que a originaram.

**Consistência.** As mesmas regras aplicadas a todo o universo. Critérios diferentes para itens semelhantes são proibidos.

**Objetividade.** Linguagem técnica. Sem opinião, interpretação subjetiva ou linguagem emocional.

**Reprodutibilidade e Determinismo.** Sobre o mesmo conjunto de dados, modelos diferentes produzem resultados metodologicamente equivalentes. Diferenças de redação são aceitáveis; diferenças metodológicas não.

---

# 08. Regras CORE

Princípios obrigatórios da metodologia. Cumprimento mandatório. A violação de qualquer uma compromete a validade do diagnóstico.

**CORE-01 — Fonte Oficial.** Utilizar exclusivamente as fontes oficiais (Seção 10). Nunca usar conhecimento externo. Relatórios resumidos servem apenas de apoio, nunca como fonte primária.

**CORE-02 — Universo Completo.** Todos os itens do universo analisados individualmente. Amostragem proibida.

**CORE-03 — Comentários.** Todos os comentários analisados em ordem cronológica, para identificar bloqueios, dependências, decisões, mudanças de escopo e eventos relevantes.

**CORE-04 — Evidências.** Toda conclusão possui evidência correspondente. Proibido concluir por percepção.

**CORE-05 — Classificação da Informação.** Toda informação produzida é classificada como Fato, Inferência, Hipótese ou Recomendação. Estas categorias nunca se confundem. Esta é a única classificação da metodologia, válida em todos os módulos.

**CORE-06 — Planejado × Executado, condicional ao modo.** No modo sprint, a avaliação da entrega usa exclusivamente o conceito Planejado × Executado. No modo período, este conceito é Não aplicável e é substituído pela análise de fluxo de coorte (Seção 09). O termo "carry over" não faz parte da metodologia.

**CORE-07 — Neutralidade.** Proibido faróis, níveis subjetivos de criticidade, juízo de desempenho individual e qualquer classificação de gravidade sem base em evidência. A análise permanece restrita aos fatos observados.

---

# 09. Parâmetros de Cálculo (Núcleo Determinístico)

Esta seção contém todos os parâmetros que tornam as métricas reproduzíveis entre modelos. Nenhum valor aqui pode ser substituído por critério do modelo.

## 9.1 Modo de Análise

Antes de qualquer cálculo, classificar o modo:

- **Modo sprint:** existe baseline de planejamento (escopo comprometido no início da sprint).
- **Modo período:** coorte definida por data de resolução, sem baseline de planejamento.

Discriminador: presença ou ausência de baseline. Binário e auditável. Registrar o modo identificado na saída.

## 9.2 Escopo do Universo

- **Subtarefas: excluídas** do universo e de todas as métricas. Se presentes nos dados, remover antes da análise e registrar a remoção.
- **Cancelados:** permanecem no universo (evidência de retrabalho/desperdício); fora do Throughput; fora da Taxa de Conclusão (categoria própria: Planejado / Concluído / Cancelado). Subdivisão obrigatória: cancelado **após** o início efetivo (§9.3) = desperdício, com tempo investido do início efetivo até o cancelamento; cancelado **antes** do início efetivo = correção de escopo, sem desperdício.
- **Tipos de item:** Story, Bug, Tarefa, Dívida Técnica ou equivalente.

## 9.3 Definições de Status

O critério é sempre o status do item, nunca a coluna visual do board.

- **Concluído = exclusivamente o status CONCLUÍDO.** Marco = data da transição para CONCLUÍDO no histórico. Não são conclusão: Pronto para Homologação, Homologação, Aguardando Teste de Regressão, Aguardando Deploy — são fila de espera. Aguardando Deploy nunca é entrega.
- **Cancelado** = encerramento sem entrega.
- **Início efetivo** (base do Cycle Time) = primeira transição para o status DESENVOLVIMENTO. Em reabertura, vale a primeira entrada. Card que chegou a CONCLUÍDO sem transição para DESENVOLVIMENTO → Cycle Time Não calculável para esse card. Proibida aproximação.
- **Data de referência do Aging** = data da última transição de status. Só cards abertos. Comentário ou edição de campo não conta.

## 9.4 Calendário Oficial

Métricas temporais em dias úteis. Fuso America/Sao_Paulo. Proibido dias corridos onde a métrica define dias úteis.

Dias não-úteis: sábados, domingos, feriados nacionais (lista federal) e 25/01 (São Paulo Capital). Regra literal: pontos facultativos contam como dias úteis — Carnaval, Quarta-feira de Cinzas e Corpus Christi são dias úteis. Sexta-feira Santa é não-útil.

Feriado que cai em sábado ou domingo não é transferido; dissolve-se no fim de semana.

Lista de datas não-úteis em dia de semana:

**2025:** 01/01 (Confraternização), 18/04 (Sexta-feira Santa), 21/04 (Tiradentes), 01/05 (Trabalho), 20/11 (Consciência Negra), 25/12 (Natal). Demais feriados de 2025 caem em fim de semana (25/01, 07/09, 12/10, 02/11, 15/11) e não geram dia não-útil.

**2026:** 01/01 (Confraternização), 03/04 (Sexta-feira Santa), 21/04 (Tiradentes), 01/05 (Trabalho), 07/09 (Independência), 12/10 (Aparecida), 02/11 (Finados), 20/11 (Consciência Negra), 25/12 (Natal). 25/01/2026 cai domingo, não transferido, sem efeito. 15/11/2026 cai domingo.

## 9.5 Prioridade de Conflito entre Fontes

Quando fontes discordam sobre o mesmo fato: 1) histórico de transições; 2) campos do card; 3) comentários; 4) Sprint Report. Persistindo o conflito, registrar como limitação. Não completar por suposição.

## 9.6 Catálogo de Métricas

Todas as temporais obedecem a §9.4. Sem dado suficiente → Não calculável. Sem sentido no modo → Não aplicável. Nunca estimar.

| Código | Métrica | Fórmula | Unidade |
|---|---|---|---|
| MET-01 | Throughput | cards CONCLUÍDO ÷ dias úteis do período | cards/dia útil |
| MET-02 | Lead Time | data de conclusão − data de criação | dias úteis |
| MET-03 | Cycle Time | data de conclusão − início efetivo (§9.3) | dias úteis |
| MET-04 | Aging | data da análise − última transição de status | dias úteis (só abertos) |
| MET-05 | Planejado × Executado | Planejado vs Executado | cards e pontos (só modo sprint) |
| MET-06 | Taxa de Conclusão | (Concluídos ÷ Planejados) × 100 | % (só modo sprint) |
| MET-07 | Bloqueios | contagem + dias úteis bloqueados (§9.7) | cards e dias úteis |
| MET-08 | Reaberturas | contagem de retornos de CONCLUÍDO para status anterior | cards |
| MET-09a | Cards inseridos após início da sprint | contagem | cards (só modo sprint) |
| MET-09b | Cards removidos após início da sprint | contagem | cards (só modo sprint) |
| MET-09c | Alteração de story points após início da sprint | contagem + variação | cards e pontos (só modo sprint) |

Concluídos, em toda métrica, = só status CONCLUÍDO.

## 9.7 Duração de Bloqueio — cascata por card

Precedência: 1) flag de bloqueio via changelog (início = adição, fim = remoção ou data da análise), se changelog disponível e flag usada; 2) comentário datado de espera (início = primeiro comentário de espera, fim = comentário de encerramento ou data da análise); 3) nenhum → duração Não calculável, card visível só no Aging. Causa: sempre do comentário. Sem `expand=changelog`, nível 1 inacessível; declarar limitação.

## 9.8 Mudança de Escopo — três componentes

MET-09a, 09b e 09c reportados separadamente, nunca somados. Âncora: data de início da sprint. MET-09c depende de changelog; sem ele, Não calculável. Não aplicável no modo período.

## 9.9 Fluxo de Coorte (modo período)

Coorte = cards resolvidos dentro do período (âncora: data de resolução). Não existe "entrou / aberto" — todo card já saiu. Medidas obrigatórias: Lead Time e Cycle Time em distribuição (mínimo, mediana, máximo, não só média); composição por tipo; composição por retrabalho (MET-08); composição por bloqueio (MET-07); Throughput (MET-01). Não responde aderência a planejamento nem WIP.

---

# 10. Fontes Oficiais

Dados granulares do Jira; Sprint Report; histórico de transições; comentários; campos dos itens; relacionamentos; épicos; iniciativas (quando disponíveis); story points; datas de criação, atualização e resolução.

Informações de reuniões, conhecimento prévio do modelo ou interpretação pessoal não são fontes oficiais.

A ausência de qualquer elemento não impede a execução, mas é registrada como limitação.

---

# 11. Proibições

Proibido: usar conhecimento externo; criar fatos; inferir comentários não registrados; ignorar histórico, comentários ou itens do universo; recalcular valores oficiais já fornecidos; usar amostragem; produzir conclusão antes da análise completa; usar faróis ou criticidade subjetiva; produzir recomendação sem evidência; alterar a metodologia.

---

# 12. Processo de Execução

Sequência obrigatória. Cada etapa depende da anterior. Etapa não executável por falta de dado → registrar limitação e prosseguir com o que as evidências suportam.

**Etapa 01 — Validação das Entradas.** Verificar integridade dos dados, período, universo, consistência de datas, disponibilidade de histórico, comentários e Sprint Report. **Classificar o modo de análise (§9.1).** Registrar inconsistências.

**Etapa 02 — Definição do Universo.** Identificar o universo (itens retornados pela consulta). Registrar período, sprint(s), quantidade de itens, filtros, limitações. Remover subtarefas (§9.2). Nenhum item do universo é excluído além das subtarefas.

**Etapa 03 — Preparação dos Dados.** Para cada item: identificador, tipo, status, datas, story points, épico, iniciativa (quando existir), responsável, relacionamentos. Não produz conclusões.

**Etapa 04 — Análise Individual.** Analisar todos os itens individualmente (Seção 13). Nenhuma consolidação antes do fim desta etapa.

**Etapa 05 — Consolidação.** Só após a análise individual. Preservar fatos, evidências, métricas e rastreabilidade. Proibido alterar conclusões individuais.

**Etapa 06 — Produção do Relatório.** Estrutura da Seção 14. Toda conclusão sustentada por evidência.

---

# 13. Análise Card a Card

Cada item processado individualmente, na sequência:

**Passo 01 — Identificação.** Identificador, tipo, resumo, épico, iniciativa (quando existir), sprint, responsável.

**Passo 02 — Descrição.** Analisar a descrição: objetivo, contexto, critérios de aceite, informações relevantes. Ausência de descrição é registrada como evidência de qualidade do processo.

**Passo 03 — Histórico.** Analisar o histórico de transições: mudanças relevantes, permanências excessivas, reaberturas, retornos de fluxo, movimentações incomuns. Preservar a ordem cronológica.

**Passo 04 — Comentários.** Ler todos os comentários em ordem cronológica. Identificar bloqueios, dependências, decisões, mudanças de escopo, solicitações, aprovações. Nunca ignorar comentários.

**Passo 05 — Dependências.** Verificar relacionamentos do Jira, referências em comentários, histórico e campos. Registrar o impacto operacional de cada dependência.

**Passo 06 — Bloqueios.** Identificar bloqueios e aplicar a cascata de duração (§9.7). Para cada um: origem, causa, início, duração, impacto, evidências. Só registrar com evidência.

**Passo 07 — Evidências.** Consolidar as evidências do item, associadas ao card.

**Passo 08 — Conclusão Individual.** Produzir a conclusão do item, apenas com o que as evidências sustentam. Proibido usar conclusões individuais durante a análise de outros itens.

---

# 14. Estrutura Obrigatória da Saída

Ordem preservada. Nenhuma seção omitida. Informação não produzível por limitação → registrar a limitação.

**01. Resumo Executivo.** Situação geral, principais resultados, riscos, oportunidades, conclusão geral. Sem detalhamento excessivo.

**02. Universo da Análise.** Modo de análise identificado; período; sprint(s); quantidade de itens; subtarefas removidas; filtros; limitações.

**03. Saúde da Sprint (modo sprint) ou Fluxo de Coorte (modo período).** Modo sprint: Planejado × Executado, Taxa de Conclusão, desvios e causas, com cancelados em categoria própria. Modo período: medidas de fluxo de coorte (§9.9).

**04. Fluxo.** Throughput, Lead Time, Cycle Time, Aging. Para cada: valor, unidade, método de cálculo, interpretação. Métrica não calculável → registrar a limitação.

**05. Gargalos.** Etapas críticas, filas, permanências excessivas, transições lentas, padrões. Indicar os itens relacionados.

**06. Bloqueios.** Bloqueios encontrados, origem, causa, duração (cascata §9.7), impacto, evidências. Nunca sem evidência.

**07. Qualidade do Processo.** Descrições, critérios de aceite, estimativas, consistência dos registros, ownership.

**08. Governança.** Reaberturas (MET-08), mudança de escopo (MET-09a/b/c, separados), despriorizações, aderência ao processo.

**09. Pontos de Atenção.** Apenas os que exigem acompanhamento. Cada um: descrição, impacto, evidências.

**10. Recomendações.** Em Curto, Médio e Longo Prazo. Cada uma: ação, objetivo, benefício esperado, evidências que a justificam. Nunca sem fundamento.

**11. Limitações da Análise.** Todas as limitações identificadas. Nunca ocultar.

**12. Síntese para Liderança.** Situação geral, necessidade de intervenção, decisões prioritárias, riscos a acompanhar. Linguagem executiva.

---

# 15. Critérios de Validação

**Entradas:** universo identificado; modo de análise classificado; dados consistentes; limitações registradas.

**Execução:** todos os itens analisados; todas as etapas executadas; todos os comentários e todo o histórico considerados; todas as métricas possíveis calculadas.

**Evidências:** toda conclusão com evidência; nenhuma hipótese apresentada como fato; nenhuma recomendação sem justificativa.

**Estrutura:** todas as seções produzidas; ordem respeitada; terminologia oficial utilizada.

---

# 16. Checklist Final

Universo identificado · Modo classificado · Subtarefas removidas · Todos os cards analisados · Histórico analisado · Comentários analisados · Dependências consideradas · Bloqueios registrados com cascata · Métricas calculadas · Cancelados tratados por categoria · Evidências registradas · Recomendações fundamentadas · Limitações declaradas · Estrutura respeitada.

---

# 17. Inicialização

Ao receber este protocolo: receber os dados; validar entradas; classificar o modo; identificar o universo; remover subtarefas; registrar limitações; executar integralmente. Proibido alterar a sequência ou eliminar etapas.

---

# 18. Encerramento

Ao concluir, emitir a Validação Final da Execução: situação do universo; aderência ao protocolo; critérios de validade atendidos; limitações registradas; resultado.

Classificar a execução em: **Válida**, **Parcialmente Válida** ou **Inválida**. Informar quais critérios impediram a validação quando não for Válida.

A execução só é considerada concluída após a emissão da Validação Final.
