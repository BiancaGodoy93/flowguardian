# FlowGuardian — Registro da Sessão e Próximos Passos

**Data da sessão:** Julho/2026
**Objetivo da sessão:** validar a revisão da metodologia e iniciar a construção do núcleo determinístico e dos comandos v3.1.

---

## Onde paramos

Comando Operacional v3.1 reescrito e entregue. Aguardando validação. Estratégico e Executivo ainda não reescritos.

---

## O que foi decidido (fechado, não reabrir sem motivo)

### Direção estrutural
- **Reescrita B confirmada:** os comandos são a fonte autoritativa; a documentação vira material explicativo (onboarding, racional, glossário, governança) e deixa de conter regra executável.
- **Apêndice quantitativo embutido em cada comando** (não documento externo referenciado), para preservar autocontenção. Duplicação entre os três comandos é aceita por design.

### As doze decisões metodológicas (D01–D12)
Registradas em detalhe com racional em `FlowGuardian_Registro_de_Decisoes.md`. Resumo:
- D01 Subtarefas excluídas.
- D02 Cancelados no universo, fora de Throughput e Taxa de Conclusão, subdivididos em desperdício (após início efetivo) e correção de escopo (antes).
- D03 Concluído = só status CONCLUÍDO; coluna visual não é critério.
- D04 Início efetivo = primeira transição para DESENVOLVIMENTO; Não calculável se ausente.
- D05 Aging ancorado na última transição de status; só cards abertos.
- D06 Feriados: regra literal; Carnaval e Corpus Christi contam como dias úteis; só Sexta-feira Santa entra.
- D07 Nacionais federais + 20/11 (desde 2024) + 25/01 SP; feriado em fim de semana não transfere.
- D08 Modo de análise (sprint/período); MET-05/06 Não aplicável no período; CORE condicional ao modo.
- D09 Duração de bloqueio em cascata: flag via changelog → comentário datado → Não calculável.
- D10 Progressões em duas bases (portfólio e período), sempre juntas, rótulos completos.
- D11 Mudança de escopo em três componentes separados (inseridos, removidos, story points), nunca somados.
- D12 Coorte do modo período por data de resolução; medidas de tempo de fluxo e composição.

### Renumeração das famílias de regras
- **CORE reaberto: 7 princípios** (Fonte oficial, Universo completo, Comentários, Evidências, Classificação, Planejado×Executado condicional ao modo, Neutralidade). Histórico e Descrição desceram para o Processo; Métricas virou parâmetro no apêndice. De-para em `FlowGuardian_CORE_Renumeracao_DePara.md`.
- **ESTR: 5 princípios próprios.** Fontes/Evidências/Classificação viraram referência ao CORE; Métricas viraram apêndice. De-para em `FlowGuardian_ESTR_EXEC_Renumeracao_DePara.md`.
- **EXEC: 4 princípios próprios.** Seis das dez EXEC eram eco do CORE ou instrução de saída. De-para no mesmo arquivo.
- **Classificação: opção A fechada.** As 4 categorias do CORE (Fato/Inferência/Hipótese/Recomendação) são a única classificação da metodologia. Risco/Oportunidade/Decisão no Executivo são seções de saída, não taxonomia. Justificativa: o Executivo é proibido de criar risco/oportunidade novo, então não pode ter categoria de classificação própria.
- **Validade ternária** (Válida/Parcialmente Válida/Inválida) confirmada nos comandos; a doc se corrige na reescrita.

### Contexto de dados travado (do board real)
- Boards Dev Revenda (4148) e Dev Frota (2726). Mesmos status e nomes nos dois.
- Status terminais: CONCLUÍDO (entrega) e CANCELADO (encerramento sem entrega).
- Coluna "ITENS CONCLUÍDOS" agrupa 7 status; só CONCLUÍDO é entrega. Os demais (Homologação, Aguardando Teste de Regressão, Aguardando Deploy, Pronto para Homologação) são fila.
- Status de trabalho = DESENVOLVIMENTO. Não há status de bloqueio dedicado.
- Flag de bloqueio: alguns times usam, outros não → cascata da D09.
- Análises periódicas rodam sempre um board por vez → limitação de comparabilidade de bloqueio não entra no comando.

---

## Artefatos produzidos nesta sessão

| Arquivo | Estado |
|---|---|
| `FlowGuardian_Registro_de_Decisoes.md` | Completo (D01–D12 com racional) |
| `FlowGuardian_Apendice_Quantitativo_CONSOLIDADO.md` | Congelado |
| `FlowGuardian_CORE_Renumeracao_DePara.md` | Aprovado |
| `FlowGuardian_ESTR_EXEC_Renumeracao_DePara.md` | Aprovado (classificação = opção A) |
| `Comando_Operacional_FlowGuardian_v3.1.md` | Entregue, aguardando validação |

Os três `.txt` originais (v3.0) são o ponto de partida; a v3.1 os substitui à medida que forem reescritos.

---

## Próximos passos (em ordem)

### 1. Validar o Comando Operacional v3.1
Pontos abertos deixados na entrega, a decidir antes de considerar fechado:
- **Numeração de versão:** ficou v3.1 porque a estrutura mudou de forma incompatível com os .txt. Decidir se a "3.0 a congelar" é esta (então renomear) ou se 3.1 é o número certo.
- **Volume de texto:** o Operacional foi condensado em relação ao .txt (Princípios, Papel da IA, Proibições mais enxutos). Confirmar se a redução é aceitável ou se a repetição do original era intencional para reforço do LLM.
- **MET-09 na saída:** aparece como três linhas (09a/b/c) na Governança, não uma. Confirmar que é o formato desejado.

### 2. Reescrever o Comando Estratégico v3.1
- Aplicar ESTR reaberto (5 princípios) e o corte princípio/processo/parâmetro.
- Embutir o recorte estratégico do apêndice: MET-10/10b/11/11b, cadeia de valor, calendário, prioridade de conflito.
- **Alteração de contrato de entrada (D10):** a coleta passa a exigir épicos e iniciativas completos, não recortados por período. Toda instrução de coleta que hoje diz "cards do período" no contexto estratégico está incompleta. Este é o ponto mais pesado do Estratégico — decidir como o comando trata a ausência do épico completo (Não calculável na progressão de portfólio, avanço no período sempre calcula).
- Recuperar a seção de Rastreabilidade / itens órfãos que existia no doc 06 e sumiu do comando .txt.

### 3. Reescrever o Comando Executivo v3.1
- Aplicar EXEC reaberto (4 princípios) + referências ao CORE.
- Risco/Oportunidade/Decisão como seções de saída (opção A).
- Reavaliar o formato/peso do EXEC (adiado nesta sessão): decidir se quatro regras justificam comando de peso igual aos outros dois ou se ele é um pós-processador. Não fundir — tem público e uso próprios.
- Reintroduzir "Indicadores Auditáveis" e a tabela de sprints que o doc 07 exigia e o comando .txt não trazia.

### 4. Especificações de geração de relatório (bloco ainda não iniciado)
Explicitamente fora de escopo até aqui, a ser adicionado depois dos três comandos: estrutura visual, formatação, componentes obrigatórios, tabelas/gráficos, identidade visual, navegação. Não é ausência da metodologia; é etapa posterior.

### 5. Reescrever a documentação (última camada)
Só depois dos comandos fechados. Na Reescrita B:
- 02/03/04 (CORE, Engine, Métricas) perdem a parte normativa e viram explicativos finos apontando para os comandos, gastando o texto no racional (por que card a card, por que dias úteis) — que hoje não existe.
- 08 (Prompt Master) contradiz a premissa autocontida: vira índice de seleção de comando ou é aposentado. Não reescrever mantendo a função de "orquestrador que referencia a documentação".
- Corrigir na mesma passada: numeração CORE (para a nova de 7), validade ternária, classificação única.
- 01, 09, 10 estão majoritariamente bons; ajuste pontual, não reescrita.

---

## Pontos de atenção que não são decisão, mas pesam

- **Determinismo real depende do apêndice inteiro embutido.** Enquanto Estratégico e Executivo não forem reescritos com seus recortes, a afirmação de "resultado equivalente em qualquer LLM" só vale para o Operacional.
- **D10 tem custo de coleta, não de cálculo.** A progressão de portfólio vai cair em Não calculável na maioria das análises até a coleta mudar para trazer épicos completos. Decidir se isso é aceitável no curto prazo ou se a coleta muda antes.
- **Ambiguidades resolvidas por padrão nesta sessão que valem revisão:** definição operacional de MET-08 (retorno de CONCLUÍDO) e de MET-09c (depende de changelog). Ambas foram preenchidas para não deixar fórmula oca; se a leitura real do time for outra, ajustar.
- **SSOT ainda em risco até a doc ser reescrita.** Hoje o CORE existe nos comandos e na doc com numerações diferentes. Só fecha quando a doc nascer sobre a numeração nova.
